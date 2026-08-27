# Gemini Provider Package Contract v1 Conformance

Evidence date: 2026-08-27. Contract: `ai-sdk/docs/KUJO_PROVIDER_PACKAGE_CONTRACT_V1.md` v1.0.1.

| Area | Result | Evidence |
|---|---|---|
| Native and driver layers | PASS | `src/gemini.kujo`, `src/provider.kujo` |
| Safe auth/endpoint handling | PASS | `tests/native_tests.kujo` |
| Deterministic tests | PASS | `scripts/release_quality_gate.sh` |
| Immutable AI SDK dependency | PASS | `kennel.toml` pins `v1.1.0` |
| Streaming | PASS | SSE parser and driver hook tests |
| Tools/structured output/multimodal | N/A | Native request fields preserved; model-dependent behavior not claimed as normalized test capability |
| Clean-room distribution | BLOCKED | `scripts/verify_installed_package.sh` reached install/reinstall/manifest validation, but consumer import failed under local Kujo v1.0.0 because lockfile package-root discovery is unavailable |
| Remote release | PASS (source release only) | Remote repository, commits `c34dd35`/`98479f2`, and immutable tags `v0.1.0`/`v0.1.1` verified; release-ready distribution claim withheld |
