---
name: "Create Cursor AI Rule"
description: "Interactive workflow for creating well-structured Cursor AI rules following how-to-create-rules.mdc standards. Guides through frontmatter, structure, and Zephyr-specific requirements."
---
# Create Cursor AI Rule

## Overview
Interactive workflow for creating well-structured Cursor AI rules. This command guides you through the process step-by-step, following standards defined in `rules/cursor-ai/how-to-create-rules.mdc`.

**Before starting:** Read `rules/cursor-ai/how-to-create-rules.mdc` for complete guidelines, templates, and best practices.

**Content focus:** Rules should contain the most important information in a dense, concise form. If you want to omit less important corner cases to keep the rule focused, **ask the user first** whether they can be omitted — do not skip information without permission.

## Prerequisites

Before creating a rule, read these sections in `rules/cursor-ai/how-to-create-rules.mdc`:
- Section 1: Rule Types and When to Use Them
- Section 2: Mandatory Structure
- Section 4: Content Guidelines
- Section 5: Rule Templates

## Steps

1. **Define rule purpose and scope**
   - Ask yourself:
     - What problem does this rule solve?
     - When should it be applied?
     - What files or contexts does it affect?
   - Choose appropriate rule type from `@how-to-create-rules.mdc` Section 1:
     - Always Apply (global standards)
     - Apply Intelligently (context-specific, most common)
     - Apply to Specific Files (directory/file patterns)
     - Apply Manually (templates)
   - Determine file name (kebab-case) and location in `.cursor/rules/`

2. **Create file and frontmatter**
   - Create new `.mdc` file in `.cursor/rules/` (or subdirectory)
   - Use template from `@how-to-create-rules.mdc` Section 5.1 or 5.2
   - Write frontmatter:
     - `description`: Clear, concise summary for AI semantic routing
     - `globs`: Array of file patterns (for file-specific rules only)
     - `alwaysApply`: `true` only for global rules, otherwise `false`
   - Verify frontmatter follows Section 2.1 requirements

3. **Write core principles**
   - Define 3-5 high-level requirements
   - Focus on constraints and patterns
   - Use **negative constraints** (what is forbidden)
   - Keep language clear and imperative
   - Reference Section 4.3 for constraint guidelines

4. **Add naming conventions** (if applicable)
   - Create table with: Element | Convention | Example
   - Cover all relevant naming patterns
   - Be specific and consistent

5. **Define structural guidelines**
   - Show minimal code skeleton (structure only, not full implementation)
   - Reference files with `@filename` instead of copying content
   - Keep examples under 20 lines
   - Follow Section 4.2 guidelines (minimize code examples)

6. **Create Must/Must Not checklist**
   - List explicit requirements (✅ MUST)
   - List explicit anti-patterns (❌ MUST NOT)
   - Be specific and actionable
   - Cover all critical constraints

7. **Apply Zephyr-specific requirements** (for this project)
   - Verify rule enforces thread safety (if applicable)
   - Ensure static allocation is prioritized
   - Use Zephyr APIs (not standard library)
   - Define error handling pattern (`-errno`)
   - State English-only requirement
   - If the rule creates source/config/build files: reference `rules/project/license-header.mdc`
   - Reference Section 3 in `@how-to-create-rules.mdc`

8. **Verify against quality checklist**
   - Use checklist from `@how-to-create-rules.mdc` Section 8
   - Ensure rule is under 500 lines
   - Verify all required sections are present
   - Check that examples are structural only
   - Confirm file references use `@filename` syntax

9. **Test the rule**
   - Save file in `.cursor/rules/`
   - For manual rules: Test with `@rule-name` in chat
   - For file-specific rules: Open matching file and verify rule applies
   - For intelligent rules: Verify description triggers correctly
   - Refine based on results

10. **Commit to version control**
    - Commit rule to git for team sharing
    - Write clear commit message explaining rule purpose
    - Document when rule should be updated

11. **Final review (only when something is clearly wrong)**
    - After work is done, skim the rule for:
      - **Repetitions**: Same requirement or example stated in multiple places — merge or reference once.
      - **Obvious optimization**: Redundant bullets, overlapping checklist items, or unnecessarily long wording that can be shortened without losing meaning.
    - **Do not force changes**: Only fix what is evidently wrong. If nothing stands out, leave the rule as is.

## Quick Reference

For detailed information, see `rules/cursor-ai/how-to-create-rules.mdc`:

- **Section 1**: Rule types and when to use them
- **Section 2**: Mandatory structure requirements
- **Section 3**: Zephyr project-specific requirements
- **Section 4**: Content guidelines and best practices
- **Section 5**: Complete templates (.mdc and .md)
- **Section 6**: DO/DON'T best practices
- **Section 7**: Three complete rule examples
- **Section 8**: Quality checklist
- **Section 9**: Integration and precedence
- **Section 10**: Workflow integration

## Rule Creation Checklist

Use this checklist during creation (full checklist in `@how-to-create-rules.mdc` Section 8):

### Structure:
- [ ] File name is descriptive and kebab-case
- [ ] File saved in `.cursor/rules/` (or subdirectory)
- [ ] Frontmatter includes `description` and appropriate `globs`
- [ ] Rule type is appropriate (Always/Intelligent/File-Specific/Manual)
- [ ] Core principles are clear (3-5 items)
- [ ] Naming conventions table included (if applicable)
- [ ] Structural guidelines with minimal skeleton
- [ ] Must/Must Not checklist is complete

### Content Quality:
- [ ] Rule is dense — core constraints prioritized (ask user before omitting any information)
- [ ] Rule is under 500 lines
- [ ] Uses file references (`@filename`) instead of copying code
- [ ] Focuses on constraints and patterns, not full examples
- [ ] Code examples are structural only (not full implementations)
- [ ] Negative constraints are explicit (what is forbidden)

### Zephyr-Specific (for this project):
- [ ] Rule enforces thread safety where applicable
- [ ] Rule prioritizes static allocation over dynamic
- [ ] Rule uses Zephyr APIs (not standard library)
- [ ] Error handling pattern is defined (`-errno`)
- [ ] English-only requirement stated

### Testing:
- [ ] Rule tested in appropriate context
- [ ] Rule produces expected results
- [ ] Rule committed to git for team sharing

### Final review (only fix if clearly wrong):
- [ ] No obvious repetitions (same requirement in multiple places)
- [ ] No redundant or overlapping items; wording not unnecessarily long

## Notes

- This command provides an interactive workflow
- All detailed guidelines, templates, and examples are in `rules/cursor-ai/how-to-create-rules.mdc`
- The rule file is automatically applied when editing rules in `.cursor/rules/`
- Rules are auto-discovered by Cursor via globs - no manual registration needed
