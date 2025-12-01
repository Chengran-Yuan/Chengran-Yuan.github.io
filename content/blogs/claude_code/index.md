---
title: 💡 Tips on how to optimize token useage when using claude code
summary: Take full control of your personal brand and privacy by migrating away from the big tech platforms!
date: 2025-11-12

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: ''

authors:
  - admin

tags:
  - tools
  - Efficiency

content_meta:
  trending: true
---

Claude Code is a powerful AI coding assistant, but costs can add up quickly if not used efficiently. Here are 14 proven strategies to optimize your usage and save money while maintaining productivity.

{{< toc mobile_only=true is_open=true >}}

## 💰 Cost Optimization Strategies

### 1. Model Selection is Critical

**Use Claude 3 Haiku by default** - costs only 1/5 of Sonnet. It's extremely fast and cheap for:
- Debugging tasks
- File reading operations
- Simple code searches
- Routine refactoring

> [!TIP]
> Only escalate to Sonnet when you need complex reasoning or architectural decisions.

> [!how] 
> 1. type **/model** in terminal
> 2. choose **haiku**  model

For more details, please refer to this [website](https://support.claude.com/en/articles/11940350-claude-code-model-configuration).


### 2. Use Search Instead of Read

**"Search for X in file" costs 100x less than "read file"**. The Read tool loads entire file contents into context, while Grep only extracts matching lines.

**Example:**
```
❌ "Read config.yaml and find database settings"
✅ "Search for 'database' in config.yaml"
```

### 3. Read Files in Chunks

Specify line numbers when reading large files: `"read lines 1-100 of server.js"`

This saves **100x cost** compared to reading entire files unnecessarily.

### 4. Parallel Operations

Execute multiple operations simultaneously in a single message. Reading 3 files in parallel = cost of 1 file, but **3x faster**.

**Example:**
```
In a single message:
1. Search for handleError in src/utils.js
2. Search for validateInput in src/validators.js
3. Search for logMessage in src/logger.js
```

### 5. Leverage Explore Agent

Use the Task tool with `subagent_type=Explore` for codebase exploration. It's **5x cheaper** than manual searching and automatically finds relevant code patterns.

**Example:**
```
Use Task agent to explore how error handling works in this codebase
```

### 6. Plan Before Modifying

Always create a plan using TodoWrite before major refactoring. This helps:
- Estimate scope and complexity
- Avoid costly rework
- Track progress systematically

**Example:**
```
Create a detailed plan for refactoring the authentication module before making any changes
```

### 7. Set Budget Alerts

Configure budget warnings at **70% and 90%** thresholds to prevent overspending. This gives you time to adjust usage patterns before hitting limits.

### 8. Limit Search Results

Request only the top 50 matches when searching. This keeps results precise and economical.

**Example:**
```
Search for 'TODO' in src/, limit to 50 results
```

### 9. Ask Specific Questions Once

**Reduce multi-turn interactions** by asking precise, comprehensive questions. This can cut costs by **2/3**.

**Bad:**
```
1. "What files are in src/?"
2. "Read utils.js"
3. "What does formatDate do?"
4. "Show me examples of its usage"
```

**Good:**
```
"Search for formatDate function in src/, show definition and top 3 usage examples"
```

### 10. Use Path Shortcuts

Provide clear file paths and line numbers when you know them. This makes operations more efficient and reduces exploration overhead.

### 11. Create Task Lists Upfront

Plan execution order before starting work. This **boosts efficiency by 40%** and prevents redundant operations.

### 12. Smart Reading

Load only necessary code lines. If you need to check a function signature, don't read the entire file.

**Example:**
```
Read lines 45-60 of api.js (where handleRequest is defined)
```

### 13. Avoid Repeat Questions

Reuse conversation context. Information already discussed is free to reference again. Build on previous responses instead of asking from scratch.

### 14. Filter Before Processing

Use glob patterns and type filters to narrow down search scope. The system filters irrelevant data first, potentially **saving up to 95% cost**.

**Example:**
```
Search for 'useState' in src/**/*.tsx (only TypeScript React files)
```

## 🔧 Automation Setup

### Configure Project-Level Guidelines

Create a `CLAUDE.md` file in your project root:

```markdown
# Claude Code Usage Guidelines

## Cost Optimization Rules

1. **Model Selection**: Use Haiku for file operations and searches
2. **File Operations**: Always use Grep/search instead of Read when possible
3. **Planning**: Create TodoWrite plan before major refactoring
4. **Context Reuse**: Reference previous information in conversation
5. **Specific Requests**: Ask precise, single-purpose questions
```

### Create Custom Slash Commands

In `.claude/commands/` directory:

**search.md:**
```markdown
Search for {{pattern}} in {{path}}. Limit results to 50 matches.
```

**plan.md:**
```markdown
Create a detailed plan using TodoWrite before making code changes.
Break down into specific, measurable steps.
```

## 📊 Cost-Saving Examples

### Before Optimization:
```
User: "Help me understand this codebase"
Claude: [Reads 50 files, costs $5]
```

### After Optimization:
```
User: "Use Explore agent to find how user authentication works"
Claude: [Uses targeted search, costs $0.50]
```

**Result: 90% cost reduction with same outcome**

## 🎯 Key Takeaways

1. **Think before you prompt** - Plan your questions to minimize iterations
2. **Search, don't read** - Grep is your best friend
3. **Parallel everything** - Batch operations in single messages
4. **Use the right tool** - Haiku for routine tasks, Sonnet for complexity
5. **Document your patterns** - Create CLAUDE.md to enforce best practices

By following these strategies, you can reduce Claude Code costs by **60-90%** while maintaining or even improving productivity.

> [!NOTE]
> These techniques are based on real usage patterns and token consumption analysis. Your mileage may vary depending on project complexity and workflow.
