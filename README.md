# dev-log

Session records of the Operations Orchestra: what each person decided while working with an AI
assistant, what the assistant decided, and what is still open. One folder per repository, then
one per member, then one file per session, named `YYYY-MM-DD-topic.md`:

```
dev-log/
├── example-device/
│   ├── martin/2026-11-17-record-and-agent.md
│   └── salvatore/2026-11-19-consolidation.md
├── aggregator/
├── orchestrator/
└── ...           (utils, anonymizer, summarizer, sparsifier)
```

A record goes under the repository the session was run from. A session that changed several
repositories names them all in its `product` field.

Each repository's `.claudoperation/policy.yml` points its records here with
`capture_dir: ../dev-log/<repository>`, so this repository must be checked out beside the
others (see the README of `example-device`). Records are written into this repository and are
committed here, not in the repository the session worked on.

Moved here from `example-device/sessions/` (branch `prototype/synthetic-record`) on 19 November
2026, so that records about any repository of the organization live in one place. Arranged by
repository later the same day; the records made before then were all run from
`example-device`.
