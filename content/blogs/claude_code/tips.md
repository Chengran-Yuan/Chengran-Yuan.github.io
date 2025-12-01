# Claude Code Cost Optimization Guidelines

This file contains instructions for Claude to automatically optimize token usage and reduce costs while working on this project.

## 🎯 Primary Rules (ALWAYS Follow)

1. **Use Haiku Model by Default**
   - Current model: haiku (claude-haiku-4-5-20251001)
   - Haiku costs 1/5 of Sonnet
   - ONLY escalate to Sonnet when: complex reasoning, architectural decisions, or deep code analysis required
   - NEVER use without explicit user request

2. **Prefer Search Over Read**
   - ALWAYS use Grep/search tools instead of Read tool when possible
   - Grep costs 100x LESS than Read
   - Example: Search for 'database' in config.yaml (NOT read entire file)
   - This is the SINGLE MOST IMPORTANT cost optimization rule

3. **Specify Line Ranges When Reading**
   - If you MUST use Read: always specify `offset` and `limit` parameters
   - Example: Read lines 1-100 (NOT entire 5000-line file)
   - This saves 100x cost on large files
   - Default: Read max 500 lines unless specific range given

4. **Batch Operations in Parallel**
   - ALWAYS combine multiple independent operations in single message
   - Reading 3 files in parallel = cost of 1 file + 3x speed
   - Call multiple tools at once: Glob, Grep, Read (independent ones)
   - DO NOT make sequential tool calls when parallel is possible

## 🔍 Optimization Strategy Rules

### Rule 5: Use Explore Agent for Codebase Discovery
- When asked "how does X work?" or "find Y in codebase"
- Use Task tool with `subagent_type=Explore`
- Costs 5x less than manual searching
- Perfect for: understanding code structure, finding implementations, locating patterns

### Rule 6: Plan Major Changes with TodoWrite
- BEFORE making significant refactoring or new features
- Create detailed plan with TodoWrite tool
- Break down into specific, measurable steps
- Prevents costly rework and tracks progress
- Example: "Let me create a plan first before refactoring the auth module"

### Rule 7: Limit Search Results
- ALWAYS use `head_limit` parameter in Grep
- Request max 50 matches per search
- Narrow scope with glob patterns: `src/**/*.tsx` not entire codebase
- Filter by file type: type="typescript" not broad searches

### Rule 8: Ask Comprehensive Questions Once
- NEVER ask multi-part questions across multiple messages
- Combine related questions in single prompt
- Reduces iteration count = reduces cost by 2/3

**Bad Example:**
```
Message 1: "What files are in src/?"
Message 2: "Show me utils.js"
Message 3: "What's the formatDate function?"
Message 4: "Show usage examples"
```

**Good Example:**
```
"Search for formatDate function in src/utils.ts and show definition + top 3 usage examples"
```

### Rule 9: Provide Context Upfront
- Include file paths, line numbers, and specific locations
- Example: NOT "search for handleError"
- Better: "find handleError in src/services/*.ts"
- Provides scope = faster, cheaper results

### Rule 10: Reuse Conversation Context
- NEVER ask for same information twice
- Reference previous findings: "Based on the earlier search showing..."
- Build on prior context: cost is FREE to reuse
- Avoid phrases like "can you find X again?"

### Rule 11: Use Smart Filtering
- BEFORE searching/reading, filter irrelevant data
- Use glob patterns to narrow scope
- Filter by file type: `--type typescript`
- Filter by folder: `src/components/` not entire src/
- Reduces processing by up to 95%

### Rule 12: Create Task Lists for Complex Work
- ALWAYS use TodoWrite for multi-step tasks (3+ steps)
- Organize work before execution
- Mark tasks: pending → in_progress → completed
- Prevents redundant operations = +40% efficiency

### Rule 13: Avoid Repetitive Operations
- Check conversation history before running tools
- Reuse previous search/read results
- Build on existing context
- Example: "Based on the earlier Grep results that showed..."

### Rule 14: Smart File Reading
- NEVER read entire files to find one function/constant
- Read only necessary lines with offset + limit
- For large files: use Grep to find line number, then Read specific range
- Pattern: Grep to locate → Read specific range → analyze

## 📋 Tool Usage Patterns

### Reading Files
```
GOOD:  Read with offset=45, limit=20 (specific range)
BAD:   Read entire 2000-line file without limits
```

### Searching Code
```
GOOD:  Grep pattern="handleError" glob="src/**/*.ts" head_limit=50
BAD:   Read all files and search manually
```

### Exploring Codebase
```
GOOD:  Task with subagent_type=Explore for "how auth works?"
BAD:   Manually grep and read 20 files
```

### Multiple Operations
```
GOOD:  Multiple Glob + Grep calls in single message (parallel)
BAD:   Sequential Read-Grep-Read in multiple messages
```

## 🚫 Cost-Killing Anti-Patterns

**NEVER:**
1. Read large files without line limits
2. Use Read instead of Grep for searching
3. Ask same question twice in same conversation
4. Make sequential calls when parallel is possible
5. Explore codebase without using Explore agent
6. Make major changes without plan
7. Ask vague questions that require exploration
8. Search entire codebase without limiting scope

## 💰 Cost-Saving Checklist

Before executing any command, ask:
- [ ] Am I using the right tool? (Grep vs Read?)
- [ ] Did I limit the scope? (glob patterns, line ranges?)
- [ ] Should I search instead of read?
- [ ] Can I run multiple ops in parallel?
- [ ] Is this information already in conversation?
- [ ] Should I make a plan first?

## 🎯 Expected Cost Reduction

Following these rules should achieve:
- **60-90% cost reduction** on most tasks
- **3x faster execution** through parallelization
- **40% efficiency boost** through better planning
- **95% filtering** of irrelevant data

## Examples of Optimized Workflow

### Bad: "Help me understand the authentication"
```
Cost: HIGH
- Reads 30+ files
- Multiple iterations
- Total: $10+ per session
```

### Good: "How does authentication work in this codebase?"
```
Cost: LOW (~$0.50 per session)
1. Use Explore agent to find auth-related code
2. Task agent identifies key files
3. Read only critical files with line limits
4. Provide comprehensive answer
5. Reuse this context for follow-up questions
```

## ⚙️ Model Configuration

- **Default Model**: haiku (claude-haiku-4-5-20251001)
- **Haiku Uses**: File operations, searches, simple debugging, refactoring
- **Sonnet Uses**: Complex reasoning, architecture, algorithm design
- **Cost Ratio**: Haiku = 1x, Sonnet = 5x, Opus = 60x

## Implementation Notes

These rules are NOT suggestions—they are **requirements** for cost-effective Claude Code usage on this project. Violating them significantly increases costs without benefit.

If a user request seems to violate these rules, explain the cost implications and suggest the optimized approach.

**Last Updated**: 2025-11-13
**Model Version**: Claude Haiku 4.5
**Optimization Status**: Active
