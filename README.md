# Deploy and Host OpenAI Chat API with Railway

Private OpenAI chat endpoint with streaming — keep your API key on the server, not in client apps.

## About OpenAI Chat API

A small FastAPI wrapper around the OpenAI Chat Completions API. Clients call your Railway URL instead of OpenAI directly. Supports JSON responses and Server-Sent Events streaming via the same `/v1/chat` endpoint.

## About Hosting OpenAI Chat API

Railway deploys the service with health checks and HTTPS. Your `OPENAI_API_KEY` stays in Railway variables — frontend and mobile apps only need your service URL and optional `X-API-Key`.

## Environment Variables

| Variable | Description | Secret | Example/Notes |
| --- | --- | --- | --- |
| `OPENAI_API_KEY` | Your OpenAI API key | Yes | User-supplied at deploy time |
| `OPENAI_MODEL` | Default chat model | No | `gpt-4o-mini` |
| `API_KEY` | Protects `/v1/chat` | Yes | `${{secret(32)}}` — send as `X-API-Key` |

## Deploy and Host

1. Deploy this repo from GitHub on Railway.
2. Set `OPENAI_API_KEY`, `OPENAI_MODEL`, and `API_KEY`.
3. Enable **public HTTP** and deploy.
4. Confirm `/health` returns OK.
5. Call the chat endpoint:

```bash
curl -X POST https://YOUR-URL/v1/chat \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_KEY" \
  -d "{\"messages\":[{\"role\":\"user\",\"content\":\"Say hello.\"}]}"
```

Add `"stream": true` to the JSON body for SSE streaming.

No database required.

## Common Use Cases

- Mobile and web apps that must not embed OpenAI keys
- Internal chat widgets and support bots
- Prototypes adding LLM features behind your own API
- Streaming chat UIs using Server-Sent Events

## Dependencies for OpenAI Chat API Hosting

The Railway template includes:

- **OpenAI Chat API** — this GitHub repo (FastAPI + Uvicorn)

## Deployment Dependencies

- [OpenAI API documentation](https://platform.openai.com/docs/api-reference/chat)
- [FastAPI documentation](https://fastapi.tiangolo.com/)

## Why Deploy OpenAI Chat API on Railway?

One service, no database to manage, automatic HTTPS, and a health-checked deploy — the fastest path from OpenAI key to a production-shaped proxy.

## Template Content

| Service | Source |
| --- | --- |
| OpenAI Chat API | GitHub repo (this template) |

## Run locally

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
uvicorn app.main:app --reload --port 8000
```

## Author

romeoxt — herbylegall9@gmail.com

## License

MIT
