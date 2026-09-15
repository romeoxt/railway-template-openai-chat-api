# Railway Template Composer Setup

## Marketplace listing

- **Title:** Deploy and Host OpenAI Chat API with Railway
- **Short description:** Private OpenAI chat endpoint with streaming — keep your API key on the server.
- **Category:** AI
- **Overview:** paste `README.md`

## Services

| Service | Source | Volume | Public HTTP |
| --- | --- | --- | --- |
| OpenAI Chat API | GitHub repo (this folder) | — | Yes |

## Variables — OpenAI Chat API

| Variable | Value | Secret | Description |
| --- | --- | --- | --- |
| `OPENAI_API_KEY` | (user supplied) | Yes | OpenAI API key |
| `OPENAI_MODEL` | `gpt-4o-mini` | No | Default chat model |
| `API_KEY` | `${{secret(32)}}` | Yes | `X-API-Key` for `/v1/chat` |

## Settings — OpenAI Chat API

- Healthcheck: `/health`
- Mark `OPENAI_API_KEY` as **required** at deploy time
- No database service needed
