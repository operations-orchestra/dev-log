# Anonymizer: design decisions

*Status: agreed design for pass 1 and the pass-2 contract, 2026-11-20. The pass-2 model choice is still open and goes to a team vote (last section).*

The anonymizer removes personal identifiers from every raw record before anything enters the Record. It works in two passes:

- **Pass 1** is deterministic. It replaces the names of people on shift with their operational role.
- **Pass 2** is a locally hosted model. It finds the names, initials and addresses that pass 1 missed.

No key from name to role is kept, so the result cannot be reversed.

## Hard rules

These are also recorded in the project `CLAUDE.md`.

- **The shift list and the people directory never leave their machine.** They are never committed to any repository. Only synthetic `*.example.yaml` files are tracked.
- **Raw text never reaches a hosted model.** Pass 2 talks only to a model on the same machine or on the experiment's private network. The anonymizer refuses to start if its model endpoint is anywhere else.

## Shift list: one YAML file per shift

```yaml
# $ORCHESTRA_SHIFTLIST/2040-03-01_morning.yaml
start: 2040-03-01T07:00
end:   2040-03-01T15:00
timezone: Europe/Zurich
crew:                                  # list of postings
  - roles:  [DQM shifter, DCS shifter] # set of roles
    people: [123456]                   # set of people, by directory id
  - roles:  [HCAL DOC]
    people: [234567]
```

- **Time window:** `start` and `end` are written in every file. Overlapping files are combined, which covers hand-overs, and gaps are allowed.
- **Postings:** a posting means each listed person held all the listed roles during the shift.
- **On-call people** are listed in every shift they cover. There are no standing roles.
- **Validation:** if anything is invalid (an unknown id, a missing field, an empty crew), the loader refuses to start and names the file and line. A silently skipped shift would leak names.

## People

- **Directory:** a `PeopleDirectory` interface, with one implementation per collaboration, backed by that collaboration's authoritative list. For each id it gives `familyname`, `givenname`, `emails` and `logins`.
- **Overlay:** a local, git-ignored file adds what no official directory holds: `nicknames`, `spellings`, and `aliases` in any script (matched exactly).
- **Refresh:** the directory is read as a snapshot when the anonymizer starts and refreshed daily. The snapshot is kept in memory only.
- **Tests:** a YAML implementation with `people.example.yaml`.

```yaml
# overlay (git-ignored)
234567: {nicknames: [Helen], aliases: [余丽华]}
345678: {nicknames: [Mo], spellings: [Muhammad, Muhamad, Mohammed]}
```

## Pass 1: deterministic matching

- **Who is matched:** only people on shift at the record's time. Everyone else is left to pass 2.
- **Generated variants:**
  - both name orders (Li Hua Yu / Yu Li Hua)
  - given names joined or hyphenated (Lihua, Li-Hua)
  - "Family, Given"
  - initial plus family name, and given name plus initial
  - given name alone, and family name alone
  - nickname plus family name (Helen Yu)
  - logins, emails, and possessives ("Jane's")
- **Initials** match only when they are listed in the person's nicknames, never generated automatically, because HB, HE, HF and HO are detector names.
- **Normalisation:**
  - NFKC, case-folded, accents stripped (José = Jose)
  - ü→ue and ß→ss also generated as variants
  - name particles optional (van der, al-, bin, de la)
  - hyphens and spaces interchangeable
- **Misspellings:** Damerau–Levenshtein distance ≤ 1 for names of 5–7 characters and ≤ 2 for 8 or more. So Mohammad, Muhammad and Muhamad all match, and Mo comes from the nickname list. There is no built-in nickname table, since any such table is English-centric.
- **Short names** (3 characters or fewer: Yu, Li, Mo) match only as whole words, with the capitalisation in the directory, and never fuzzily.
- **Ambiguous hits:** a fuzzy hit that is also an ordinary or jargon word is left to pass 2.
- **Two people match one name:** prefer whoever is on shift. Otherwise use the roles they share, or `[person]` if they share none.
- **Fields scanned:** `text`, `author` (which becomes `author_role`, looked up at `t_recorded`), and every string value in `fields`.

## Replacement tokens

| Found | Becomes |
|---|---|
| A person on shift | `[<role>]`, e.g. `[HCAL DOC]` |
| A person with several roles | `[DQM shifter/DCS shifter]` |
| A possessive | `[HCAL DOC]'s` |
| A person with no known role | `[person]` |
| An e-mail address | `[email]` |

## Pass 2: model contract (decided)

- **When it runs:** on every record that has text, after pass 1. It receives pass 1's uncertain spans as hints.
- **What it handles:** context. In "HB turned off the HO", HB is a person and HO is the detector.
- **What it returns:** spans only, as JSON listing the exact substrings and their kind (name, initials, email, login). The code does the replacement; the model never rewrites text.
- **How spans are replaced:** a span becomes `[person]`, unless pass 1 can link it to someone on shift, in which case it gets their role.

## Code and packaging

- **`anonymizer` repo, feature branch:**
  - `shiftlist.py`, `people.py`, `variants.py`, `matcher.py`
  - `model.py`: the pass-2 interface plus a stub
  - the example YAML files, and a `.gitignore` for the real ones
- **Tests**, all on synthetic data:
  - Mohammad / Muhammad / Muhamad / Mo
  - Li Hua Yu / Yu Li Hua / Helen Yu / Yu
  - HB and HO collisions
  - two people with the same given name
  - misspellings
  - the pass-2 stub, and a marked test that runs against the real model
- **`utils` repo, feature branch:**
  - a `Dockerfile` on a pixi base image, built from `pixi.lock`, containing all Orchestra packages (`rapidfuzz` added to `pixi.toml`)
  - `docker-compose.yml` with an internal-only network
  - model weights and the shift list are mounted at run time, never copied into the image

---

## Open: pass-2 model choice (team vote)

All four options run locally. The span-only contract above applies whichever one wins.

| Option | What | Pros | Cons |
|---|---|---|---|
| **A. llama.cpp server sidecar** | A small instruct LLM (e.g. Qwen-family 3–8B or Gemma-family 4B, GGUF) behind an OpenAI-compatible API | Reuses the existing `openai_compatible` backend; understands context; runs on CPU | 2–6 GB of weights; seconds per record on CPU |
| **B. Ollama sidecar** | The same models as A | Simple model management (`ollama pull`); OpenAI-compatible | Another daemon; less control over how the model runs |
| **C. In-process `llama-cpp-python`** | The model loaded inside the anonymizer container | One container, no network hop | Larger image, harder build, model not shared with other services |
| **D. NER model (GLiNER / spaCy / Presidio)** | Not an LLM; tags person spans directly | Very fast and small; gives spans by design | Weak on initials and jargon collisions; English-centric |

**Proposed:** A, with D as an optional cheap pre-filter later if speed becomes a problem.

**The vote should also settle:**

1. **Model family and size:** this trades recall on initials and non-English names against CPU time.
2. **GPU:** is one available where the raw records live? That decides whether a 7–8B model is practical.
3. **Speed budget:** how many records per day, and how much delay before a record reaches the Record is acceptable?
4. **Failure behaviour:** if pass 2 fails or times out, is the record held back (safe) or sent on with only pass 1 applied? Proposed: hold it back.
5. **Recall target for `audit()`:** what fraction of names marked by experts must be removed before the anonymizer is trusted?
