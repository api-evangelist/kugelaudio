# KugelAudio

KugelAudio is a Y Combinator-backed, Germany-based voice AI company (KugelAudio GmbH) offering low-latency text-to-speech built, trained, and hosted entirely in the European Union. Its kugel-3 and kugel-2-turbo models produce natural speech in 26+ languages, with voice cloning, per-project pronunciation dictionaries, word-level timestamps, and inline break/spell/prosody tags. EU data sovereignty is the core differentiator — outside the reach of the US CLOUD Act, with a direct EU endpoint plus on-premise and dedicated deployment.

- Website: https://www.kugelaudio.com
- Documentation: https://docs.kugelaudio.com
- API reference: https://docs.kugelaudio.com/api-reference/introduction
- Base URL: `https://api.kugelaudio.com` (direct EU: `https://api.eu.kugelaudio.com`)

Backed by: y-combinator

## APIs

**KugelAudio TTS API** — REST at `/v1/` for generation, voices, cloning, dictionaries, normalization, and transcription, plus three WebSocket streaming channels (`/ws/tts`, `/ws/tts/stream`, `/ws/tts/multi`) tuned for real-time voice agents with token-by-token input, barge-in, and up to 20 concurrent contexts per connection. Bearer API key authentication. Drop-in compatibility surfaces exist for ElevenLabs-compatible SDKs (`/11labs`) and Vapi (`/vapi`), alongside LiveKit and PipeCat integrations.

## Artifacts

| Artifact | Path | Method |
| --- | --- | --- |
| OpenAPI 3.1 (51 operations) | `openapi/kugelaudio-tts-openapi-original.json` | searched |
| Agent Skill (provider-published) | `skills/kugelaudio-api.md` + `skills/_index.yml` | searched |
| llms.txt | `llms/kugelaudio-llms.txt` | searched |
| Well-known + RFC 9727 api-catalog | `well-known/` | searched |
| Packages / SDKs | `packages/kugelaudio-packages.yml` | searched |
| Error catalog | `errors/kugelaudio-error-codes.yml` | searched |
| Authentication | `authentication/kugelaudio-authentication.yml` | searched |
| Conventions | `conventions/kugelaudio-conventions.yml` | searched |
| Lifecycle | `lifecycle/kugelaudio-lifecycle.yml` | searched |
| Streaming AsyncAPI 3.0 | `asyncapi/kugelaudio-tts-asyncapi.yml` | generated |
| OpenAPI Overlay | `overlays/kugelaudio-tts-overlay.yaml` | generated |
| Data model | `data-model/kugelaudio-data-model.yml` | derived |
| Conformance | `conformance/kugelaudio-conformance.yml` | derived |
| MCP tool candidates | `mcp/kugelaudio-mcp.yml` | derived (candidate) |
| Domain security | `security/kugelaudio-domain-security.yml` | probed |

## Notes for the provider

Findings worth raising with KugelAudio, all verified 2026-07-19:

1. **The docs site serves the wrong OpenAPI.** `https://docs.kugelaudio.com/api-reference/openapi.json` — the spec the docs navigation and `llms.txt` both point at — is the untouched Mintlify **"OpenAPI Plant Store"** sample, not KugelAudio's API. The real spec lives at `https://api.kugelaudio.com/openapi.json` and is only discoverable through the `/.well-known/api-catalog` linkset. Any agent or codegen tool following the documented path gets a plant store.
2. **The real spec omits `servers[]` and `securitySchemes`.** Every endpoint requires an API key, but the published document declares no security at all and no server URL, so generated clients have neither a host nor auth. `overlays/kugelaudio-tts-overlay.yaml` supplies both.
3. **Most operations are untagged** and `operationId`s are raw FastAPI-generated names (`get_voice_by_id_v1_voices__voice_id__get`), which makes for poor SDK and MCP tool ergonomics.
4. **Only 422 errors are modeled in the spec**, while the docs publish a rich 21-row error table with stable `error_code` values and WebSocket close codes. None of it reaches the machine-readable contract.
5. **The three WebSocket channels are absent from the spec entirely** — the lowest-latency path, and the reason most customers pick the product, has no machine-readable description. `asyncapi/kugelaudio-tts-asyncapi.yml` is our reconstruction from the docs.
6. **Spec-vs-docs drift on word timestamps**: the spec's `WordTimestamp` uses `start_s`/`end_s`/`confidence`; the streaming docs show `start_ms`/`end_ms`/`char_start`/`char_end`/`score`.
7. **No `security.txt`, no vulnerability-disclosure page, and no trust center.** DNS posture is otherwise strong (DNSSEC enabled, SPF, DMARC `p=reject`, TLS 1.3, HSTS with a two-year max-age) — though `api.kugelaudio.com` serves no HSTS header and no CAA records are set on the domain.
8. **No idempotency contract.** Writes such as voice creation and reference upload are not safely retryable.
9. **No dated changelog** and no published SLA, despite a clearly written 6-month/12-month deprecation policy.
10. **The Java SDK is documented but unpublished** — no Maven Central artifact exists for it. The npm/PyPI packages also point their repository metadata at `github.com/Kugelaudio/KugelAudio`, which is not public.

On the positive side, KugelAudio is one of very few providers in the network shipping an **RFC 9727 `api-catalog`** and a **provider-published Agent Skill** with a verifiable SHA-256 digest — both genuinely ahead of the field.
