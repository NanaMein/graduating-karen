# OpenCode on Windows

This repository is mainly for learning and mentoring.

OpenCode is optional. You only need it if you want a more interactive assistant to help explain things, look up current information, and guide you step by step.

## What OpenCode is

OpenCode is a terminal-based AI coding assistant. In this repository, it is meant to act like a patient instructor rather than a tool that edits files for you.

This repo includes a special agent called **Kaaego** — short for **Karen’s Alter Ego**.

## What you need first

- A Windows computer
- Internet access
- A terminal app such as PowerShell or Windows Terminal
- A code editor such as VS Code
- If you want OpenCode to answer questions, you will also need to connect an AI provider when OpenCode asks you to

## Easiest Windows path: Bun first

If you want the simplest path on Windows, start with **Bun**.

This is the easiest place to begin for this guide, but note that OpenCode’s official docs still say Windows Bun support is **in progress**. If Bun works on your machine, it is a very light setup. If it gives you trouble, use npm or WSL instead.

Use Bun when:

- you do **not** already have npm available
- you want to avoid installing Node.js just to run OpenCode
- you want a clean, modern setup for this repository

### Install Bun on Windows

Open PowerShell and run:

```powershell
powershell -c "irm bun.sh/install.ps1|iex"
```

After installing Bun, restart your terminal and confirm it works:

```powershell
bun --version
```

### Install OpenCode with Bun

Once Bun is installed, install OpenCode with:

```powershell
bun install -g opencode-ai
```

Then open this repository folder in a terminal and run:

```powershell
opencode
```

## If npm already exists, you can use it

If your computer already has npm because Node.js is already installed, you can use the npm route instead. In other words: if npm is already there, just use it; if not, Bun is a simpler choice than installing Node only for OpenCode.

```powershell
npm install -g opencode-ai
```

Then run:

```powershell
opencode
```

## Recommended for best compatibility: WSL

OpenCode’s official docs recommend **WSL** (Windows Subsystem for Linux) for the best experience on Windows.

If you already use WSL, or if you want the most Linux-like environment, WSL is still a very good choice.

### Basic WSL flow

1. Install WSL using Microsoft’s official instructions.
2. Open your WSL terminal.
3. Install OpenCode inside WSL:

   ```bash
   curl -fsSL https://opencode.ai/install | bash
   ```

4. Go to this repository folder.
5. Run OpenCode from inside the project:

   ```bash
   opencode
   ```

## How to use this repository with OpenCode

1. Clone this repository or download it as a ZIP.
2. Open the folder in a terminal.
3. Start OpenCode from inside the repository.
4. OpenCode will read the project config in `opencode.json`.
5. It will also load the agent file in `.opencode/agents/kaaego.md`.

Because of that setup:

- **Kaaego** becomes the default agent
- Kaaego can **search the web silently** when it needs outside information
- Kaaego **cannot edit the repository**

## Why this exists

This repo is meant to be easy to read even without an account or special tools.

OpenCode is here only for times when someone wants deeper help, more context, or a guided learning experience.

## Good to know

- If you change any OpenCode config or agent files, restart OpenCode so it can load the new settings.
- If OpenCode asks you to connect a provider, follow the prompts inside OpenCode.
