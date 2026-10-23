<div align="center">

# GameNodeX

**Self-hosted control panel for game server hosting.**
Run nodes, sell game servers under your own brand, plug in any billing.

[![Website](https://img.shields.io/badge/website-gamenodex.com-2563eb)](https://gamenodex.com/?utm_source=github&utm_medium=readme)
[![Free plan](https://img.shields.io/badge/free%20plan-1%20node%20·%203%20servers-16a34a)](https://gamenodex.com/signup?utm_source=github&utm_medium=readme)
[![Docs](https://img.shields.io/badge/docs-read-6b7280)](https://gamenodex.com/docs?utm_source=github&utm_medium=readme)

[Website](https://gamenodex.com/?utm_source=github&utm_medium=readme) ·
[Get started free](https://gamenodex.com/signup?utm_source=github&utm_medium=readme) ·
[Documentation](https://gamenodex.com/docs?utm_source=github&utm_medium=readme) ·
[Русская версия](README.ru.md)

</div>

<p align="center"><img src="docs/screenshot.png" alt="GameNodeX dashboard" width="900"></p>

---

## Why GameNodeX

Building your own hosting panel takes months. Renting a seat in someone else's SaaS means their brand, their limits and your customers' data on their servers. GameNodeX is the third option: **a complete panel you install on your own hardware.**

- 🏠 **Self-hosted** — your database, your nodes, your domain, your customers. Not SaaS, not a reseller account.
- 🎨 **Your brand only** — name, logo, colors, favicon, login page and support links are settings. Customers never see our name.
- 🔌 **Any billing** — documented REST API (OpenAPI), signed webhooks, and a ready WHMCS module.
- 🧩 **Mods in one click** — Modrinth, Steam Workshop, Thunderstore, uMod and GameBanana, with dependencies and clean uninstall.
- 🔒 **Secure by design** — mTLS between the panel and every node, per-server containers and SFTP chroots, 2FA, full audit log.
- 🔓 **No lock-in** — plain Docker containers, PostgreSQL and S3. Your data stays in open formats.

## What's the "master"?

GameNodeX has two parts:

```
          Your infrastructure                              Our side
┌────────────────────────────────────────────┐
│  Master panel  (one Linux server + Docker)  │ ── license renewal only ──▶ License server
│  admin UI · customer panel · REST API · DB  │
└──────────────┬──────────────┬───────────────┘
          mTLS │         mTLS │
        ┌──────▼─────┐  ┌─────▼──────┐
        │  Node  +   │  │  Node  +   │   … any datacenter, any country
        │  agent     │  │  agent     │
        └────────────┘  └────────────┘
```

**The master** is the brain of your hosting. It's the panel itself — installed once on any Linux server with Docker:

- **Admin panel** for your team: nodes, game catalog, plans, customers, backups, monitoring, settings.
- **Customer panel** under your brand: customers start/stop their servers, use the live console, files, SFTP, mods, backups and schedules.
- **REST API + webhooks** for your billing or CRM.
- **Scheduler** that places new servers on suitable nodes by location, free resources and port/IP pools.
- **Certificate authority** for your nodes: connect a node with a one-time token, the master issues and renews its certificate automatically.
- **Game catalog** with versions: change a game's settings once and they roll out to every node by themselves.

**Nodes** are your Linux machines with Docker and a lightweight agent. Every game server is a container with its own CPU, memory and disk limits. Nodes talk only to your master — never to us.

## Features

| | |
|---|---|
| **Nodes** | One-token onboarding, automatic mTLS certificates, locations, port and IP pools, drain for maintenance, live CPU/RAM/disk load |
| **Game servers** | Create, start, stop, reinstall; live console, logs, stats, file manager with editor, SFTP, scheduled tasks |
| **Game catalog** | Any game with a Docker image; versioned settings, automatic rollout, **starter set** of ready games in one click |
| **Mods & maps** | Modrinth, Steam Workshop, Thunderstore, uMod, GameBanana; dependencies, compatibility checks, clean uninstall, customer uploads with quotas |
| **Backups** | Straight from the node to your S3-compatible storage; several storages per location/node; rotation and quotas per plan; database dumps |
| **Databases** | MySQL / MariaDB / PostgreSQL for game servers |
| **Monitoring** | CPU, memory, disk and player history per node and server; offline alerts; Prometheus metrics |
| **Users & access** | Roles and fine-grained staff permissions, server co-owners, 2FA, audit log |
| **Billing** | Plans with resource limits, suspension for non-payment, REST API, HMAC-signed webhooks with retries, WHMCS module |
| **Branding** | Name, logo, colors, favicon, login page, light and dark themes — no rebuild |

## Supported games

Any game that runs from a Docker image can be added to the catalog. For these, mods, maps and plugins are already set up:

> Minecraft Java (Paper · Fabric · Forge) · Minecraft Bedrock · Counter-Strike 2 (CounterStrikeSharp · Workshop) · Counter-Strike 1.6 (AMX Mod X · GameBanana) · Counter-Strike: Source (SourceMod) · Rust (Oxide / uMod) · Garry's Mod · Valheim · V Rising · Risk of Rain 2 (BepInEx · Thunderstore) · Project Zomboid · Arma 3 · DayZ · Unturned · Space Engineers (Steam Workshop) · Terraria (tModLoader · TShock) · Factorio · SA-MP

## From bare metal to the first customer

1. **Deploy the master** on your server with one command and activate your license key.
2. **Connect nodes** — create a token in the panel and run the agent on each node. Certificates are issued automatically.
3. **Launch servers** — tick games from the starter set, define plans with limits; the panel places servers on suitable nodes.
4. **Run your business** — your billing creates and suspends servers through the API, customers manage theirs in your panel.

Step-by-step guide: **[gamenodex.com/docs](https://gamenodex.com/docs?utm_source=github&utm_medium=readme)**

## Pricing

Every plan has every feature. You pay for scale: installations, nodes and game servers.

| Plan | Price | Nodes | Game servers |
|---|---|---|---|
| **Free** | $0 forever | 1 | 3 |
| **Starter** | $29 / mo | 3 | 50 |
| **Pro** | $79 / mo | 10 | 300 |
| **Business** | $199 / mo | 30 | 1000 |
| **Enterprise** | on request | unlimited | unlimited |

Yearly billing — 2 months free. No credit card needed for the free plan. Current prices: **[gamenodex.com](https://gamenodex.com/?utm_source=github&utm_medium=readme#pricing)**

## FAQ

**Is it SaaS?** No. Every customer runs their own installation. The panel contacts our server only to renew the license; no telemetry is collected. Enterprise has an offline license for air-gapped networks.

**What do I need?** One Linux server with Docker for the master and Linux machines with Docker for nodes. Optionally S3-compatible storage for backups (MinIO works).

**Can I connect my billing?** Yes — through the REST API and webhooks, or use the WHMCS module.

**Is the source code here?** This repository is the project's public page. The panel is distributed as ready-to-run builds from [gamenodex.com](https://gamenodex.com/?utm_source=github&utm_medium=readme).

## Contact

- 🌐 Website: [gamenodex.com](https://gamenodex.com/?utm_source=github&utm_medium=readme)
- ✉️ Sales and support: [support@gamenodex.com](mailto:support@gamenodex.com)
- 🐞 Questions and feature requests: [Issues](../../issues)

<div align="center">

**[Start for free →](https://gamenodex.com/signup?utm_source=github&utm_medium=readme)**

If GameNodeX looks useful, give the repo a ⭐ — it helps other hosters find it.

</div>
# Master
# app
# app
