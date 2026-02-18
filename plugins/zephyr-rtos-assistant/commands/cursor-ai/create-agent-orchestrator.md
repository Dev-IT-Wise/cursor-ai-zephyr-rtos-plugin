---
name: "Create Agent Orchestrator"
description: "Analyze workspace and create customized agent workflow orchestrator with supporting rules. Generates .cursor/rules/ infrastructure for project structure, languages, and patterns."
---
# Create Agent Orchestrator

## Overview
Analyze the current workspace and create a customized agent workflow orchestrator with supporting rule files. This command generates a complete `.cursor/rules/` infrastructure tailored to your project's structure, languages, and patterns.

**Recommended:** Use **Plan mode** for this command. Creating an orchestrator involves many architectural decisions that benefit from discussion before implementation.

## Critical: Ask Before Assuming

**DO NOT assume project conventions.** Ask the user about:

- **Naming conventions**: snake_case vs camelCase vs PascalCase for each language
- **Error handling patterns**: exceptions, error codes, Result types, errno?
- **Documentation style**: Doxygen, JSDoc, rustdoc, docstrings?
- **Directory purposes**: What belongs in each major directory?
- **Code patterns**: Singleton allowed? Static classes? Dependency injection?
- **Build/config preferences**: Which files need rules? Which can be skipped?
- **Strictness level**: How strict should rules be? What's enforced vs recommended?

**When uncertain about ANY convention or pattern, ASK.** Do not invent rules based on assumptions.

## Steps

1. **Gather requirements from user**
   - Ask about project type and domain (embedded, web, CLI, library, etc.)
   - Ask about team size and experience level
   - Ask about existing coding standards or style guides
   - Ask about must-have vs nice-to-have rules
   - Clarify any ambiguous patterns found in codebase
   - **Do not proceed until key conventions are confirmed**

2. **Analyze workspace structure**
   - Scan top-level directories to identify project components
   - Identify programming languages used (by file extensions)
   - Detect build systems (CMake, Make, npm, cargo, etc.)
   - Find configuration file patterns (YAML, JSON, TOML, etc.)
   - Note any existing `.cursor/` configuration
   - **Present findings to user and ask for corrections/additions**

3. **Identify rule categories needed**
   Based on analysis, determine which rule types are required:
   - **Directory-specific rules**: For each major directory with distinct patterns (e.g., `src/`, `lib/`, `drivers/`, `tests/`)
   - **Language-specific rules**: For each programming language found (C, C++, Python, TypeScript, Rust, etc.)
   - **File type rules**: For configuration files, build files, documentation
   - **Project-specific rules**: For unique project patterns (changelog, CI/CD, etc.)
   - **Ask user to confirm or modify the proposed rule categories**

4. **Create orchestrator file**
   Create `.cursor/rules/agent-workflow-orchestrator.mdc` with:
   - `alwaysApply: true` frontmatter
   - 4-step workflow (Analyze → Read Rules → Apply Standards → Generate)
   - Routing table mapping directories/extensions to rule files
   - Universal standards section (language, documentation requirements)
   - Command execution guidelines

5. **Create supporting rule files** (one task per rule file)
   For each identified category, create a rule file:
   - Use appropriate `globs` patterns for auto-activation
   - Include core principles (3-5 items)
   - Add naming conventions table if applicable
   - Define structural guidelines with minimal code skeleton
   - Create Must/Must Not checklist

   **Process each rule file individually:**
   - Analyze existing code in that category for patterns
   - **Ask user to confirm observed patterns before writing rule**
   - Draft rule content based on confirmed patterns
   - Write rule file to `.cursor/rules/[category]/[name].mdc`

6. **Create README.md**
   Generate `.cursor/rules/README.md` documenting:
   - Purpose of the rules system
   - List of all created rules with descriptions
   - How rules work together
   - How to create new rules

7. **Verify orchestrator completeness**
   - Check all identified directories have routing entries
   - Check all languages have corresponding rules
   - Verify no orphan rules (rules without orchestrator reference)
   - Test that globs patterns are correct

## Output Structure

```
.cursor/
├── rules/
│   ├── agent-workflow-orchestrator.mdc  # Main orchestrator (alwaysApply: true)
│   ├── README.md                         # Documentation
│   ├── coderules/                        # Language-specific rules
│   │   ├── [language].mdc
│   │   └── ...
│   ├── [project-type]/                   # Domain-specific rules
│   │   ├── [component].mdc
│   │   └── ...
│   └── project/                          # Project-wide rules
│       ├── changelog.mdc
│       └── ...
└── commands/
    └── cursor-ai/
        └── create-new-rule.md            # Helper command
```

## Orchestrator Template

```markdown
---
description: "Agent workflow orchestrator - enforces 4-step workflow for [PROJECT_NAME]"
alwaysApply: true
---
# Agent Workflow Orchestrator

## Workflow

### Step 1: Analyze Context
- What files will be created/edited?
- What programming language?
- What directory context?

### Step 2: Read Required Rules
[Routing table based on analysis]

### Step 3: Apply Universal Standards
- [Project-specific standards]

### Step 4: Generate Code
Follow rules from Step 2, then standards from Step 3.
```

## Rule File Template

```markdown
---
description: "[Brief description for AI semantic routing]"
globs:
  - "[pattern]/**/*.[ext]"
alwaysApply: false
---
# [Rule Title]

## Core Principles
1. **[Principle]**: [Explanation]

## Naming Conventions
| Element | Convention | Example |
|---------|-----------|---------|

## Structural Guidelines
[Minimal code skeleton]

## Must / Must Not
### MUST:
- ✅ [Requirement]

### MUST NOT:
- ❌ [Anti-pattern]
```

## Analysis Checklist

Before creating orchestrator, verify:

- [ ] All major directories identified
- [ ] All programming languages detected
- [ ] Build system(s) identified
- [ ] Configuration file patterns noted
- [ ] Existing coding patterns observed
- [ ] Project-specific conventions documented

## Created Files Checklist

After creation, verify:

- [ ] `agent-workflow-orchestrator.mdc` exists with `alwaysApply: true`
- [ ] All routing entries point to existing rule files
- [ ] All rule files have correct `globs` patterns
- [ ] README.md documents all rules
- [ ] No circular references between rules

## Notes

- **Use Plan mode** - this command benefits from collaborative planning
- **Ask, don't assume** - every project has unique conventions
- Start with essential rules only - add more as patterns emerge
- Keep orchestrator under 200 lines for fast loading
- Each rule file should be under 500 lines
- Use `@filename` references instead of duplicating content
- Test rules by working on actual project files
