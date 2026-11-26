# Gemini repository hardening

Reviewed public main `329942f`, the immutable `v0.1.3` package,
the native Developer API client, the SDK package driver, and both offline
execution paths.

- Native requests share HTTPS, API-key, timeout, redirect and model-resource
  validation. Native streaming uses Gemini's SSE endpoint, parses arbitrarily
  fragmented LF/CRLF data and preserves all candidates with their metadata.
  The client preserves typed errors and redacts the configured key.
  [GenerateContent and streaming](https://aistudio.google.com/api-reference/generate-content).
- The SDK driver maps system instructions, media parts, tool declarations,
  function responses, opaque thought signatures, and JSON schemas. The
  normalized stream selects the primary candidate, keeps native metadata,
  resolves finish and safety status, and preserves terminal token accounting.
  [Function calling](https://aistudio.google.com/docs/function-calling).
- Single and batch embedding hooks validate input shape and numeric vectors.
  A trusted SDK package declaration permits the fixed SSE selector under
  same-origin and no-redirect rules.
  [Gemini embeddings](https://aistudio.google.com/api-reference/embeddings).
- The example uses the documented replacement for the deprecated model.
  [Gemini deprecation schedule](https://aistudio.google.com/docs/deprecations).

Five existing checks passed at baseline and all six additions failed there.
All 11 tests passed using checksum-verified Kujo releases 1.6.0 and 1.10.0 and
the pinned SDK revision shown in `kennel.toml`. A clean archive exercised
public streaming and embedding descriptor exports with byte-identical
1.10.0 VM and interpreter output. Kennel installed and reinstalled the
immutable `v0.1.3` package and passed its installed export smoke.

Five alternating 3,000-event runs on Intel macOS with released Kujo 1.6.0
produced the same ordered event hash. Median parser time moved from
1,442.993 to 90.297 ms. Verification used injected transport responses
and official API documentation.
