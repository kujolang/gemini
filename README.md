# Kujo Gemini Provider

Native Google Gemini Developer API client with an AI SDK provider adapter.

## Install and first request

```bash
kujo package-add github:kujolang/gemini@v0.1.0
export GEMINI_API_KEY=your-key
```

```kujo
from gemini import create_client, client_generate_content
client := create_client({})
result := client_generate_content(client, "gemini-2.5-flash", [{"role":"user","parts":[{"text":"Hello"}]}], {})
```

Native calls preserve Gemini `contents`, parts, candidates, safety metadata, and usage. `gemini_provider()` exposes the normalized AI SDK driver for chat, streaming, tools, structured output, vision, and embeddings where the selected model supports them.

Live examples require credentials; the default test suite is offline and credential-free.
