---
name: kugelaudio-api
description: Use when integrating KugelAudio text-to-speech into an application or voice agent.
---

# KugelAudio API

Use this skill to integrate KugelAudio's public text-to-speech API.

## Authentication

The API uses a user-owned API key, not OAuth. Ask the user to create a key in the [KugelAudio dashboard](https://www.kugelaudio.com/en/dashboard) and keep it in the `KUGELAUDIO_API_KEY` environment variable. Never request that a user paste a secret into chat or client-side code.

## API resources

- OpenAPI: https://api.kugelaudio.com/openapi.json
- API reference: https://docs.kugelaudio.com/api-reference/introduction
- Authentication guide: https://docs.kugelaudio.com/api-reference/authentication
- Quick start: https://docs.kugelaudio.com/quickstart

Use `https://api.kugelaudio.com` for HTTP requests and `wss://api.kugelaudio.com` for WebSocket streaming. Start with the OpenAPI document for endpoint schemas and use `kugel-3` for new integrations.
