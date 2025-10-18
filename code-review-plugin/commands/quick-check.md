---
description: Fast code review checking security, performance, and quality
allowed-tools: Bash(git:*), Read
model: claude-3-5-haiku-20241022
argument-hint: [file-path] or leave empty for staged files
---

# Quick Check

Fast code review without Context7 documentation checks. Scans for critical issues in security, performance, and code quality.

## Target

Complete in < 30 seconds

## 1. Detect Files to Scan

**If argument provided**: Scan specified file/directory  
**If no argument**: Scan staged files via `git diff --cached --name-only`

If no staged files, scan recently modified files:
```bash
git diff HEAD --name-only
```

## 2. Invoke Agents (Parallel)

Run all 3 agents simultaneously for speed:

### @security-reviewer
- Focus on CRITICAL and HIGH severity
- Skip low-priority warnings
- Report exploitable vulnerabilities

### @performance-reviewer
- Check algorithm complexity
- Look for obvious N+1 queries
- Flag memory leak patterns

### @code-quality-reviewer
- Skip Context7 checks (quick mode)
- Only check basic code smells
- Flag obvious anti-patterns

## 3. Generate Summary Report

```
⚡ Quick Check Results

Files scanned: X

🔴 Critical Issues: X
🟠 High Priority: X
🟡 Medium Priority: X

[Details by category]

💡 Run '/deep-review' for comprehensive analysis with documentation checks.
```

## Output Style

- Terse and actionable
- Only show issues found
- Group by severity, then by type
- Include file:line references

