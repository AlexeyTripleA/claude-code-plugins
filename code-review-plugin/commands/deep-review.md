---
description: Comprehensive review with Context7 documentation verification
allowed-tools: Bash(git:*), Read, mcp__context7__*
model: claude-3-5-sonnet-20241022
argument-hint: [file-path] or leave empty for staged files
---

# Deep Review

Comprehensive code review with live documentation checks via Context7. Detects security issues, performance bottlenecks, code quality problems, and outdated patterns.

## Target

1-3 minutes for thorough analysis

## 1. Gather Context

Detect files to scan (same logic as quick-check).

Read package.json to identify:
- Framework and version (React, Vue, Next.js, etc.)
- Major dependencies and versions
- Build tools

## 2. Query Context7 for Documentation

For each detected library:
```javascript
// Resolve library IDs
mcp__context7__resolve_library_id("react@18.3.1")
mcp__context7__resolve_library_id("axios@1.6.0")

// Get relevant documentation
mcp__context7__get_library_docs("react", "18.3.1", "hooks")
mcp__context7__get_library_docs("react", "18.3.1", "performance")
mcp__context7__get_library_docs("axios", "1.6.0", "best-practices")
```

Keep this context available for all agents.

## 3. Invoke All Agents (Full Mode)

### @security-reviewer
- All severity levels
- Check dependencies for known CVEs
- Verify security best practices per framework

### @performance-reviewer
- Deep complexity analysis
- Check caching strategies
- Verify optimization patterns against docs

### @code-quality-reviewer (with Context7)
- Compare code against current documentation
- Flag deprecated APIs and patterns
- Suggest modern alternatives from docs
- Verify best practices per library

## 4. Generate Comprehensive Report

```
🔍 Deep Review Results

📦 Project Context:
- React 18.3.1
- TypeScript 5.2
- Axios 1.6.0

Files analyzed: X
Lines of code: ~X

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔴 CRITICAL Issues: X
[Details with Context7 references]

🟠 HIGH Priority: X
[Details]

🟡 MEDIUM Priority: X
[Details]

🟢 Suggestions: X
[Details]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📚 Documentation Insights:
- Found X deprecated patterns
- X APIs have newer alternatives
- X best practices violations

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Summary:
[Overall assessment]

Next steps:
[Prioritized action items]
```

## Output Style

- Detailed and educational
- Include documentation references
- Explain WHY issues matter
- Provide specific code fixes
- Link to official docs when relevant

