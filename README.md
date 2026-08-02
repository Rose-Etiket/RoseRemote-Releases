# RoseRemote — Releases & Linux Agent Install

This repo is the public distribution point for RoseRemote, a self-hosted, peer-to-peer remote desktop tool. It holds:

- **Windows installer downloads** — see [Releases](../../releases).
- **Install instructions for the headless Linux agent** — below.

RoseRemote's source is closed and lives in a private repository. This repo intentionally ships **no source code** — only install docs and a pointer to the pre-built agent container image, published from CI on every change to the agent.

## Linux — headless agent

Runs as an unattended host device: ideal for a server or VM with no screen attached. The account you point it at must already exist on your RoseRemote server and have Admin access (unattended sessions are an Admin-only feature).

### Quick start

```bash
docker run -d --name roseremote-agent \
  -e Server__Url=https://your-server:5140 \
  -e Auth__Email=you@example.com \
  -e Auth__Password=your-password \
  ghcr.io/rose-etiket/roseremote-agent:latest
```

### Or with Docker Compose

```bash
curl -fsSLO https://raw.githubusercontent.com/Rose-Etiket/RoseRemote-Releases/main/docker-compose.yml
# edit the environment values, then:
docker compose up -d
```

### Configuration reference

| Variable | Required | Default | Notes |
|---|---|---|---|
| `Server__Url` | Yes | — | Your RoseRemote server's base URL |
| `Auth__Email` | Yes | — | Must belong to an existing Admin account |
| `Auth__Password` | Yes | — | |
| `Device__Name` | No | container hostname | Shown in the device list |
| `Video__FrameRate` | No | `2` | Frames/sec — low by default, this mode targets headless/scripted use over interactive desktop use |
| `Video__EnableHardwareEncoding` | No | `false` | |
| `Ice__UseIceServers` | No | `false` | Only needed for STUN/TURN relay traversal across restrictive NATs |

## Windows

Grab the latest installer from [Releases](../../releases).

## Support

Issues with the agent or installer: open an issue on this repo. For anything about the product itself, see [remote.roseetiket.nl](https://remote.roseetiket.nl).
