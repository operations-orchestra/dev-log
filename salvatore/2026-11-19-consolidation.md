# Salvatore: Splitting the prototype into the organization's repositories

Until now, the whole prototype lived in one repository, `example-device`, with a folder per Orchestra component named after the repository it would one day move to. Salvatore made that move: `utils`, `aggregator`, `anonymizer`, `summarizer`, `sparsifier` and `orchestrator` now each live in their own repository of the `operations-orchestra` organization, all on the branch `prototype/synthetic-record`. `example-device` keeps the synthetic device, the source adapters, the viewer, the command line, the tests and the docs, and finds the other repositories as sibling checkouts.

## What Salvatore did

| Approve | Claim |
| :-- | --- |
| ☑ H1<br>🎯 Direction | Make `example-device` match the structure of the `operations-orchestra` organization: create the branch `prototype/synthetic-record` in every repository, and move the component folders of `example-device` into the repositories of the same name.<br>**Before:** six components as top-level folders of `example-device`; the other repositories held only a README and a licence.<br>**Now:** each repository holds its component as a package of the same name (`aggregator/aggregator/`, `utils/utils/`, ...), and `example-device` imports them from the sibling checkouts. All 108 tests still pass.<br>**Why key:** the components can now be developed, reviewed and owned separately, as the organization intended.<br>led_to: #A1, #A2, #A3, #A4 |
| ☑ H2<br>💡 Origination | There was no repository for the summarizer. Salvatore chose to create one for it rather than leave it in `example-device` or fold it into the anonymizer, and then created `operations-orchestra/summarizer` on GitHub.<br>**Example:** the local repository was started on the new branch and later based on GitHub's initial commit, so its history matches the other repositories.<br>**Why key:** completes the set of seven repositories the README now tells readers to clone.<br>led_to: #A6 |
| ☑ H3<br>🎯 Direction | Move `utils`, `anonymizer` and `orchestrator` out as well (the first request named only three components), and fix `pyproject.toml` so `example-device` packages only what is left in it.<br>refines: #H1<br>led_to: #A2, #A5 |

<details><summary>Also (3 more)</summary>

| Approve | Claim |
| :-- | --- |
| ☐ H4<br>🎯 Direction | Update the README of `example-device` to the new layout. |
| ☐ H5<br>📚 Knowledge | The Quick start block of the README fails when pasted into zsh: its `#` comments are passed to `orchestra` as arguments, and a `(...)` in a comment is read as a glob, so `synth` never runs and the later commands find no Record.<br>led_to: #Q1 |
| ☐ H6<br>🎯 Direction | Build a knowledge graph of the seven repositories with graphify before going further. |

</details>

## AI decisions

☐ All AI claims and minor details below are recorded accurately

| Endorse | AI decision |
| :-- | --- |
| ☐ A1 | Each component repository holds its code as a package folder of the same name, not at the repository root, so every `import aggregator` and the like works unchanged and the package's own README does not collide with the repository's.<br>depends_on: #H1 |
| ☐ A2 | `example-device` finds the sibling repositories through `PYTHONPATH`: pytest's `pythonpath` in `pyproject.toml`, and `[activation.env]` in `pixi.toml` for `pixi run orchestra`. The component repositories have no `pyproject.toml` yet, so they cannot be installed with pip.<br>depends_on: #H1, #H3 |
| ☐ A3 | The viewer's source links and its interfaces page find each package's files with `importlib` (`package_dir`, `source_path` in `viewer/api.py`) wherever it is installed; the read-only source page serves only files inside those packages.<br>depends_on: #H1 |
| ☐ A4 | `tests/test_boundaries.py` checks each package where it lives. Without this it would have skipped every moved folder silently, so the import rule would no longer have been tested.<br>depends_on: #H1 |
| ☐ A5 | The LLM profiles (`config/llm.yaml`, `config/llm.example.yaml`) stay in `example-device`; `orchestrator/llm_config.py` now looks for them under the working directory instead of next to its own package. `orchestra ask --profile` must therefore run from the root of `example-device`, or with `$ORCHESTRA_LLM_CONFIG` set.<br>depends_on: #H3<br>refines: 2026-11-17-record-and-agent#H16<br>Never discussed |
| ☐ A6 | The new branch in each component repository starts from its `main`; the summarizer's local branch was based on the initial commit GitHub created, whose README and licence were identical to the local ones.<br>depends_on: #H2 |
| ☐ A7 | The README now opens with a loop that clones the seven repositories side by side, and its folder table became a table of repositories, packages and states, with links; it explains how `PYTHONPATH` is set with and without pixi.<br>depends_on: #H4 |

<details><summary>Minor details (9)</summary>

- M1 Installed pixi (0.84.2, in `~/.pixi`); asked whether a local install could be removed. It is the only pixi on the machine; the project environment `example-device/.pixi` can be deleted and is rebuilt from `pixi.lock`.
- M2 Asked which repository had no GitHub remote (the summarizer).
- M3 Asked for all seven repositories to be committed, then pushed.
- M4 AI: each new repository got a `.gitignore` for `__pycache__/` and `*.pyc`, after test runs left compiled files staged (never discussed).
- M5 AI: the untracked `example-device/planning/` folder, present before the session, was left out of the commit (never discussed).
- M6 AI: graphify's output went to `operations-orchestra/graphify-out/`, outside every repository: 1,058 nodes, 2,184 edges, 62 communities, 212,097 tokens for reading the 18 documents. `RecordStore` is the main bridge between communities.
- M7 AI: `aggregator/schema.sql` added nothing to the graph, because graphify's SQL parser is not installed (never discussed).
- M8 AI: the 154 dangling edges graphify reported are imports of the standard library and pytest, not missing code.
- M9 AI: before the move the tests passed 108 of 108; right after it, 4 failed (viewer and LLM config paths) until #A3 and #A5.

</details>

## Open questions
- Q1: Rewrite the README's Quick start so it pastes cleanly into zsh, with the explanations outside the code block (offered, not done). Until then, `setopt interactive_comments` works around it.
- `docs/DESIGN.md` still describes the components as folders of one repository (for example the decision "folders named after repos").
- The component repositories have no `pyproject.toml`; adding one to each would let `example-device` list them as ordinary dependencies instead of relying on `PYTHONPATH`.
- Suggested by the graph: why `RecordStore` links the write API to 15 other communities, now that every other repository depends on the aggregator.

<details><summary>Links and evidence</summary>

- H1, H3, A1–A5 → example-device `0d616f3` "Move the Orchestra components into their own repositories"
- A1, M4 → utils `4346b50`, aggregator `5f3c0eb`, anonymizer `9ae73cf`, sparsifier `d2dfb74`
- H2, A6 → summarizer `61fcaa1`, on top of GitHub's initial commit `35b4ecd`
- A5 → orchestrator `1be90a4` (`orchestrator/llm_config.py`), example-device `tests/test_agent.py`
- A2 → example-device `pyproject.toml`, `pixi.toml`
- A3, A4 → example-device `viewer/api.py`, `viewer/server.py`, `tests/test_boundaries.py`
- H4, A7 → example-device `README.md`
- H6, M6–M8 → `operations-orchestra/graphify-out/GRAPH_REPORT.md`
- graph → [2026-11-19-graph-report.md](2026-11-19-graph-report.md), rebuilt after this record moved to dev-log, without the uncommitted `example-device/planning/`
</details>

<details><summary>Record details</summary>

| Field | Value |
| --- | --- |
| claudoperation | 0.3 |
| session | 2026-11-19-consolidation |
| member | salvatore |
| product | example-device, utils, aggregator, anonymizer, summarizer, sparsifier, orchestrator (branch prototype/synthetic-record) |
| product_type | functional |
| span | 2026-11-19 |
| approval | individual |
</details>
