# Elephant Benchmarks

Public benchmark history for Elephant.

This repository is meant to host:

- static benchmark data under `locomo/`
- a lightweight GitHub Pages front page
- optional GitHub Releases for larger debug trace bundles

## Layout

```text
.
├── .github/workflows/pages.yml
├── index.html
└── locomo/
    ├── index.json
    └── runs/
        └── <run-id>/
            ├── summary.json
            ├── questions.jsonl.gz
            └── debug.jsonl.gz   # optional, often better as a release asset
```

## Publishing Flow

1. Export a publish bundle from the Elephant repo:

```bash
cargo run --release --bin locomo-bench -- \
  publish \
  bench/locomo/results/canonical/full.json \
  --out bench/locomo/published \
  --run-id 2026-03-10-series1
```

2. Sync `bench/locomo/published/` into `locomo/` in this repo.

3. Commit and push.

4. GitHub Pages serves `index.html`, which reads `locomo/index.json`.

## Notes

- Keep `debug.jsonl.gz` out of the default Pages payload unless you explicitly want it there.
- Prefer immutable run directories under `locomo/runs/`.
- Treat `locomo/index.json` as the stable machine-readable entrypoint.
