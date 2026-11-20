# Salvatore: Designing the anonymizer's two passes

The anonymizer was only a skeleton: a `RoleDirectory` protocol, an `Anonymized` result, and a docstring describing two passes. Salvatore set the strategy, and a design review ("grill me") then settled every branch of it except one:

- **Pass 1** replaces the names of people on shift with their operational role, using a shift list.
- **Pass 2** is a local model that finds names pass 1 missed or that only context reveals.

The design is written up in `design-docs/2026-11-20-anonymizer-design.md`, with a PDF for the team. Which model runs pass 2 goes to a team vote. No code was written in this session.

## What Salvatore did

| Approve | Claim |
| :-- | --- |
| ☐ H1<br>🎯 Direction | Two passes. Pass 1 uses a shift list that gives each person's position, not their name, and recognises nicknames, initials and misspellings. Pass 2, a bare-bones generic LLM, handles text where pass 1 is not enough.<br>**Why key:** fixes the shape of everything below.<br>led_to: #A1, #A7 |
| ☐ H2<br>🎯 Direction | Each shift entry maps a **set of roles** to a **set of people**, written as one YAML file per shift. A proposed `pattern` + `days` format, with three shifts a day in one file, was rejected: one file per shift is easier for people to read, and concatenating them is easy.<br>**Before:** a single file holding `role: [[last, first]: [nicknames]]`.<br>**Now:** `start`, `end`, `timezone`, and a `crew` of postings `{roles, people}`.<br>led_to: #A9 |
| ☐ H3<br>🛡 Constraint | Two hard rules, added to the project `CLAUDE.md`: the shift list never leaves its machine and is never committed, and raw text never reaches a hosted model.<br>**Why key:** they rule out hosted APIs for pass 2 and decide how the Docker image is built.<br>led_to: #A10, #A11 |
| ☐ H4<br>📚 Knowledge | "Ambiguous" means ambiguous in context, not to the software. In "HB turned off the HO", a model can tell that HO is the detector and HB a person, which pass 1 cannot. So pass 2 runs on every record that has text, not only on the ones pass 1 flags.<br>led_to: #A7 |
| ☐ H5<br>🎯 Direction | No standing roles: on-call people are listed in every shift they cover. Anyone not on shift at the record's time becomes `[person]`. |
| ☐ H6<br>💡 Origination | People come from an authoritative directory that can be queried and that is specific to each instrument's collaboration. The name fields are called `familyname` and `givenname`.<br>led_to: #A1, #A8 |
| ☐ H7<br>🎯 Direction | Pass 1 matches **only people on shift** at the record's time. This replaced the proposal to also match the whole collaboration directory exactly; everyone else is left to pass 2. |
| ☐ H8<br>🎯 Direction | Tests must not be English-centric. One case is Mohammad / Muhammad / Muhamad / Mo. Another is Li Hua Yu with the name order switched and an English nickname: Helen Yu, or just Yu.<br>led_to: #A4, #A5 |
| ☐ H9<br>🎯 Direction | Deploy through Docker from the start, with the Dockerfile in `utils`, and include **all** the Orchestra packages, not only the three the anonymizer needs.<br>led_to: #A10 |
| ☐ H10<br>🎯 Direction | The choice of the pass-2 model goes to a team vote. Salvatore asked for a Markdown summary of all the decisions in `dev-log/design-docs/`, plus a PDF that is easier to read. |

## AI decisions

☐ All AI claims and minor details below are recorded accurately

| Endorse | AI decision |
| :-- | --- |
| ☐ A1 | Postings refer to people by directory id. A local, git-ignored **overlay** adds what no official directory holds: `nicknames`, `spellings`, and `aliases` in any script. Repeating nicknames inside every shift would let a single missed copy leak a name.<br>depends_on: #H1, #H6 |
| ☐ A2 | Initials are matched only when they are listed in a person's nicknames, never generated automatically, because HB, HE, HF and HO are detector names. Fuzzy hits that are also ordinary or jargon words are left to pass 2. |
| ☐ A3 | Misspellings are matched with Damerau–Levenshtein distance ≤ 1 for names of 5–7 characters and ≤ 2 for 8 or more. Names of 3 characters or fewer (Yu, Li, Mo) match only as whole words, with the directory's capitalisation, and never fuzzily. |
| ☐ A4 | Normalisation: NFKC, case-folded, accents stripped, with ü→ue and ß→ss also generated as variants. Name particles are optional (van der, al-, bin, de la), and hyphens and spaces are interchangeable. Both name orders are always generated, and given names are also tried joined or hyphenated.<br>depends_on: #H8 |
| ☐ A5 | No built-in nickname table (such as Robert→Bob), because any such table is English-centric. Nicknames come only from the overlay and from pass 2.<br>depends_on: #H8 |
| ☐ A6 | Replacement tokens: `[<role>]`, several roles joined with `/`, possessives kept (`[HCAL DOC]'s`), `[person]` when no role is known, and `[email]` for addresses. When two people match one name, the one on shift wins. Otherwise their shared roles are used, or `[person]` if they share none. |
| ☐ A7 | Pass 2 returns spans only: JSON listing exact substrings and their kind. The code does every replacement, and the model never rewrites text. Pass 1's uncertain spans are passed in as hints.<br>depends_on: #H1, #H4 |
| ☐ A8 | The directory is read as a snapshot at start-up and refreshed daily, kept in memory only.<br>depends_on: #H6 |
| ☐ A9 | An invalid shift file (an unknown id, a missing field, an empty crew) stops the anonymizer at start-up with the file and line, because a skipped shift would leak names. Overlapping shift files are combined, which covers hand-overs.<br>depends_on: #H2 |
| ☐ A10 | The Docker image uses a pixi base and is built from `example-device/pixi.lock`, with every sibling repository on `PYTHONPATH`, and `rapidfuzz` is added to `pixi.toml`. The build context is `operations-orchestra/`. Model weights and the shift list are mounted at run time, never copied into the image. A compose file puts the model sidecar on an internal-only network.<br>depends_on: #H3, #H9 |
| ☐ A11 | The anonymizer will refuse to start unless its model endpoint resolves to localhost or a private network address, enforcing #H3 whatever LLM profile is configured.<br>depends_on: #H3 |

<details><summary>Minor details (6)</summary>

- M1 AI: read the existing skeleton first. `RoleDirectory.role_of(name, t)` already took a time, which is what pushed the shift list from a single table to timed entries.
- M2 AI: the roles in use come from `example-device/example_device/texts.py`: Shift leader, DAQ/DCS/DQM shifter, HCAL DOC, HCAL expert, Run coordinator.
- M3 AI: `rapidfuzz` is not yet in the pixi environment.
- M4 AI: the PDF was rendered from the Markdown with python-markdown (through `pixi exec`, not installed in the project) and headless Chrome. The first render flattened the nested lists, which were then fixed.
- M5 Asked for a summary of the decisions before any code was written, interrupting the start of the build.
- M6 AI: `CLAUDE.md` lives in `operations-orchestra/`, which is not a git repository, so the hard rules (#H3) are recorded only locally (never discussed).

</details>

## Open questions
- **The pass-2 model (team vote):**
  - A: a llama.cpp server sidecar
  - B: an Ollama sidecar
  - C: in-process `llama-cpp-python`
  - D: a NER model (GLiNER / spaCy / Presidio)

  The design doc proposes A.
- **Also for the vote:**
  - model family and size
  - whether a GPU is available where the raw records live
  - the speed budget
  - whether a record is held back or sent on when pass 2 fails (the proposal is to hold it back)
  - the recall target for `audit()`
- **The build is not started:** feature branches in `anonymizer` (`shiftlist.py`, `people.py`, `variants.py`, `matcher.py`, `model.py` stub, tests) and in `utils` (`Dockerfile`, `docker-compose.yml`).
- **Which collaboration directory to implement first,** and how it is queried, is not yet known.

<details><summary>Links and evidence</summary>

- H1–H10, A1–A11 → [design-docs/2026-11-20-anonymizer-design.md](../design-docs/2026-11-20-anonymizer-design.md) and its PDF
- H3, A11 → `operations-orchestra/CLAUDE.md`, section "Personal data: hard rules" (local, not in a repository)
- M1 → anonymizer `anonymizer/__init__.py` (skeleton, branch `prototype/synthetic-record`)
- A10 → example-device `pixi.toml`, `pyproject.toml` (how the sibling repositories are found today)
- graph → [2026-11-20-graph-report.md](2026-11-20-graph-report.md)
</details>

<details><summary>Record details</summary>

| Field | Value |
| --- | --- |
| claudoperation | 0.3 |
| session | 2026-11-20-anonymizer-design |
| member | salvatore |
| product | anonymizer, utils (design only; branch prototype/synthetic-record) |
| product_type | design |
| span | 2026-11-20 |
| approval | individual |
</details>
