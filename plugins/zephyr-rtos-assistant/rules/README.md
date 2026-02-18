---
description: "Overview of Cursor rules for Zephyr RTOS project - orchestrator, coderules, zephyr architecture, and project conventions"
---
# Cursor Rules Overview

This directory contains Cursor rules that guide the AI assistant to generate code following project-specific conventions, architectural patterns, and Zephyr RTOS best practices.

## Purpose

These rules ensure consistency across the codebase and help maintain code quality by automatically applying the correct standards based on file type, location, and context.

---

## Available Rules

### Core Orchestrator

#### `agent-workflow-orchestrator.mdc`
**Agent workflow orchestrator** - Always applied. Primary directive file that enforces a mandatory 4-step workflow: (1) analyze context, (2) read applicable rules, (3) apply standards, (4) generate code. Routes AI to context-specific rules based on file paths, language, and component type. Ensures consistency and prevents code generation before proper analysis.

---

### Code Style Rules (`coderules/`)

#### `coderules/c.mdc`
**C coding style** - Zephyr kernel-style standards:
- Static Facade pattern, snake_case naming
- Device Tree integration, thread-safe static allocation
- Zephyr-specific error handling

**Applies to:** All C source files (`.c`, `.h`)

#### `coderules/cpp.mdc`
**C++ coding style** - Modern C++ standards for Zephyr:
- PascalCase classes, camelCase methods, snake_case namespaces
- Static Manager pattern (no Singleton)
- C++17/C++20 without exceptions or RTTI

**Applies to:** All C++ source files (`.cpp`, `.hpp`)

#### `coderules/bash.mdc`
**Bash scripting standards** - Safe and maintainable scripts:
- Unofficial Bash Strict Mode (`set -euo pipefail`)
- Variable naming, error handling, path handling best practices

**Applies to:** All Bash scripts (`*.sh`, `scripts/**`)

---

### Zephyr Architecture Rules (`zephyr/`)

#### `zephyr/drivers.mdc`
**Driver development standards** - Creating hardware interface drivers:
- Standalone Zephyr module structure
- DeviceTree bindings location (`dts/bindings/`)
- CMakeLists.txt and Kconfig integration
- Zephyr driver API patterns

**Applies to:** Files in `drivers/` directory

#### `zephyr/external-modules.mdc`
**Module development standards** - Creating reusable Zephyr modules:
- Module structure with `zephyr/module.yml`
- Cross-project reuse patterns
- Integration via west workspace

**Applies to:** Files in `modules/` directory

#### `zephyr/libs.mdc`
**Library development standards** - Creating in-tree C++ libraries:
- Standalone library structure
- Static Manager pattern (no Singleton)
- CMakeLists.txt integration
- Initialization and lifecycle management

**Applies to:** Files in `lib/` directory

#### `zephyr/kconfig.mdc`
**Kconfig configuration standards** - Configuration file structure:
- `menuconfig` vs `config` selection
- Log level configuration patterns
- Module naming and logging integration

**Applies to:** All `Kconfig` files

---

### Project Rules (`project/`)

#### `project/changelog.mdc`
**Changelog format** - Maintaining `CHANGELOG.md`:
- Keep a Changelog format
- Semantic Versioning standards
- Change categorization (Added, Changed, Deprecated, etc.)

**Applies to:** `CHANGELOG.md` file

### Cursor AI Rules (`cursor-ai/`)

#### `cursor-ai/how-to-create-rules.mdc`
**Meta-rules for creating rules** - Best practices for writing effective Cursor rules:
- Rule structure and organization
- Content guidelines (minimizing examples, prioritizing constraints)
- Context optimization techniques
- Technical requirements

**Reference when:** Creating or modifying any rule file

---

## How Rules Work

1. **Workflow Orchestration**: The `agent-workflow-orchestrator.mdc` (always applied) enforces a 4-step process for every task
2. **Automatic Routing**: Based on Step 1 analysis, the orchestrator identifies which rules to read:
   - File location (`drivers/`, `modules/`, `lib/`)
   - Programming language (C, C++, Bash)
   - File type (source code, Kconfig, changelog)
3. **Combined Application**: Multiple rules apply simultaneously (e.g., `drivers.mdc` + `c.mdc` + `kconfig.mdc` when working on a driver)
4. **Sequential Execution**: Code generation only happens after context analysis, rule reading, and standards application

## Creating New Rules

When creating or modifying rules, follow the guidelines in:
**📖 [`cursor-ai/how-to-create-rules.mdc`](cursor-ai/how-to-create-rules.mdc)**

This ensures rules are optimized for LLM context, memory efficiency, and technical accuracy.
