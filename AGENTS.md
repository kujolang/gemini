# Agent guidance

Public root exports live in `gemini.kujo`. Native protocol code is in `src/gemini.kujo`; the AI SDK driver is in `src/provider.kujo`. Fixtures and deterministic tests are under `tests/`. Run `bash scripts/release_quality_gate.sh` before any release. Do not add provider branches to AI SDK core, mutable dependencies, secrets, or network-dependent default tests. Keep Gemini parts, candidates, safety ratings, finish reasons, and usage native data intact.
