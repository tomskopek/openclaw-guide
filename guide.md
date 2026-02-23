# How to Set Up OpenClaw on a VPS

A minimal guide to get OpenClaw running on a fresh server in ~10 minutes.

---

## 1. Provision a Server

Go to [Hetzner Cloud](https://console.hetzner.cloud/) and create a server:

- **OS**: Ubuntu 24.04
- **Type**: CX22 (2 vCPU, 4GB RAM) — plenty to start
- **Location**: Pick the closest region
- **SSH Key**: Add your public key during setup

Once it's live, grab the IP address from the dashboard.

```bash
ssh root@YOUR_SERVER_IP
```

## 2. Create a User

Don't run OpenClaw as root. Create a dedicated user:

```bash
adduser claw
usermod -aG sudo claw
```

Give it passwordless sudo (so OpenClaw can install packages when needed):

```bash
echo "claw ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/claw
chmod 440 /etc/sudoers.d/claw
```

Switch to the new user:

```bash
su - claw
```

## 3. Install Homebrew

OpenClaw installs via Homebrew:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the post-install instructions to add brew to your PATH:

```bash
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.bashrc
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
```

## 4. Install OpenClaw

```bash
brew install openclaw
```

Run the setup wizard:

```bash
openclaw onboard
```

This walks you through:
- Choosing a model provider (Anthropic recommended)
- Entering your API key
- Connecting a chat channel (Telegram, Slack, etc.)

## 5. Add Your Anthropic Key

If you don't have one yet, get an API key at [console.anthropic.com](https://console.anthropic.com/).

The onboard wizard will ask for it. Or configure it later:

```bash
openclaw configure --section auth
```

## 6. Start the Gateway

```bash
openclaw gateway start
```

That's it. OpenClaw is running. If you connected Telegram or Slack during onboard, send it a message — it'll respond.

## 7. Keep It Running (Optional)

To keep OpenClaw running after you disconnect:

```bash
openclaw gateway start --daemon
```

Check status anytime:

```bash
openclaw status
```

---

## Quick Reference

| Command | What it does |
|---|---|
| `openclaw onboard` | First-time setup wizard |
| `openclaw gateway start` | Start the gateway |
| `openclaw gateway start --daemon` | Start in background |
| `openclaw gateway stop` | Stop the gateway |
| `openclaw status` | Check status |
| `openclaw configure --section auth` | Update API keys |
| `openclaw configure --section channels` | Add/edit chat channels |

---

## Total Cost

- **Hetzner CX22**: ~€4.35/month (~$4.75)
- **Anthropic API**: Pay-per-use (Claude Sonnet ~$3/M input tokens)
- **Domain** (optional): ~$10/year

You can run a personal AI assistant for under $10/month.
