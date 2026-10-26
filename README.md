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

Bottles are built and tested on ARM macOS and x86_64 Linux. Intel macOS keeps
tap-syntax checks only: upstream Homebrew currently provides no compatible
Rust, OpenSSL 3, or Python 3.12 bottles for that runner. No Intel bottle build
is claimed. The platform-independent PyPI package remains available.

## Release maintenance

After publishing an upstream release to PyPI, dispatch the updater:

```sh
gh workflow run update-formula.yml --repo swisspra/homebrew-tap
```

The updater exempts only the newly verified main package from Homebrew's release
cooldown. Its dependencies retain the normal cooldown.

Native resources rely on the formula's declared `pkgconf`/Rust build tools and
OpenSSL 3/Python 3.12 dependencies. CFFI uses system libffi on macOS and Homebrew
libffi on Linux; retain the build, runtime, and linkage checks when updating
resources.

Documentation/workflow-only PRs run tap-syntax checks without requiring bottles.
Added or modified Ruby formulas still require successful bottle builds and
artifacts on each bottle target; missing artifacts remain a hard failure.

After reviewing the generated PR and all `brew test-bot` platform checks pass,
publish its bottles and formula using the exact reviewed head commit:

```sh
gh workflow run publish.yml --repo swisspra/homebrew-tap \
  -f pull_request=PR_NUMBER -f head_sha=REVIEWED_HEAD_SHA
```
