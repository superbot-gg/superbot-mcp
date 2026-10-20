---
name: superbot
description: Run a request through superbot, the user's own AI agent. Applies when the user types /superbot <request> or asks superbot to do something.
---

# superbot

superbot is the user's own AI agent: it takes a request and hands back a finished result. It is reached through one MCP tool named `superbot` (server https://superbot.gg/mcp). That is the only tool; its input fields pick one of three modes.

## The tool

`superbot` takes one request per call. The input fields that are set pick the mode:

- search_tools: `use_case` is a short description of the task. The reply lists matching adapters.
- get_tool_details: `slug` is an adapter from a search_tools reply. The reply is that adapter's inputs.
- omni: `intent` is the request in plain words, with optional `adapter`, `args` and `context` (what the user is trying to solve). `intent` alone is enough: superbot picks the adapter or answers directly.

The request is everything after `/superbot`, or what the user asked superbot to do. An omni reply is the answer to it. A reply with status=processing carries a `request_id`; calling again with that `request_id` returns the finished answer. A reply that ends with a question for the user is a decision card, and the user's pick goes back in the next call.

superbot acts for the user with its own credentials and approvals, under an appointment the user made for this route. Its answers are AI-generated and can make mistakes. When it reports a miss, superbot has picked the request up and an adapter is being synthesized.

## If the superbot tool is not connected

A session with no `superbot` tool has not installed the server yet. The user installs it by giving their coding agent this line:

```
install the superbot MCP server globally: https://superbot.gg/mcp
```

In Claude Code the same install is `claude mcp add --transport http superbot https://superbot.gg/mcp -s user`: superbot asks the user to sign in the first time, in their browser, and the agent needs a restart to see the new server. The link install has no sign-in step: the agent posts to `https://superbot.gg/mcp/install` with `client=claude-code`, runs the `add` command in the reply, and the account owner approves the `link_url` once.
In Codex the same link install has no sign-in step either: the agent posts to `https://superbot.gg/mcp/install` with `client=codex`, and the reply's `config_toml` is a `[mcp_servers.superbot]` entry with its own key. A Codex config with only the endpoint `url` and no key also connects: its first `superbot` call answers with a `link_url` to approve.
No account yet? Follow https://superbot.gg/auth.md: it signs the user in with an emailed code and gives you a token for `https://superbot.gg/mcp`.

<!-- claims: manage-ai-apps -->
