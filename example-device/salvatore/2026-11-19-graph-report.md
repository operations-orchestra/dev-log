# Graph Report - operations-orchestra  (2026-11-19)

## Corpus Check
- 67 files · ~68,749 words
- Verdict: corpus is large enough that graph structure adds value.
- Unclassified: 21 file(s) not represented in the graph (top: (none) 17, .lock 1, .toml 1)
- WARNING: 21 of 89 files seen (24%) have no supported extractor and are missing from this graph entirely. It may look complete while representing only part of the codebase.

## Summary
- 1031 nodes · 2155 edges · 67 communities (41 shown, 26 thin omitted)
- Extraction: 90% EXTRACTED · 10% INFERRED · 0% AMBIGUOUS · INFERRED: 208 edges (avg confidence: 0.88)
- Token cost: 69,811 input · 0 output

## Community Hubs (Navigation)
- Agent Tests
- CLI and Control Archive
- Anonymizer Interface
- Viewer API Endpoints
- Viewer App Constants
- Record Write and Replay API
- Source Page Resolution
- Synthetic Event Generator
- LLM Profile Config
- GUI Plan and Pages
- Record Info and Summary
- Generation Entry Point
- Viewer Tests
- Feed Skeleton Docstrings
- Data-Quality Archive
- Part References and Certification
- Precedent Confidence
- Prototype Ground Rules
- Device Config and Presets
- Run Calendar Planning
- Store Tests
- DQM Archive Adapter
- Viewer Link Helpers
- Aggregator Store Core
- Sparsifier Interface
- Precedent Matching
- Agent and Precedent Decisions
- Viewer Navigation and Replay
- Entry Writes and Corrections
- Import Boundary Rule
- GUI Session Decisions
- LLM Example YAML
- Record Schema and Calendar
- Dev-Log and Repo Split
- Operation Policy Config
- Viewer Page Mounting
- Viewer Charts
- Record Core Concepts
- Design Hand-off Overview
- Device Model
- As-of Store Tests
- Repositories and Feed Status
- Planted Fault Scenarios
- Direct-Link Builder
- As-of Reads and Query Tools
- Diagnosis Agent Concepts
- cmscoord Detector Plan
- Viewer Entry Rendering
- LLM Profile Decisions
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
1. `RecordStore` - 132 edges
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
- `RecordStore` --implements--> `Operations Record`  [INFERRED]
  aggregator/aggregator/store.py → example-device/README.md
- `Record as one SQLite file, SQL confined to one module` --references--> `RecordStore`  [INFERRED]
  dev-log/martin/2026-11-16-orchestra-prototype-gui.md → aggregator/aggregator/store.py
- `graphify knowledge graph of seven repositories` --references--> `RecordStore`  [EXTRACTED]
  dev-log/salvatore/2026-11-19-consolidation.md → aggregator/aggregator/store.py
- `Sibling repos found via PYTHONPATH (pyproject, pixi.toml)` --semantically_similar_to--> `Sibling repository layout via PYTHONPATH`  [INFERRED] [semantically similar]
  dev-log/salvatore/2026-11-19-consolidation.md → example-device/README.md
- `RecordStore` --implements--> `Operations Record`  [EXTRACTED]
  aggregator/aggregator/store.py → example-device/docs/DESIGN.md

## Import Cycles
- 2-file cycle: `example-device/example_device/__init__.py -> example-device/example_device/generator.py -> example-device/example_device/__init__.py`

## Hyperedges (group relationships)
- **Agent diagnosis flow: tools, confidence, citation check** — example_device_docs_design_diagnosis_agent, example_device_docs_design_query_tools, example_device_docs_design_confidence_model, example_device_docs_design_citation_check, example_device_docs_design_precedent_table [EXTRACTED 1.00]
- **Record time-integrity properties** — example_device_docs_design_as_of_reads, example_device_docs_design_append_only, example_device_docs_design_state_lookback, aggregator_aggregator_readme_three_incident_labels [INFERRED 0.85]
- **Detector model migration to cmscoord** — example_device_docs_detector_plan_detector_interface, example_device_docs_detector_plan_toy_detector_model, example_device_docs_detector_plan_cmscoord_adapter, example_device_docs_detector_plan_lv_overlay, aggregator_aggregator_readme_part_ref [EXTRACTED 1.00]
- **GUI remake: ordered pages (detector, how built, what is in it, scenarios, replay)** — example_device_docs_gui_plan_gui_remake, example_device_docs_gui_plan_detector_map_page, example_device_docs_gui_plan_how_the_record_is_built_page, example_device_docs_gui_plan_tables_page, example_device_docs_gui_plan_scenarios_page, example_device_docs_gui_plan_replay_mode [EXTRACTED 1.00]
- **Operations Orchestra component repos** — aggregator_readme_aggregator, anonymizer_readme_anonymizer, orchestrator_readme_orchestrator, sparsifier_readme_sparsifier, summarizer_readme_summarizer, utils_readme_utils [INFERRED 0.85]
- **Evolution of Record content design (sparsification to status-change readings and part references)** — dev_log_martin_2026_11_16_orchestra_prototype_gui_sparsification, dev_log_martin_2026_11_17_record_and_agent_status_change_readings, dev_log_martin_2026_11_16_orchestra_prototype_gui_multi_element_cause, dev_log_martin_2026_11_17_record_and_agent_part_references, dev_log_martin_2026_11_17_record_and_agent_calendar_tables [INFERRED 0.85]
- **Precedent matching: rules, confidence, expert reviews, agent page** — dev_log_martin_2026_11_16_orchestra_prototype_gui_precedent_rules, dev_log_martin_2026_11_17_record_and_agent_precedent_confidence, dev_log_martin_2026_11_17_record_and_agent_precedent_reviews, dev_log_martin_2026_11_17_record_and_agent_agent_page [INFERRED 0.85]
- **Mechanics of splitting example-device into sibling repositories** — dev_log_salvatore_2026_11_19_consolidation_repo_split, dev_log_salvatore_2026_11_19_consolidation_package_folder_layout, dev_log_salvatore_2026_11_19_consolidation_pythonpath, dev_log_salvatore_2026_11_19_consolidation_importlib_source_links, dev_log_salvatore_2026_11_19_consolidation_boundary_test_per_package, dev_log_salvatore_2026_11_19_consolidation_llm_config_cwd [EXTRACTED 1.00]

## Communities (67 total, 26 thin omitted)

### Community 0 - "Agent Tests"
Cohesion: 0.05
Nodes (32): call(), _fake_model(), pair(), run(), test_agent_report_judges_by_later_reviews_only(), test_check_rejects_a_citation_no_tool_returned(), test_confidence_learns_from_reviews_and_evidence(), test_demo_command_runs() (+24 more)

### Community 1 - "CLI and Control Archive"
Cohesion: 0.08
Nodes (22): ControlArchive, _as_of(), _ask(), _brain(), _demo(), _export_static(), _info(), main() (+14 more)

### Community 2 - "Anonymizer Interface"
Cohesion: 0.05
Nodes (12): Anonymized, Anonymizer, RoleDirectory, CertificationAdapter, DataQualityAdapter, DowntimeAdapter, ElogAdapter, RawRecord (+4 more)

### Community 3 - "Viewer API Endpoints"
Cohesion: 0.09
Nodes (31): agent(), ApiError, _archive_summary(), _as_of(), built(), demo_device(), demo_planted(), detector_map() (+23 more)

### Community 4 - "Viewer App Constants"
Cohesion: 0.06
Nodes (33): ALIAS, CLASS_NAME, CMP, DROP, DV, ER_POS, HINT, KIND_LABEL (+25 more)

### Community 5 - "Record Write and Replay API"
Cohesion: 0.06
Nodes (4): Replay helpers (incident_frame, became_known, ...), Write API (add_entry, supersede, open_incident, label_incident, ...), RecordStore, meta()

### Community 6 - "Source Page Resolution"
Cohesion: 0.09
Nodes (13): _describe_module(), package_dir(), source_path(), Current, find_records(), make_handler(), do_GET(), do_POST() (+5 more)

### Community 8 - "LLM Profile Config"
Cohesion: 0.11
Nodes (10): test_git_holds_only_an_example_without_keys(), test_profiles_keep_keys_out_of_the_file_and_out_of_sight(), profiles(), config_path(), ConfigError, get_profile(), keys_path(), load_profiles() (+2 more)

### Community 9 - "GUI Plan and Pages"
Cohesion: 0.06
Nodes (26): Agent panel in Replay and Agent page, Build-a-Record control (not built, open decision), Device page (detector map, calendar, fault catalogue), GUI Plan (understand and check what has been built), Hand-written SVG charts (buildChart, knowledgeChart) instead of uPlot, How the Record is built page, Interfaces of unbuilt parts page, LLM content marks and 'Who writes what' page (removed in remake) (+18 more)

### Community 10 - "Record Info and Summary"
Cohesion: 0.10
Nodes (11): describe(), info(), marks_detector(), plot_element(), bar(), dt(), tick(), show_incident() (+3 more)

### Community 11 - "Generation Entry Point"
Cohesion: 0.12
Nodes (13): preset(), generate(), end(), store(), tiny(), test_budget_above_hard_cap_is_refused(), test_budget_too_small_is_refused(), test_different_seed_gives_different_record() (+5 more)

### Community 12 - "Viewer Tests"
Cohesion: 0.13
Nodes (19): call(), _known_times(), test_built_page_examples_are_real_rows(), test_demo_endpoint_lists_each_planted_case_with_its_entries(), test_detector_map_shows_state_at_the_time_control(), test_diff_lists_what_was_learned_in_between(), test_incident_and_entry_pages_hide_what_is_not_yet_known(), test_interfaces_page_is_read_from_the_skeletons() (+11 more)

### Community 14 - "Data-Quality Archive"
Cohesion: 0.13
Nodes (8): status_of(), write_archive(), write_archive(), test_static_demo_holds_the_finished_record_and_every_replay_step(), build_bundle(), put(), export(), key()

### Community 16 - "Precedent Confidence"
Cohesion: 0.18
Nodes (9): StoredEntry, learned_counts(), candidates(), incident_parts(), incident_symptoms(), kinds_of(), signature(), symptom_kind() (+1 more)

### Community 18 - "Prototype Ground Rules"
Cohesion: 0.14
Nodes (19): Demo-only features vs production-like features, HCAL-shaped seeded generator with hidden answers, Record as one SQLite file, SQL confined to one module, Two-part prototype: feed skeleton and orchestra code on synthetic Record, Runs, fills and beam modes as calendar tables, Certification tracking: not certified yet by default, store bad ranges, Quick start fails when pasted into zsh, example-device README (+11 more)

### Community 19 - "Device Config and Presets"
Cohesion: 0.18
Nodes (6): DeviceConfig, estimate_bytes(), estimate_rows(), fit_to_budget(), SizeBudgetError, build_model()

### Community 20 - "Run Calendar Planning"
Cohesion: 0.18
Nodes (9): _build_fills(), segment(), build_plan(), interrupt(), place(), _build_runs(), Fill, Plan (+1 more)

### Community 21 - "Store Tests"
Cohesion: 0.18
Nodes (9): _entry(), fresh(), test_a_correction_adds_a_version_and_keeps_the_old_entry(), test_create_refuses_to_overwrite(), test_entry_must_name_a_producer_and_cannot_be_known_before_it_happened(), test_entry_round_trip(), test_incident_labels_are_write_once(), test_opened_record_is_read_only() (+1 more)

### Community 23 - "Viewer Link Helpers"
Cohesion: 0.20
Nodes (18): answerKey(), elLink(), empty(), entryLink(), erDiagram(), esc(), fmt(), fmtFull() (+10 more)

### Community 24 - "Aggregator Store Core"
Cohesion: 0.13
Nodes (5): IncidentView, LinkView, PartRef, seen(), do_POST()

### Community 25 - "Sparsifier Interface"
Cohesion: 0.15
Nodes (4): Series, Sparsifier, StatusRule, Entry

### Community 26 - "Precedent Matching"
Cohesion: 0.22
Nodes (8): precedents(), ask_time(), at_moment(), compare(), first_ask_time(), _parts(), summary(), _symptoms()

### Community 27 - "Agent and Precedent Decisions"
Cohesion: 0.20
Nodes (13): Agent design: typed read-only tools, structured proposal, two brains, Precedent rules: same element vs same symptom, Martin session 2026-11-17: Slimming the Record, parts, and the agent, Agent page judged by precedent reviews, Six read-only agent tools, Compare LLM brain with scripted brain, cmscoord detector geometry dependency, Entry class/source/type tree (+5 more)

### Community 28 - "Viewer Navigation and Replay"
Cohesion: 0.24
Nodes (14): drawBar(), drawNav(), exitReplay(), loadRecord(), makeSortable(), openRecordPanel(), render(), setAsOf() (+6 more)

### Community 30 - "Import Boundary Rule"
Cohesion: 0.26
Nodes (7): Folders named after repositories with import-boundary test, Boundary test checks each package where it lives, _all_imports(), _folder(), _imports(), test_package_only_imports_what_it_may(), test_sql_lives_only_in_the_aggregator()

### Community 31 - "GUI Session Decisions"
Cohesion: 0.21
Nodes (10): Martin session 2026-11-16: Orchestra prototype and GUI, Schema additions: service connections, settings, window summaries, GUI jobs: understand, browse, then replay, GUI remake (five ordered pages, replay as deliberate mode), Incident-relevant plots in the Record, Several elements per root cause (to-do), Replay withholds later-linked evidence, Part references with roles and known-at times (+2 more)

### Community 32 - "LLM Example YAML"
Cohesion: 0.20
Nodes (11): default, backend, options, backend, options, api_key_env, base_url, model (+3 more)

### Community 33 - "Record Schema and Calendar"
Cohesion: 0.22
Nodes (8): aggregator (owner of the Operations Record), aggregator README, Calendar tables (fill, run, beam_mode) and certification, part_ref table (parts with roles and times), view.py (orchestra info/show/plot), Several elements per entry (part_ref), Plan: realistic detector model by integrating cmscoord, Detector integration stages A-E

### Community 34 - "Dev-Log and Repo Split"
Cohesion: 0.31
Nodes (8): dev-log README, Dev-log session records (one file per session per member), Salvatore session 2026-11-19: Splitting into organization repositories, graphify knowledge graph of seven repositories, Viewer source links via importlib (package_dir, source_path), Sibling repos found via PYTHONPATH (pyproject, pixi.toml), Move components into own repositories, New summarizer repository

### Community 35 - "Operation Policy Config"
Cohesion: 0.22
Nodes (8): default, product, product_type, exempt, rules, paths, product, product_type

### Community 36 - "Viewer Page Mounting"
Cohesion: 0.39
Nodes (9): api(), mapSvg(), mount(), mountAgent(), mountReplaySections(), mountTimeline(), parseT(), planted() (+1 more)

### Community 37 - "Viewer Charts"
Cohesion: 0.22
Nodes (9): buildChart(), hideTip(), niceTicks(), num(), showTip(), tickLabel(), ticks(), wireChart() (+1 more)

### Community 38 - "Record Core Concepts"
Cohesion: 0.25
Nodes (3): Incident (recovery action, confirmed cause, certification labels), Operations Orchestra, Operations Record

### Community 39 - "Design Hand-off Overview"
Cohesion: 0.25
Nodes (5): Operations Orchestra Prototype Design and Hand-off, Feed Interfaces (adapters, anonymizer, summarizer, sparsifier), orchestra CLI commands (synth, info, show, plot, view, ask, demo), SourceAdapter contract (adapters/base.py), Viewer GUI (Record browser)

### Community 43 - "Repositories and Feed Status"
Cohesion: 0.29
Nodes (7): Sparsification: four numbers per 15-minute window, aggregator repository, Feed components: anonymizer, summarizer, sparsifier (interfaces only), aggregator/linker.py direct-link builder (interface only), orchestrator repository, Sibling repository layout via PYTHONPATH, utils repository

### Community 44 - "Planted Fault Scenarios"
Cohesion: 0.29
Nodes (7): Planted Case (planted.json), Planted Fault Modes (configure_failure, fed_comm_loss, lv_drift_trip, hot_channels, box_sync_loss, planned_change), What counts as a precedent (open question 2), Synthetic HCAL-like Example Device Generator, cmscoord adapter implementation, detector/ package interface (at, layers, part, units, translate, layout), Toy Detector Model (example_device/model.py)

### Community 46 - "As-of Reads and Query Tools"
Cohesion: 0.33
Nodes (4): query_log table, As-of Read API (entries, state_at, incidents, ...), Orchestrator Query Tools (state, events, co_occurring, search_incidents, get_incident, series), Time-to-run lookup (lumisection clock)

### Community 47 - "Diagnosis Agent Concepts"
Cohesion: 0.33
Nodes (4): Diagnosis Agent (structured proposal: known/new/uncertain), Model Brain (OpenAI-compatible tool calling), precedent table (precedent reviews), Scripted Brain

### Community 48 - "cmscoord Detector Plan"
Cohesion: 0.40
Nodes (3): cmscoord, cmscoord layers (logical, frontend, backend, trigger, physical), cmscoord tables (units, components, membership)

### Community 49 - "Viewer Entry Rendering"
Cohesion: 0.40
Nodes (5): clsTag(), describe(), dur(), entryRows(), knowledgeChart()

### Community 50 - "LLM Profile Decisions"
Cohesion: 0.67
Nodes (4): LLM profiles kept in repository, keys in ~/.config, llm_config looks for profiles under working directory, Key lookup: environment then ~/.config/orchestra/keys.env, LLM profiles (config/llm.yaml, ORCHESTRA_LLM_CONFIG)

## Knowledge Gaps
- **48 isolated node(s):** `operations-orchestra-example`, `aggregator repo README`, `Write API (add_entry, supersede, open_incident, label_incident, ...)`, `Replay helpers (incident_frame, became_known, ...)`, `view.py (orchestra info/show/plot)` (+43 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 376 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **26 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `RecordStore` connect `Record Write and Replay API` to `Agent Tests`, `Viewer API Endpoints`, `LLM Profile Config`, `Record Info and Summary`, `Generation Entry Point`, `Feed Skeleton Docstrings`, `Part References and Certification`, `Precedent Confidence`, `As-of Calendar Reads`, `Prototype Ground Rules`, `Store Tests`, `Aggregator Store Core`, `Precedent Matching`, `Entry Writes and Corrections`, `Record Schema and Calendar`, `Dev-Log and Repo Split`, `Record Core Concepts`, `Device Model`, `Entry Reads and Lumisections`, `Direct-Link Builder`, `As-of Reads and Query Tools`?**
  _High betweenness centrality (0.335) - this node is a cross-community bridge._
- **Are the 9 inferred relationships involving `RecordStore` (e.g. with `build_direct_links()` and `LinkRule`) actually correct?**
  _`RecordStore` has 9 INFERRED edges - model-reasoned connections that need verification._
- **What connects `operations-orchestra-example`, `aggregator repo README`, `Write API (add_entry, supersede, open_incident, label_incident, ...)` to the rest of the system?**
  _48 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Agent Tests` be split into smaller, more focused modules?**
  _Cohesion score 0.05092592592592592 - nodes in this community are weakly interconnected._
- **Why does `_Gen` connect `Synthetic Event Generator` to `Device Model`, `Generation Entry Point`, `Device Config and Presets`, `Run Calendar Planning`?**
  _High betweenness centrality (0.055) - this node is a cross-community bridge._
- **Are the 5 inferred relationships involving `_Gen` (e.g. with `DeviceConfig` and `DeviceModel`) actually correct?**
  _`_Gen` has 5 INFERRED edges - model-reasoned connections that need verification._
- **Should `CLI and Control Archive` be split into smaller, more focused modules?**
  _Cohesion score 0.0784313725490196 - nodes in this community are weakly interconnected._