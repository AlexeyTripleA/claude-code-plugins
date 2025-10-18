---
description: Universal code review with medium-depth analysis
allowed-tools: Bash(git:*), Read, mcp__context7__*
model: claude-3-5-sonnet-20241022
argument-hint: [file-path] or leave empty for staged files
---

# Review

Universal code review command with balanced depth. Checks security, performance, and quality with selective Context7 usage.

## 1. Detect Scope

**If argument provided**: Scan specified file or directory  
**If no argument**: Scan staged files via `git diff --cached --name-only`

If no staged files, ask user what to review or default to recent changes.

## 2. Context Gathering

Light Context7 usage:
- Only query for libraries actually used in scanned files
- Focus on security and critical best practices docs
- Skip general documentation queries

## 3. Invoke All Agents (Medium Mode)

### @security-reviewer
- All security checks
- Priority on CRITICAL and HIGH
- Report MEDIUM and LOW if found

### @performance-reviewer  
- Check obvious bottlenecks
- Flag N+1 queries and algorithm issues
- Skip micro-optimizations

### @code-quality-reviewer
- Basic code quality checks
- Use Context7 only for suspicious patterns
- Flag clear anti-patterns and code smells

## 4. Generate Balanced Report

```
📋 Code Review Results

Files reviewed: X

━━━━━━━━━━━━━━━━━━━━

Security: [✓/⚠/✗]
Performance: [✓/⚠/✗]  
Code Quality: [✓/⚠/✗]

━━━━━━━━━━━━━━━━━━━━

Issues Found: X total

[Grouped by severity and type]

━━━━━━━━━━━━━━━━━━━━

💡 Tips:
- Run '/deep-review' for comprehensive analysis
- Run '/quick-check' for faster scans
```

## Target Performance

30-60 seconds for typical review scope

## Output Style

- Clear and organized
- Balance between detail and brevity
- Action-oriented recommendations
- Easy to scan visually

