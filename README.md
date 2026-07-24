# swisspra/homebrew-tap

Homebrew tap for [On Board](https://github.com/swisspra/On_Board) — a local-first
MCP server for multi-agent project coordination.

## Install

```sh
brew install swisspra/tap/onboard-memory
```

or:

```sh
brew tap swisspra/tap
brew install onboard-memory
```

> On Homebrew 6+, the first install of a non-official tap asks you to trust it —
> approve the prompt or run `brew trust swisspra/tap`.

This installs two commands (same entry point):

- `onboard-memory-mcp` — the name used in MCP client configs
- `onboard-memory` — short alias

Point your MCP client at the installed binary, e.g.:

```json
{
  "command": "onboard-memory-mcp",
  "env": { "AGENT_PROJECT_DIR": "/path/to/your/project" }
}
```

## Upgrade

```sh
brew update && brew upgrade onboard-memory
```

The formula tracks the latest [`onboard-memory-mcp`](https://pypi.org/project/onboard-memory-mcp/)
release on PyPI; a scheduled workflow opens a bump PR automatically when a new
version ships.
