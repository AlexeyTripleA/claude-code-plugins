# Universal Code Review Plugin

AI-powered code reviewer checking security, performance, and code quality with live documentation via Context7.

## What it does

- **Security**: OWASP Top 10 vulnerabilities, hardcoded secrets, injections
- **Performance**: Algorithm complexity, N+1 queries, memory leaks
- **Code Quality**: Best practices, anti-patterns, deprecated APIs
- **Live Docs**: Verifies code against current library documentation

## Commands

### `/quick-check [path]`
Fast scan without documentation checks. Perfect for quick verification.

```bash
/quick-check              # Staged files
/quick-check src/api/     # Specific directory
/quick-check src/auth.js  # Specific file
```

**Speed**: < 30 seconds  
**Checks**: Critical security, obvious performance issues, basic quality

---

### `/review [path]`
Balanced review with selective Context7 usage. Default command.

```bash
/review                   # Staged files
/review src/              # Full directory
/review src/components/UserForm.tsx
```

**Speed**: 30-60 seconds  
**Checks**: All security, performance bottlenecks, code quality + selective doc verification

---

### `/deep-review [path]`
Comprehensive analysis with full Context7 integration.

```bash
/deep-review              # Staged files
/deep-review src/         # Deep analysis of directory
```

**Speed**: 1-3 minutes  
**Checks**: Everything + deprecated patterns, outdated APIs, framework-specific best practices

## What it catches

### 🔴 Security
- Hardcoded passwords, API keys, tokens
- SQL injection, XSS, command injection
- Missing authentication/authorization
- Insecure crypto, exposed secrets
- Known CVEs in dependencies

### 🟡 Performance
- O(n²) algorithm complexity
- N+1 database query problems
- Memory leaks (listeners, timers)
- Sequential API calls (use Promise.all)
- Missing caching, pagination

### 🟢 Code Quality
- Code smells (long functions, deep nesting)
- Anti-patterns (callback hell, god objects)
- Deprecated APIs via Context7
- Missing error handling
- Poor naming, duplicated code

## Example Output

### Quick Check
```
⚡ Quick Check Results

Files scanned: 3

🔴 Critical Issues: 1
🟠 High Priority: 2
🟡 Medium Priority: 4

🔴 CRITICAL: Hardcoded API Key
File: src/config.ts:12
Fix: Move to environment variables

🟠 HIGH: N+1 Query Problem
File: src/api/posts.ts:45
Fix: Use eager loading with include

💡 Run '/deep-review' for comprehensive analysis
```

### Deep Review
```
🔍 Deep Review Results

📦 Project Context:
- React 18.3.1
- TypeScript 5.2
- Next.js 14.0

Files analyzed: 8
Lines of code: ~1,200

━━━━━━━━━━━━━━━━━━━━━━━━━━

🔴 CRITICAL Issues: 0
🟠 HIGH Priority: 2
🟡 MEDIUM Priority: 5
🟢 Suggestions: 8

━━━━━━━━━━━━━━━━━━━━━━━━━━

📚 Documentation Insights:
- Found 2 deprecated React patterns
- axios interceptor pattern has better alternative
- 1 security best practice violation

━━━━━━━━━━━━━━━━━━━━━━━━━━

[Detailed findings with Context7 references]
```

## Context7 Integration

Verifies your code against **live, version-specific documentation**:

1. **Detects** your libraries from package.json
2. **Queries** Context7 for current docs
3. **Compares** your code patterns
4. **Flags** deprecated/outdated approaches
5. **Suggests** modern alternatives with references

**Example:**
```javascript
// Your code uses old pattern
useEffect(() => { ... }, [])

// Context7 checks React 18.3 docs
// Flags if pattern is deprecated
// Suggests current best practice
```

## Setup

### 1. Get Context7 API Key (Free)

1. Go to [context7.com](https://context7.com)
2. Sign up (free tier available)
3. Get your API key

### 2. Configure Environment Variable

Add to your shell config (`~/.zshrc` or `~/.bashrc`):
```bash
export UPSTASH_CONTEXT7_API_KEY="your_context7_api_key_here"
```

Then reload:
```bash
source ~/.zshrc  # or ~/.bashrc
```

### 3. Restart Claude Code

After setting the environment variable, restart Claude Code for changes to take effect.

## Installation

1. Install plugin in Claude Code marketplace
2. Set `UPSTASH_CONTEXT7_API_KEY` environment variable (see Setup above)
3. Restart Claude Code
4. Run `/review` to start

**Note:** Without Context7 API key, `/quick-check` command will still work for basic security and performance checks, but documentation verification will be limited.

## Helper Skills (Automatic Hints)

The plugin includes **lightweight Skills** that automatically notice issues during normal conversations:

### Security Hint
Activates when Claude sees potentially insecure patterns:
```
You: "Why isn't this working?"
[shows code with SQL injection]

Claude: "I see SQL string concatenation on line 23, which could 
allow SQL injection. Run `/review src/api/` to check for 
security vulnerabilities."
```

### Performance Hint
Activates when Claude notices performance issues:
```
You: "How can I improve this?"
[shows nested loops]

Claude: "This nested loop creates O(n²) complexity. 
Run `/quick-check` for performance optimization suggestions."
```

### Code Quality Hint
Activates when Claude sees maintainability concerns:
```
You: "What's wrong here?"
[shows 100-line function]

Claude: "This function is quite long. Consider splitting it.
Run `/review src/service.js` for refactoring suggestions."
```

**Key points:**
- Skills work automatically - no need to invoke them
- They only provide brief hints, not full analysis
- They always suggest running a command for detailed review
- Skills don't replace commands - they complement them

## Configuration

Context7 is pre-configured in `.mcp.json`. No manual setup needed.

## Tips

- Start with `/quick-check` for fast feedback
- Use `/review` as default workflow
- Run `/deep-review` before major commits or PRs
- Helper Skills will nudge you during normal coding conversations
- Combine with linters - this catches logic issues, not syntax

## What's Different

Unlike traditional linters:
- ✅ Catches **logic errors** (N+1 queries, SQL injection)
- ✅ Verifies against **current documentation**
- ✅ Understands **context** (framework-specific patterns)
- ✅ Explains **why** something is wrong

## Requirements

- Claude Code v1.0+
- Node.js 18+ (for Context7 MCP)

---

**Note**: This plugin performs analysis only. It doesn't modify code automatically.
