# Graph Report - operations-orchestra  (2026-11-20)

## Corpus Check
- 69 files · ~71,245 words
- Verdict: corpus is large enough that graph structure adds value.
- Unclassified: 22 file(s) not represented in the graph (top: (none) 19, .lock 1, .toml 1)
- WARNING: 22 of 91 files seen (24%) have no supported extractor and are missing from this graph entirely. It may look complete while representing only part of the codebase.

## Summary
- 1073 nodes · 2194 edges · 68 communities (42 shown, 26 thin omitted)
- Extraction: 91% EXTRACTED · 9% INFERRED · 0% AMBIGUOUS · INFERRED: 207 edges (avg confidence: 0.88)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Record Store and Write API
- Control Archive and Incident Text
- Anonymizer Interface
- Viewer API Endpoints
- Aggregator Record Schema
- Viewer App Script
- Source Page Resolution
- Anonymizer Design Decisions
- Synthetic Event Generator
- GUI Plan and Pages
- LLM Profile Config
- Device Generation Entry
- Viewer Tests
- Device Config and Presets
- Entry Writes and Corrections
- As-of Calendar Reads
- Run Calendar Planning
- Incident Reads and Proposals
- Store Tests
- Repo Split Consolidation
- DQM Archive Adapter
- Precedent Replay
- Viewer Rendering Helpers
- Diagnosis Agent Core
- Sparsifier Interface
- Agent Tests
- Static Demo Export
- Aggregator Package and Schema Docs
- GUI Session Decisions
- Model Brain Tests
- Viewer Navigation and Replay
- Record Slimming Decisions
- Prototype Ground Rules
- LLM Example YAML
- Model Brain
- Control Readings Synthesis
- Import Boundary Test
- Data-Quality Synthesis
- Citation Check and Query Log
- Direct-Link Builder
- Operation Policy Config
- Viewer Page Mounting
- Viewer Charts
- Incident Views
- LLM Brain Decisions
- Scripted Brain and Confidence
- As-of Store Tests
- Record Schema Decisions
- Record Text Views
- Repository Layout
- Viewer Entry Rendering
- Entry Type Catalogue
- Aggregator Repo README
- Anonymizer Repo README
- Data-Quality Plots
- Detector Map Page
- Incident Page
- Read API Page
- Tables Page
- Orchestrator Repo README
- Example Package
- Sparsifier Repo README
- Summarizer Repo README
- Utils Repo README

## God Nodes (most connected - your core abstractions)
1. `RecordStore` - 130 edges
2. `_Gen` - 34 edges
3. `generate()` - 29 edges
4. `ControlArchive` - 22 edges
5. `call()` - 20 edges
6. `esc()` - 20 edges
7. `RecordTools` - 20 edges
8. `plot_element()` - 19 edges
9. `_as_of()` - 19 edges
10. `handle_api()` - 19 edges

## Surprising Connections (you probably didn't know these)
- `Record as one SQLite file, SQL confined to one module` --references--> `RecordStore`  [INFERRED]
  dev-log/martin/2026-11-16-orchestra-prototype-gui.md → aggregator/aggregator/store.py
- `HCAL-shaped seeded generator with hidden answers` --semantically_similar_to--> `Seeded synthetic generator`  [INFERRED] [semantically similar]
  dev-log/martin/2026-11-16-orchestra-prototype-gui.md → example-device/README.md
- `RecordStore` --implements--> `Operations Record`  [EXTRACTED]
  aggregator/aggregator/store.py → example-device/docs/DESIGN.md
- `Folder Dependency Rule (test_boundaries.py)` --rationale_for--> `RecordStore`  [EXTRACTED]
  example-device/docs/DESIGN.md → aggregator/aggregator/store.py
- `GUI remake (five ordered pages, replay as deliberate mode)` --semantically_similar_to--> `Six ordered browser pages (detector, build, contents, scenarios, replay, agent)`  [INFERRED] [semantically similar]
  dev-log/martin/2026-11-16-orchestra-prototype-gui.md → example-device/README.md

## Import Cycles
- 2-file cycle: `example-device/example_device/__init__.py -> example-device/example_device/generator.py -> example-device/example_device/__init__.py`

## Hyperedges (group relationships)
- **Evolution of Record content design (sparsification to status-change readings and part references)** — dev_log_martin_2026_11_16_orchestra_prototype_gui_sparsification, dev_log_martin_2026_11_17_record_and_agent_status_change_readings, dev_log_martin_2026_11_16_orchestra_prototype_gui_multi_element_cause, dev_log_martin_2026_11_17_record_and_agent_part_references, dev_log_martin_2026_11_17_record_and_agent_calendar_tables [INFERRED 0.85]
- **Precedent matching: rules, confidence, expert reviews, agent page** — dev_log_martin_2026_11_16_orchestra_prototype_gui_precedent_rules, dev_log_martin_2026_11_17_record_and_agent_precedent_confidence, dev_log_martin_2026_11_17_record_and_agent_precedent_reviews, dev_log_martin_2026_11_17_record_and_agent_agent_page [INFERRED 0.85]
- **Adaptations that keep example-device working after the repository split** — dev_log_salvatore_2026_11_19_consolidation_package_folder_layout, dev_log_salvatore_2026_11_19_consolidation_pythonpath_sibling_discovery, dev_log_salvatore_2026_11_19_consolidation_viewer_importlib_lookup, dev_log_salvatore_2026_11_19_consolidation_boundary_test_per_package, dev_log_salvatore_2026_11_19_consolidation_llm_profiles_location [EXTRACTED 1.00]
- **Agent diagnosis flow: tools, confidence, citation check** — example_device_docs_design_diagnosis_agent, example_device_docs_design_query_tools, example_device_docs_design_confidence_model, example_device_docs_design_citation_check, example_device_docs_design_precedent_table [EXTRACTED 1.00]
- **Record time-integrity properties** — example_device_docs_design_as_of_reads, example_device_docs_design_append_only, example_device_docs_design_state_lookback, aggregator_aggregator_readme_three_incident_labels [INFERRED 0.85]
- **Detector model migration to cmscoord** — example_device_docs_detector_plan_detector_interface, example_device_docs_detector_plan_toy_detector_model, example_device_docs_detector_plan_cmscoord_adapter, example_device_docs_detector_plan_lv_overlay, aggregator_aggregator_readme_part_ref [EXTRACTED 1.00]
- **GUI remake: ordered pages (detector, how built, what is in it, scenarios, replay)** — example_device_docs_gui_plan_gui_remake, example_device_docs_gui_plan_detector_map_page, example_device_docs_gui_plan_how_the_record_is_built_page, example_device_docs_gui_plan_tables_page, example_device_docs_gui_plan_scenarios_page, example_device_docs_gui_plan_replay_mode [EXTRACTED 1.00]
- **Operations Orchestra component repos** — aggregator_readme_aggregator, anonymizer_readme_anonymizer, orchestrator_readme_orchestrator, sparsifier_readme_sparsifier, summarizer_readme_summarizer, utils_readme_utils [INFERRED 0.85]
- **Anonymizer two-pass pipeline** — dev_log_design_docs_2026_11_20_anonymizer_design_pass_1_deterministic_matching, dev_log_design_docs_2026_11_20_anonymizer_design_pass_2_model_contract, dev_log_design_docs_2026_11_20_anonymizer_design_replacement_tokens, dev_log_design_docs_2026_11_20_anonymizer_design_shift_list [EXTRACTED 1.00]
- **Pass-2 local model options** — dev_log_design_docs_2026_11_20_anonymizer_design_option_a_llama_cpp_server_sidecar, dev_log_design_docs_2026_11_20_anonymizer_design_option_b_ollama_sidecar, dev_log_design_docs_2026_11_20_anonymizer_design_option_c_in_process_llama_cpp_python, dev_log_design_docs_2026_11_20_anonymizer_design_option_d_ner_model [EXTRACTED 1.00]
- **Personal-data hard rule enforcement** — dev_log_design_docs_2026_11_20_anonymizer_design_hard_rules, dev_log_salvatore_2026_11_20_anonymizer_design_private_endpoint_check, dev_log_design_docs_2026_11_20_anonymizer_design_utils_docker_packaging, dev_log_salvatore_2026_11_20_anonymizer_design_project_claude_md [INFERRED 0.85]

## Communities (68 total, 26 thin omitted)

### Community 0 - "Record Store and Write API"
Cohesion: 0.05
Nodes (6): Replay helpers (incident_frame, became_known, ...), Write API (add_entry, supersede, open_incident, label_incident, ...), RecordStore, marks_detector(), scope(), meta()

### Community 1 - "Control Archive and Incident Text"
Cohesion: 0.07
Nodes (24): show_incident(), ControlArchive, _as_of(), _ask(), _demo(), _export_static(), _info(), main() (+16 more)

### Community 2 - "Anonymizer Interface"
Cohesion: 0.05
Nodes (12): Anonymized, Anonymizer, RoleDirectory, CertificationAdapter, DataQualityAdapter, DowntimeAdapter, ElogAdapter, RawRecord (+4 more)

### Community 3 - "Viewer API Endpoints"
Cohesion: 0.08
Nodes (32): agent(), agent_report(), ApiError, _archive_summary(), _as_of(), built(), demo_device(), demo_planted() (+24 more)

### Community 4 - "Aggregator Record Schema"
Cohesion: 0.05
Nodes (34): aggregator (owner of the Operations Record), aggregator README, Calendar tables (fill, run, beam_mode) and certification, part_ref table (parts with roles and times), query_log table, As-of Read API (entries, state_at, incidents, ...), view.py (orchestra info/show/plot), Operations Orchestra Prototype Design and Hand-off (+26 more)

### Community 5 - "Viewer App Script"
Cohesion: 0.06
Nodes (33): ALIAS, CLASS_NAME, CMP, DROP, DV, ER_POS, HINT, KIND_LABEL (+25 more)

### Community 6 - "Source Page Resolution"
Cohesion: 0.09
Nodes (13): _describe_module(), package_dir(), source_path(), Current, find_records(), make_handler(), do_GET(), do_POST() (+5 more)

### Community 7 - "Anonymizer Design Decisions"
Cohesion: 0.07
Nodes (24): Anonymizer, Anonymizer: design decisions, anonymizer repo modules (shiftlist.py, people.py, variants.py, matcher.py, model.py), audit() recall target, Option A: llama.cpp server sidecar, Option B: Ollama sidecar, Option C: in-process llama-cpp-python, Option D: NER model (GLiNER / spaCy / Presidio) (+16 more)

### Community 9 - "GUI Plan and Pages"
Cohesion: 0.06
Nodes (26): Agent panel in Replay and Agent page, Build-a-Record control (not built, open decision), Device page (detector map, calendar, fault catalogue), GUI Plan (understand and check what has been built), Hand-written SVG charts (buildChart, knowledgeChart) instead of uPlot, How the Record is built page, Interfaces of unbuilt parts page, LLM content marks and 'Who writes what' page (removed in remake) (+18 more)

### Community 10 - "LLM Profile Config"
Cohesion: 0.12
Nodes (10): test_git_holds_only_an_example_without_keys(), test_profiles_keep_keys_out_of_the_file_and_out_of_sight(), profiles(), config_path(), ConfigError, get_profile(), keys_path(), load_profiles() (+2 more)

### Community 11 - "Device Generation Entry"
Cohesion: 0.12
Nodes (13): preset(), generate(), SizeBudgetError, end(), store(), tiny(), test_budget_above_hard_cap_is_refused(), test_budget_too_small_is_refused() (+5 more)

### Community 12 - "Viewer Tests"
Cohesion: 0.13
Nodes (19): call(), _known_times(), test_built_page_examples_are_real_rows(), test_demo_endpoint_lists_each_planted_case_with_its_entries(), test_detector_map_shows_state_at_the_time_control(), test_diff_lists_what_was_learned_in_between(), test_incident_and_entry_pages_hide_what_is_not_yet_known(), test_interfaces_page_is_read_from_the_skeletons() (+11 more)

### Community 13 - "Device Config and Presets"
Cohesion: 0.14
Nodes (7): DeviceConfig, estimate_bytes(), estimate_rows(), fit_to_budget(), build_model(), DeviceModel, write_model()

### Community 15 - "As-of Calendar Reads"
Cohesion: 0.12
Nodes (8): info(), plot_element(), bar(), dt(), tick(), test_info_lists_incidents(), test_plot_writes_a_png(), test_show_incident_respects_as_of()

### Community 16 - "Run Calendar Planning"
Cohesion: 0.18
Nodes (9): _build_fills(), segment(), build_plan(), interrupt(), place(), _build_runs(), Fill, Plan (+1 more)

### Community 19 - "Store Tests"
Cohesion: 0.18
Nodes (9): _entry(), fresh(), test_a_correction_adds_a_version_and_keeps_the_old_entry(), test_create_refuses_to_overwrite(), test_entry_must_name_a_producer_and_cannot_be_known_before_it_happened(), test_entry_round_trip(), test_incident_labels_are_write_once(), test_opened_record_is_read_only() (+1 more)

### Community 20 - "Repo Split Consolidation"
Cohesion: 0.14
Nodes (12): Component repositories (utils, aggregator, anonymizer, summarizer, sparsifier, orchestrator), Open question: DESIGN.md still describes folders of one repository, example-device repository, 2026-11-19 graph report, graphify knowledge graph of the seven repositories (H6, M6), Open question: add pyproject.toml to component repositories, Branch prototype/synthetic-record, README Quick start fails in zsh (comments as arguments, glob) (H5, Q1) (+4 more)

### Community 22 - "Precedent Replay"
Cohesion: 0.19
Nodes (9): precedents(), ask_time(), at_moment(), compare(), first_ask_time(), _parts(), summary(), _symptoms() (+1 more)

### Community 23 - "Viewer Rendering Helpers"
Cohesion: 0.20
Nodes (18): answerKey(), elLink(), empty(), entryLink(), erDiagram(), esc(), fmt(), fmtFull() (+10 more)

### Community 24 - "Diagnosis Agent Core"
Cohesion: 0.24
Nodes (6): learned_counts(), candidates(), incident_parts(), incident_symptoms(), kinds_of(), signature()

### Community 25 - "Sparsifier Interface"
Cohesion: 0.15
Nodes (4): Series, Sparsifier, StatusRule, Entry

### Community 26 - "Agent Tests"
Cohesion: 0.19
Nodes (12): call(), pair(), run(), test_agent_report_judges_by_later_reviews_only(), test_check_rejects_a_citation_no_tool_returned(), test_demo_command_runs(), test_every_scripted_answer_on_the_planted_cases_passes_the_check(), test_fig2_new_then_known() (+4 more)

### Community 27 - "Static Demo Export"
Cohesion: 0.30
Nodes (5): test_static_demo_holds_the_finished_record_and_every_replay_step(), build_bundle(), put(), export(), key()

### Community 29 - "GUI Session Decisions"
Cohesion: 0.18
Nodes (14): Martin session 2026-11-16: Orchestra prototype and GUI, Demo-only features vs production-like features, Schema additions: service connections, settings, window summaries, Folders named after repositories with import-boundary test, GUI jobs: understand, browse, then replay, GUI remake (five ordered pages, replay as deliberate mode), HCAL-shaped seeded generator with hidden answers, Incident-relevant plots in the Record (+6 more)

### Community 30 - "Model Brain Tests"
Cohesion: 0.18
Nodes (6): _fake_model(), test_model_brain_citations_are_checked(), test_model_brain_speaks_the_tool_calling_protocol(), Brain, diagnose(), Trigger

### Community 31 - "Viewer Navigation and Replay"
Cohesion: 0.24
Nodes (14): drawBar(), drawNav(), exitReplay(), loadRecord(), makeSortable(), openRecordPanel(), render(), setAsOf() (+6 more)

### Community 32 - "Record Slimming Decisions"
Cohesion: 0.21
Nodes (11): Precedent rules: same element vs same symptom, Sparsification: four numbers per 15-minute window, Martin session 2026-11-17: Slimming the Record, parts, and the agent, Agent page judged by precedent reviews, Six read-only agent tools, cmscoord detector geometry dependency, Entry class/source/type tree, Precedent reviews table (+3 more)

### Community 33 - "Prototype Ground Rules"
Cohesion: 0.23
Nodes (10): Two-part prototype: feed skeleton and orchestra code on synthetic Record, example-device README, CMS Operations Orchestra, Proposal Fig. 2 story, Known limits of the synthetic Record, Planted fault situations, Record browser (orchestra view), Seeded synthetic generator (+2 more)

### Community 34 - "LLM Example YAML"
Cohesion: 0.20
Nodes (11): default, backend, options, backend, options, api_key_env, base_url, model (+3 more)

### Community 35 - "Model Brain"
Cohesion: 0.23
Nodes (4): _brain(), Citation, ModelBrain, Proposal

### Community 36 - "Control Readings Synthesis"
Cohesion: 0.20
Nodes (3): status_changes(), StatusRule, write_archive()

### Community 37 - "Import Boundary Test"
Cohesion: 0.33
Nodes (5): _all_imports(), _folder(), _imports(), test_package_only_imports_what_it_may(), test_sql_lives_only_in_the_aggregator()

### Community 39 - "Citation Check and Query Log"
Cohesion: 0.20
Nodes (3): check(), Call, QueryLog

### Community 41 - "Operation Policy Config"
Cohesion: 0.22
Nodes (8): default, product, product_type, exempt, rules, paths, product, product_type

### Community 42 - "Viewer Page Mounting"
Cohesion: 0.39
Nodes (9): api(), mapSvg(), mount(), mountAgent(), mountReplaySections(), mountTimeline(), parseT(), planted() (+1 more)

### Community 43 - "Viewer Charts"
Cohesion: 0.22
Nodes (9): buildChart(), hideTip(), niceTicks(), num(), showTip(), tickLabel(), ticks(), wireChart() (+1 more)

### Community 44 - "Incident Views"
Cohesion: 0.32
Nodes (3): IncidentView, seen(), do_POST()

### Community 45 - "LLM Brain Decisions"
Cohesion: 0.29
Nodes (8): Agent design: typed read-only tools, structured proposal, two brains, Compare LLM brain with scripted brain, LLM profiles kept in repository, keys in ~/.config, Diagnosis agent, Key lookup: environment then ~/.config/orchestra/keys.env, LLM brain, LLM profiles (config/llm.yaml, ORCHESTRA_LLM_CONFIG), Scripted brain

### Community 46 - "Scripted Brain and Confidence"
Cohesion: 0.32
Nodes (5): test_confidence_learns_from_reviews_and_evidence(), ScriptedBrain, score(), Settings, verdict()

### Community 48 - "Record Schema Decisions"
Cohesion: 0.29
Nodes (6): Several elements per root cause (to-do), Record as one SQLite file, SQL confined to one module, Runs, fills and beam modes as calendar tables, Certification tracking: not certified yet by default, store bad ranges, Part references with roles and known-at times, Operations Record

### Community 51 - "Repository Layout"
Cohesion: 0.40
Nodes (5): aggregator repository, aggregator/linker.py direct-link builder (interface only), orchestrator repository, Sibling repository layout via PYTHONPATH, utils repository

### Community 52 - "Viewer Entry Rendering"
Cohesion: 0.40
Nodes (5): clsTag(), describe(), dur(), entryRows(), knowledgeChart()

## Knowledge Gaps
- **61 isolated node(s):** `operations-orchestra-example`, `aggregator repo README`, `Write API (add_entry, supersede, open_incident, label_incident, ...)`, `Replay helpers (incident_frame, became_known, ...)`, `view.py (orchestra info/show/plot)` (+56 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 398 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **26 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `RecordStore` connect `Record Store and Write API` to `Control Archive and Incident Text`, `Viewer API Endpoints`, `Aggregator Record Schema`, `Source Page Resolution`, `LLM Profile Config`, `Device Config and Presets`, `Entry Writes and Corrections`, `As-of Calendar Reads`, `Record Info and Summary`, `Store Tests`, `Precedent Replay`, `Diagnosis Agent Core`, `Aggregator Package and Schema Docs`, `Model Brain Tests`, `Citation Check and Query Log`, `Direct-Link Builder`, `Incident Views`, `Record Schema Decisions`, `Record Text Views`?**
  _High betweenness centrality (0.276) - this node is a cross-community bridge._
- **Are the 8 inferred relationships involving `RecordStore` (e.g. with `build_direct_links()` and `LinkRule`) actually correct?**
  _`RecordStore` has 8 INFERRED edges - model-reasoned connections that need verification._
- **What connects `operations-orchestra-example`, `aggregator repo README`, `Write API (add_entry, supersede, open_incident, label_incident, ...)` to the rest of the system?**
  _61 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Record Store and Write API` be split into smaller, more focused modules?**
  _Cohesion score 0.04689265536723164 - nodes in this community are weakly interconnected._
- **Why does `Operations Record` connect `Aggregator Record Schema` to `Record Store and Write API`?**
  _High betweenness centrality (0.046) - this node is a cross-community bridge._
- **Are the 5 inferred relationships involving `_Gen` (e.g. with `DeviceConfig` and `DeviceModel`) actually correct?**
  _`_Gen` has 5 INFERRED edges - model-reasoned connections that need verification._
- **Should `Control Archive and Incident Text` be split into smaller, more focused modules?**
  _Cohesion score 0.0707070707070707 - nodes in this community are weakly interconnected._