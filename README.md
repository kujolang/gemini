# Kujo Gemini Provider

[![Version](https://img.shields.io/badge/version-0.1.3-black)](https://github.com/kujolang/gemini/releases/tag/v0.1.3)
[![License](https://img.shields.io/badge/license-MIT-lightgrey)](LICENSE)
[![built with Kujo](https://img.shields.io/badge/built%20with-Kujo-white.svg)](https://github.com/kujolang/kujo)

Native Google Gemini Developer API support for Kujo, with normalized AI SDK integration.

## Install

```bash
kujo run /path/to/kennel/kennel.kujo --interpreter -- add github:kujolang/gemini@v0.1.3 --alias gemini
kujo run /path/to/kennel/kennel.kujo --interpreter -- install
export GEMINI_API_KEY=your-key
```

## 30-second quick start

```kujo
from gemini import create_client, client_generate_content
client := create_client({})
result := client_generate_content(client, "gemini-2.5-flash", [{"role":"user","parts":[{"text":"Hello from Kujo!"}]}], {})
print(result["data"]["candidates"][0]["content"]["parts"][0]["text"])
```

## Native API

The native client preserves Gemini contents, parts, candidates, safety metadata, streaming events, tools, structured output, multimodal input, and usage. Use it when you need Gemini-specific request and response fidelity.

## AI SDK integration

`gemini_provider({"model": "gemini-2.5-flash"})` provides normalized chat, streaming, tools, structured output, vision, and embeddings semantics where supported by the selected model. AI SDK core retains transport, retries, redaction, and final normalization responsibilities.

## Authentication and security

Set `GEMINI_API_KEY`. Remote endpoints require HTTPS; embedded URL credentials and credential leakage are rejected. Tests never contain real secrets.

## Testing and documentation

```bash
bash scripts/release_quality_gate.sh
bash scripts/verify_installed_package.sh
```

The default gate is deterministic and offline. See [docs/](docs/) for implementation and Contract v1 evidence.
