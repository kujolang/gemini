# Gemini Implementation Report

## Executive Summary

Initial Kujo Gemini package using the current Gemini Developer API `generateContent` surface and a pure AI SDK driver.

## Official API Evidence

Google's official `google-genai` SDK documents `genai.Client(api_key=...)`, `client.models.generate_content`, content parts, streaming, files, tools, and API-version selection. The official REST reference documents `GenerateContentResponse` candidates, `finishReason`, safety ratings, and usage metadata.

## Evidence Date

2026-08-27.

## Protocol Classification

NATIVE DISTINCT PROTOCOL. Gemini uses `contents`/`parts`, candidate responses, and Gemini SSE rather than OpenAI chat wire shapes.

## Architecture

Native client in `src/gemini.kujo`; AI SDK adapter in `src/provider.kujo`; root exports in `gemini.kujo`.

## Native API Coverage

Client configuration, `generateContent`, `streamGenerateContent` SSE parsing, `countTokens`, `embedContent`, and model listing. Native parts, tools, generation config, safety settings, candidates, finish reason, and usage are preserved.

## Public Exports

`create_client`, `generate_content`, `stream_generate_content`, client operations, `list_models`, `count_tokens`, `embed_content`, `parse_stream`, `gemini_provider`, `gemini_driver`.

## Kujo Requirement

Kujo >= 1.0.2.

## AI SDK Dependency

`github:kujolang/ai-sdk@v1.1.0`.

## Authentication

`GEMINI_API_KEY` with `GOOGLE_API_KEY` fallback, sent as `x-goog-api-key`; remote HTTPS and credential-bearing URLs are rejected.

## Native Semantics

Gemini contents and parts remain structured. Candidate and safety metadata remain in `raw_provider`.

## Streaming

Gemini SSE `data:` frames are parsed with additive event tolerance and malformed-frame containment.

## Tools / Structured Output / Reasoning / Multimodal / Embeddings

Native request configuration preserves provider fields. Embedding endpoint is exposed. Model-dependent behavior is not fabricated in normalized metadata.

## Usage / Finish Reasons / Errors

`usageMetadata` maps prompt and candidate token counts; `STOP` maps to `stop`, `MAX_TOKENS` to `length`; native error payloads are retained subject to redaction.

## AI SDK Driver

Pure descriptor/decoder hooks; no network I/O, transport selection, retry, budget, or endpoint-policy bypass.

## Security

Secret redaction, HTTPS enforcement, URL credential rejection, protected API-key header, malformed response and stream containment are tested.

## Tests

`bash scripts/release_quality_gate.sh` runs two offline deterministic test files.

## Clean-Room Install / Installed Consumer Smoke

Passed with the official Kujo v1.0.2 macOS x64 release binary: Kennel add/install/reinstall/validate and the installed consumer smoke passed with `KUJO_MODULE_PATH` unset.

## Live Validation

SKIPPED — credentials/environment unavailable.

## AI SDK Changes

None.

## Kujo Changes

None.

## Kennel Changes

None.

## Contract Conformance

See `GEMINI_PROVIDER_PACKAGE_CONFORMANCE.md`.

## Limitations

Initial package does not claim native file lifecycle, batch, cache, or Vertex/Enterprise auth surfaces.
