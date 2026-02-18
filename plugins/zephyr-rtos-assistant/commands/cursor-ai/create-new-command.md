---
name: "Create Cursor AI Command"
description: "Create a well-structured, reusable Cursor AI command following documentation standards. Builds commands triggerable with / prefix in chat."
---
# Create Cursor AI Command

## Overview
Create a well-structured, reusable Cursor AI command following official documentation standards. This command helps you build effective commands that can be triggered with `/` prefix in chat.

## Command Structure Requirements

### 1. File naming
- Use descriptive kebab-case names (e.g., `review-code.md`, `write-tests.md`)
- Save in `.cursor/commands/` directory
- Use `.md` extension

### 2. Required sections
Every command MUST include:
- **Overview**: Clear, concise description of what the command does
- **Steps** (if multi-step): Numbered list of actions to perform
- **Checklist** (optional): Actionable items with `- [ ]` format

### 3. Content guidelines
- Write in plain Markdown
- Be specific and actionable
- Include context and motivation
- Use clear, imperative language
- Add examples where helpful
- Keep focused on one workflow

### 4. Workflow patterns for reliable execution

When creating commands with multi-step data processing workflows:

**Per-item processing:**
- If processing multiple items (registers, files, entries), specify "one task per item" in steps
- AI will create one todo entry per item, not per batch
- This ensures progress tracking and error localization

**Incremental writes:**
- Specify "validate then write after each" or "append to output after each"
- AI will update output file after processing each item
- Partial results survive interruptions
- One wrong item doesn't invalidate all output

**Source validation:**
- Specify "re-check the source for [item] when validating"
- AI will re-read source data before appending each item
- Reduces transcription errors

**Why this matters:**
- Reduces errors (validate each item against source before writing)
- Persists progress (incremental writes)
- Localizes mistakes (one wrong item is isolated)

**When to use:**
- Data extraction/transformation workflows
- Multi-file generation
- Batch processing tasks

**When to avoid:**
- Simple single-action commands
- Commands where batch processing is more efficient and safe

## Steps

1. **Define command purpose**
   - What problem does it solve?
   - Who will use it?
   - What's the expected outcome?

2. **Structure the command**
   - Start with ## Overview
   - Add ## Steps for multi-step workflows
   - Include ## Checklist for verification items
   - Add ## Examples if helpful

3. **Write clear instructions**
   - Use imperative mood ("Review code", not "Reviewing code")
   - Be specific about actions
   - Include context where needed
   - Add technical details if required

4. **Test the command**
   - Save the file in `.cursor/commands/`
   - Type `/` in chat to verify it appears
   - Run the command with test input
   - Refine based on results

5. **Final review (only when something is clearly wrong)**
   - After work is done, skim the command for:
     - **Repetitions**: Same instruction or requirement in multiple places — merge or reference once.
     - **Obvious optimization**: Redundant bullets, overlapping checklist items, or unnecessarily long wording that can be shortened without losing meaning.
   - **Do not force changes**: Only fix what is evidently wrong. If nothing stands out, leave the command as is.

## Command Template

```markdown
# [Command Name]

## Overview
[Clear, 1-2 sentence description of what this command does and why it's useful]

## Steps
1. **[Step name]**
   - [Action item]
   - [Action item]
   - [Action item]

2. **[Step name]**
   - [Action item]
   - [Action item]

3. **[Step name]**
   - [Action item]
   - [Action item]

## [Optional Section Name]
[Additional context, examples, or guidelines]

## Checklist
- [ ] [Verification item]
- [ ] [Verification item]
- [ ] [Verification item]
```

## Best Practices

### DO:
- ✅ Keep commands focused on a single workflow
- ✅ Use descriptive section headers
- ✅ Include actionable steps
- ✅ Add checklists for verification
- ✅ Write in plain, clear English
- ✅ Test commands before sharing

### DON'T:
- ❌ Create overly complex commands
- ❌ Mix multiple unrelated workflows
- ❌ Use vague or ambiguous language
- ❌ Forget to include overview section
- ❌ Skip testing the command
- ❌ Use code blocks for instructions (use them for examples only)

## Parameters Usage

Commands can accept additional context when invoked:
```
/command-name additional context here
```

Anything after the command name is included in the model prompt alongside your command content.

## Examples of Good Commands

### Simple command (single purpose)
```markdown
# Format Code

## Overview
Automatically format all code files according to project style guidelines.

## Steps
1. **Identify files to format**
   - Find all source files in project
   - Exclude generated files
   - Check file types

2. **Apply formatting**
   - Run project formatter
   - Fix style violations
   - Verify no syntax errors

## Checklist
- [ ] All files formatted
- [ ] No syntax errors introduced
- [ ] Style guide compliance verified
```

### Complex command (multi-step workflow)
```markdown
# Setup New API Endpoint

## Overview
Create a new REST API endpoint with proper structure, validation, tests, and documentation.

## Steps
1. **Define endpoint specification**
   - Determine HTTP method and path
   - Define request/response schemas
   - Document expected behavior
   - Plan error handling

2. **Implement endpoint**
   - Create route handler
   - Add input validation
   - Implement business logic
   - Add error handling

3. **Write tests**
   - Unit tests for handler
   - Integration tests for endpoint
   - Test error cases
   - Verify response format

4. **Update documentation**
   - Add API documentation
   - Include example requests
   - Document error responses
   - Update changelog

## API Endpoint Checklist
- [ ] Route defined and registered
- [ ] Input validation implemented
- [ ] Business logic complete
- [ ] Error handling added
- [ ] Unit tests written and passing
- [ ] Integration tests written and passing
- [ ] API documentation updated
- [ ] Example requests included
```

## Command Creation Checklist
- [ ] Command name is descriptive and kebab-case
- [ ] File saved in `.cursor/commands/` directory
- [ ] Overview section clearly explains purpose
- [ ] Steps are actionable and specific
- [ ] Checklist items are verifiable
- [ ] Command tested in chat with `/`
- [ ] Command produces expected results
- [ ] Documentation is clear and complete

### Final review (only fix if clearly wrong):
- [ ] No obvious repetitions (same instruction in multiple places)
- [ ] No redundant or overlapping items; wording not unnecessarily long

## Notes
- Keep commands updated as workflows evolve
