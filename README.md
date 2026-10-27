# Entry skills

[Agent Skills](https://agentskills.io) and plugins for [Entry](https://entry.fyi), the personal homepage for busy professionals. They teach an AI agent to work with your Entry through [Entry's MCP server](https://github.com/entry-fyi/mcp), and to look people and companies up on Entry through its public API.

| Skill | What it teaches |
|---|---|
| [`entry`](skills/entry/SKILL.md) | Working with **your own** Entry through `https://entry.fyi/mcp`: read your profile and drafts, write and edit drafts, propose profile changes and ask you to publish. The right tool for each request, revisions and conflicts, field limits, and the rule that you approve everything public. |
| [`entry-public-profiles`](skills/entry-public-profiles/SKILL.md) | Looking up **published** Entries through the public, read-only API (no account or key): search, profiles, work, projects, writing and links. |

## Install

### Claude Code (plugin: skills + MCP server)

```
/plugin marketplace add entry-fyi/skills
/plugin install entry@entry
```

Then run `/mcp` and sign in to Entry in your browser.

### Codex

```bash
codex plugin marketplace add entry-fyi/skills
```

### Cursor

Add Entry from the [Cursor Marketplace](https://cursor.com/marketplace), or [add just the server](https://cursor.com/en/install-mcp?name=entry&config=eyJ1cmwiOiJodHRwczovL2VudHJ5LmZ5aS9tY3AifQ%3D%3D).

### Gemini CLI

```bash
gemini extensions install https://github.com/entry-fyi/skills
```

Then run `/mcp auth entry` and sign in.

### Any agent that reads Agent Skills

```bash
npx skills add entry-fyi/skills
```

This installs the skills only. For `entry`, also connect the MCP server: [steps for every client](https://github.com/entry-fyi/mcp#connect-your-assistant).

## What's in this repository

| File | Used by |
|---|---|
| `skills/*/SKILL.md` | Every client that reads [Agent Skills](https://agentskills.io/specification) |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude Code plugins |
| `.cursor-plugin/plugin.json` and the logo in the assets folder | Cursor plugins (its MCP server is `.mcp.json`) |
| `plugin.json`, `mcp.json`, `.agents/plugins/marketplace.json` | [Agent Plugins](https://agent-plugins.org) (Codex) |
| `gemini-extension.json` | Gemini CLI extensions |

## Your data

Signing in is OAuth: you choose which Entries an agent may reach and what it may do, and you can disconnect at any time in Entry under Settings → Integrations. An agent can't publish, unpublish or change your live page. See [entry.fyi/developers](https://entry.fyi/developers) and the [privacy policy](https://entry.fyi/privacy).

## Support

[Open an issue](https://github.com/entry-fyi/skills/issues) or email hello@entry.fyi.

MIT licensed.
