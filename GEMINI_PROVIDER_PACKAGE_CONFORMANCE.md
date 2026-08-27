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
| Clean-room distribution | PASS | `scripts/verify_installed_package.sh` passed with Kujo v1.0.2, including add/install/reinstall/validate and installed consumer |
| Remote release | PASS | Remote repository, immutable tag `v0.1.1`, and source commit verified |
