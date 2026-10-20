# superbot for coding agents

superbot is your own AI agent: one model that makes pictures, video, songs, 3D and apps, browses the web and uses your computer, on desktop and phone. Try it now in your browser, free and with no account: https://superbot.gg/chat?utm_source=github&utm_medium=registry

It also works with the coding agents this repository connects. This repository holds the public descriptors that connect a coding agent to superbot: a Claude Code plugin and marketplace, a Codex plugin, a Gemini CLI extension, an MCP server entry and one skill. Every one of them points at the same remote MCP server and the same single tool, `superbot`.

Get the desktop and phone apps at https://superbot.gg/download

## Install

Pick the path that matches your agent. They all end at the same server.

### The remote MCP server

The server is `https://api.superbot.gg/mcp` (streamable HTTP). The first call asks you to sign in, in your browser.

```sh
claude mcp add --transport http superbot https://api.superbot.gg/mcp -s user
codex mcp add superbot --url https://api.superbot.gg/mcp
gemini mcp add --transport http -s user superbot https://api.superbot.gg/mcp
```

Restart the agent so it sees the new server.

### The link installer

An agent CLI can skip the browser sign-in. Post to the installer, run the `add` command in the reply, and the account owner approves the `link_url` once:

```sh
curl -sS -X POST "https://api.superbot.gg/mcp/install?client=claude-code"
```

Use `client=codex` for Codex. Its reply carries a `config_toml` entry instead.

### The skill

```sh
npx skills add https://superbot.gg
```

The skill is the file in `skills/superbot/SKILL.md`. It is also served at https://superbot.gg/skills/superbot/SKILL.md and listed in the index at https://superbot.gg/.well-known/agent-skills/index.json.

### As a plugin

Claude Code, from inside a session:

```
/plugin marketplace add superbot-gg/superbot-mcp
/plugin install superbot@superbot
```

Codex:

```sh
codex plugin marketplace add superbot-gg/superbot-mcp
codex plugin add superbot@superbot
```

Gemini CLI:

```sh
gemini extensions install https://github.com/superbot-gg/superbot-mcp
```

## What the tool does

There is one MCP tool, named `superbot`. You give it a request in plain words and it hands back a finished result. The input fields that are set pick one of three modes: `search_tools` lists the adapters that match a task, `get_tool_details` returns the inputs of one adapter, and `omni` runs the request.

People ask it to:

- search the web for current information
- read a web page or a link you paste
- build a spreadsheet, document, deck or PDF from a spec
- generate an image from a text prompt
- find an MCP server or command-line tool for a job superbot lacks, and install it on your computer after you approve (that needs the desktop app paired)

superbot acts for you with its own credentials and approvals. Its answers are AI-generated and can make mistakes.

## What is in this repository

- `.mcp.json`: the MCP server entry, used by Claude Code and by Codex.
- `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`: the Claude Code plugin and a one-plugin marketplace.
- `.codex-plugin/plugin.json`: the Codex plugin.
- `gemini-extension.json`: the Gemini CLI extension.
- `glama.json`: the Glama listing file.
- `skills/superbot/SKILL.md`: the skill.
- `SECURITY.md` and `LICENSE`.

## Security

To report a vulnerability, see [SECURITY.md](SECURITY.md).

## License

MIT, see [LICENSE](LICENSE). Copyright 2026 EZO Labs Inc.

<!-- claims: manage-ai-apps, web-search, read-pages, documents, images, media, find-install-tools -->
