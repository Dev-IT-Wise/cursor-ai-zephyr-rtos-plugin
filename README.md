# Zephyr RTOS Assistant — Cursor Plugin

**by [Devitwise](https://devitwise.com)**

> **Experimental** — this plugin is in active development. We welcome collaboration and contributions — issues, PRs, and feedback are encouraged!

Your AI assistant for Zephyr RTOS. Cursor plugin with rules, commands, and best practices for embedded — less doc hunting, more coding.

## Contents

### Rules

- **Agent Workflow Orchestrator** — AI workflow orchestration (analyze → read rules → generate)
- **Coderules** — C, C++, Bash standards (Zephyr kernel style, Static Facade/Manager)
- **Zephyr** — drivers, modules, libs, Kconfig, DeviceTree, CMake, shell
- **Project** — changelog, license headers

### Commands

- **Zephyr RTOS**: `create-snippet` — create build snippets (YAML + overlay + .conf)
- **Build**: `build-application` — build/flash via project scripts
- **Setup**: `setup-new-feature`, `fix-permissions`
- **Cursor AI**: `create-new-rule`, `create-new-command`, `create-agent-orchestrator`

## Installation

1. Use this repo as a template or clone it
2. In Cursor, install from marketplace (when available) or copy `plugins/zephyr-rtos-assistant/` contents to your project's `.cursor/`

## Validation

```bash
node scripts/validate-template.mjs
```

## Structure

```
.cursor-plugin/
  marketplace.json      # marketplace manifest
plugins/
  zephyr-rtos-assistant/
    .cursor-plugin/
      plugin.json       # plugin manifest
    rules/              # Cursor rules
    commands/           # commands
    assets/             # logo
scripts/
  validate-template.mjs # validator
```

## Resources

- [Cursor Plugin Template](https://github.com/cursor/plugin-template)
- [Zephyr RTOS Documentation](https://docs.zephyrproject.org/)
- [Cursor Documentation](https://docs.cursor.com/)

## License

MIT
