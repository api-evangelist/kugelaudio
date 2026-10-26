# KugelAudio

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
