# Entry skills

[Agent Skills](https://agentskills.io) and plugins for [Entry](https://entry.fyi), the personal homepage for busy professionals. They teach an AI agent to work with your Entry through [Entry's MCP server](https://github.com/entry-fyi/mcp) or, on your own machine, the optional [`entry` command line](https://entry.fyi/developers#cli), and to look people and companies up on Entry through its public API.

| Skill | What it teaches |
|---|---|
| [`entry`](skills/entry/SKILL.md) | Working with **your own** Entry through `https://entry.fyi/mcp`, or through the `entry` command line when an agent runs on your machine and MCP is not connected: read your profile and drafts, write and edit drafts, propose profile changes and ask you to publish. The right tool or command for each request, revisions and conflicts, field limits, and the rule that you approve everything public. |
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

This installs the skills only. For `entry`, also connect the MCP server ([steps for every client](https://github.com/entry-fyi/mcp#connect-your-assistant)) or install the command line below.

### The `entry` command line (optional, for agents on your machine)

For a local agent that can run shell commands, or a scheduled job, the `entry` skill can use the [`entry` command line](https://entry.fyi/developers#cli) instead of MCP. The skill uses MCP when it is connected and the command line otherwise.

```bash
npm install -g @entry-fyi/cli
entry login
```

Needs Node 22 or later, and `@entry-fyi/cli` 0.1.0 or later (`entry --version`). Installing it does not sign in, open a browser or contact Entry. `entry login` opens Entry in your browser, where you see what the command line will be able to do and choose which Entries it may reach; `entry logout` revokes it. A scheduled job with no browser uses an access token you make in Entry under Settings → Integrations, set as `ENTRY_API_KEY`. The plugin's skills never install it without asking you.

## What's in this repository

| File | Used by |
|---|---|
| `skills/*/SKILL.md`, `skills/entry/references/cli.md` | Every client that reads [Agent Skills](https://agentskills.io/specification) |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude Code plugins |
| `.cursor-plugin/plugin.json` and the logo in the assets folder | Cursor plugins (its MCP server is `.mcp.json`) |
| `plugin.json`, `mcp.json`, `.agents/plugins/marketplace.json` | [Agent Plugins](https://agent-plugins.org) (Codex) |
| `gemini-extension.json` | Gemini CLI extensions |

## Your data

The skills and plugin manifests in this repository are text: they run no code on your machine. The optional command line, if you install it, is a program that does. Everything talks to Entry services run by Entry:

- **`https://entry.fyi/mcp`** (the `entry` skill and the MCP server). Signing in is OAuth: you choose which Entries an agent may reach and what it may do, and you can disconnect at any time in Entry under Settings → Integrations. The agent reads your profile and drafts, including details you haven't published, and what it creates (drafts, profile proposals, publication requests) is saved in your Entry until you delete it. Entry keeps a record of what a connected assistant did for 13 months. An agent can't publish, unpublish or change your live page.
- **The `entry` command line** (`@entry-fyi/cli`, optional, only if you install it). It is a local program that sends its requests to `https://entry.fyi/api/v1/me`, the same API with the same approval and limits as the MCP server, and to nothing else. Signing in is OAuth in your browser, as above; the login is stored in your operating system's credential store (Keychain, Credential Manager or Secret Service), never in a file, and `entry logout` revokes it. A job can use an access token you make in Settings → Integrations, supplied as `ENTRY_API_KEY`; the command line never prints a credential. It reads and writes what you let it reach, as above, keeps no analytics and sends nothing to anyone else. Entry keeps the same 13-month record of what it did. An agent that has a shell can run it, so it can do anything the login or token allows, and nothing beyond the Entries and scopes you chose.
- **`https://api.entry.fyi/api/v1`** (the `entry-public-profiles` skill). Anonymous, read-only requests for published Entries: the handle, id or search text the agent looks up is sent there. No account or key, and nothing is written.

Entry is for people aged 16 and over. See [entry.fyi/developers](https://entry.fyi/developers), the [privacy policy](https://entry.fyi/privacy) and the [terms](https://entry.fyi/terms).

## Support

[Open an issue](https://github.com/entry-fyi/skills/issues) or email hello@entry.fyi.

MIT licensed.
