# V2Ray Config Manager Pro

A bilingual (English / فارسی), browser-based manager for importing, parsing, deduplicating, filtering, converting and exporting V2Ray/Xray configurations.

## Open the application

### [Launch V2Ray Config Manager Pro](https://v2ray-config-manager-fullstack.vercel.app/)

The link above is the hosted application.

## Features

- English and Persian interface with RTL support
- Import VLESS, VMess, Trojan, Shadowsocks, SSR, Hysteria, Hysteria2 and TUIC links
- Import Clash YAML, sing-box JSON and Xray/V2Ray JSON
- Parse plain-text and Base64 subscription content
- Detect duplicate configurations
- Search, filter, tag, compare and organize nodes
- Convert and export supported formats
- Local browser storage for offline use
- Optional full-stack API, authentication, SQLite storage and scheduled health checks

## Quick use

1. Open the [live application](https://v2ray-config-manager-fullstack.vercel.app/).
2. Paste configuration links, subscription content or supported JSON/YAML into the import area.
3. Review the parse report before saving.
4. Filter, tag or compare imported nodes.
5. Export only the configurations you intend to use.

## Run the offline frontend locally

After downloading the project files, serve them with any static HTTP server:

```bash
python3 -m http.server 8080
```

Open `http://localhost:8080`. A local HTTP server is more reliable than opening `index.html` directly because browsers restrict some `file://` features.

## Offline mode

The static frontend can parse, organize and export configurations in the browser. Data is stored locally in the current browser profile. Clearing site data or switching browsers removes that local data, so export a backup first.

Features that require a running backend are unavailable in static mode, including server accounts, shared databases, server-side subscription fetching, scheduled jobs, Telegram automation and real Xray/sing-box connectivity tests.

## Full-stack architecture

```text
Browser UI -> Node.js REST API -> SQLite
                    |
                    +-> Xray-core / sing-box health tests
                    +-> scheduled GitHub Actions worker
                    +-> optional Telegram bot
```

The backend requires Node.js 22.5 or newer because it uses built-in `node:sqlite`. GitHub Pages cannot run this backend; use the live deployment or a separate Node-compatible host for server features.

## Security notes

- Never commit real UUIDs, passwords, API keys, worker tokens or subscription credentials.
- Treat exported configurations as secrets.
- Use a strong, unique administrator password for a server deployment.
- Keep `AUTH_SECRET`, `WORKER_TOKEN` and Telegram tokens in hosting secrets.
- A syntactically valid proxy configuration is not proof that the endpoint is safe or operational.

## Review and testing status

The supplied project test suite contains 118 checks. During review, 111 passed and four underlying checks failed (the report shows seven failures because parent suites also fail). The browser compatibility suite passed. The remaining failures concerned test-fixture process launching, due-subscription test setup and worker-auth status handling; no exposed production credentials were found.

Do not present the full-stack backend as production-ready until every CI check passes.

## License

No open-source license was included in the supplied archive. All rights remain with the copyright holder until a license is added explicitly.
