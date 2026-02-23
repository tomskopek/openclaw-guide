# OpenClaw VPS Setup Guide

A minimal guide to get [OpenClaw](https://github.com/openclaw/openclaw) running on a fresh Hetzner VPS in ~10 minutes.

**Live version:** [guide.tom.bingo](https://guide.tom.bingo)

## Steps

1. **Provision a server** — Hetzner CX22 (~$5/month)
2. **Create a user** — dedicated `claw` user with passwordless sudo
3. **Install Homebrew** — package manager
4. **Install OpenClaw** — `brew install openclaw`
5. **Add your API key** — Anthropic recommended
6. **Start the gateway** — `openclaw gateway start --daemon`

Total cost: ~$10/month for your own personal AI assistant.

## Files

- `guide.md` — Plain markdown version
- `index.html` — Web version (deployed at guide.tom.bingo)

## Links

- [OpenClaw Docs](https://docs.openclaw.ai)
- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
- [OpenClaw Discord](https://discord.com/invite/clawd)
