# Info Researcher Plugin

AI-powered research agent for finding current information online using multiple data sources.

## What It Does

- **Multi-source Search**: Uses Brave Search, Tavily, Bright Data, Reddit, and built-in web search
- **Critical Analysis**: Evaluates source credibility
- **Structured Results**: Organizes findings into clear sections
- **Sequential Thinking**: Uses MCP sequential-thinking for complex queries
- **Facts with Sources**: Provides specific numbers, quotes, and references

## Agent

### `Info Researcher`
Research agent that finds current information online for any given query.

**Capabilities:**
- Multiple searches with different phrasings
- Gathers facts from various sources
- Critically evaluates information credibility
- Structures results into sections:
  - Key findings
  - Main sources
  - Additional details
  - Conflicting information (if any)

## MCP Servers Used

### 1. **Brave Search**
Privacy-focused search engine.
- Fast search results
- Quality content
- API: [Brave Search API](https://brave.com/search/api/)

### 2. **Tavily**
Specialized search for AI agents.
- Optimized for LLMs
- Structured data
- API: [Tavily API](https://tavily.com)

### 3. **Bright Data**
Web scraping and data collection platform.
- Real-time web data access
- PRO mode with advanced features
- API: [Bright Data MCP](https://brightdata.com)

### 4. **Reddit**
Search Reddit for community opinions.
- Current discussions
- User experiences
- Open access (no token required)

### 5. **Sequential Thinking**
Server for complex reasoning chains.
- Analyzes complex queries
- Step-by-step thinking
- No token required

## API Token Setup

### Required Tokens

For full functionality, the following API keys are needed:

| Service | Environment Variable | Required |
|---------|---------------------|----------|
| Brave Search | `BRAVE_API_KEY` | Recommended |
| Tavily | `TAVILY_API_KEY` | Recommended |
| Bright Data | `BRIGHTDATA_API_TOKEN` | Optional |

### 1. Getting API Keys

#### Brave Search API

1. Go to [Brave Search API](https://brave.com/search/api/)
2. Sign up (free tier: 2,000 requests/month)
3. Create an API key in your dashboard
4. Copy the key

#### Tavily API

1. Go to [tavily.com](https://tavily.com)
2. Sign up (free tier: 1,000 requests/month)
3. Get your API key from account settings
4. Copy the key

#### Bright Data API (Optional)

1. Go to [brightdata.com](https://brightdata.com)
2. Sign up
3. Create an API token in the control panel
4. Copy the token

### 2. Setting Environment Variables

#### macOS / Linux (Zsh)

Add to `~/.zshrc`:

```bash
# Researcher Plugin API Keys
export BRAVE_API_KEY="your_brave_search_key"
export TAVILY_API_KEY="your_tavily_key"
export BRIGHTDATA_API_TOKEN="your_brightdata_token"  # optional
```

Then apply changes:

```bash
source ~/.zshrc
```

#### macOS / Linux (Bash)

Add to `~/.bashrc` or `~/.bash_profile`:

```bash
# Researcher Plugin API Keys
export BRAVE_API_KEY="your_brave_search_key"
export TAVILY_API_KEY="your_tavily_key"
export BRIGHTDATA_API_TOKEN="your_brightdata_token"  # optional
```

Then apply changes:

```bash
source ~/.bashrc
```

#### Windows (PowerShell)

```powershell
# Temporary (until session closes)
$env:BRAVE_API_KEY="your_brave_search_key"
$env:TAVILY_API_KEY="your_tavily_key"
$env:BRIGHTDATA_API_TOKEN="your_brightdata_token"

# Permanent (system environment variables)
[System.Environment]::SetEnvironmentVariable('BRAVE_API_KEY', 'your_brave_search_key', 'User')
[System.Environment]::SetEnvironmentVariable('TAVILY_API_KEY', 'your_tavily_key', 'User')
[System.Environment]::SetEnvironmentVariable('BRIGHTDATA_API_TOKEN', 'your_brightdata_token', 'User')
```

### 3. Verify Installation

Check that environment variables are set:

```bash
echo $BRAVE_API_KEY
echo $TAVILY_API_KEY
echo $BRIGHTDATA_API_TOKEN
```

All commands should output your API keys (not empty strings).

### 4. Restart Claude Code

After setting environment variables, **you must restart Claude Code** for changes to take effect.

## Installation

1. Install the plugin from Claude Code marketplace
2. Configure environment variables (see above)
3. Restart Claude Code
4. Start using the Info Researcher agent

## Usage

Simply invoke the agent and ask a question:

```
@info-researcher Find the latest news about GPT-4
```

```
@info-researcher What are the most popular React frameworks in 2024?
```

```
@info-researcher Compare Python and Go performance for web development
```

## Example Output

```
🔍 Research Results: "Latest news about GPT-4"

━━━━━━━━━━━━━━━━━━━━━━━━━━
📌 Key Findings:

1. OpenAI announced GPT-4 Turbo with improved speed
2. Context window increased to 128K tokens
3. Cost reduced by 50% compared to GPT-4

━━━━━━━━━━━━━━━━━━━━━━━━━━
📚 Main Sources:

- OpenAI Blog: "Introducing GPT-4 Turbo" (openai.com)
- TechCrunch: "OpenAI's latest update..." (techcrunch.com)
- Reddit r/MachineLearning: Community discussion

━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 Additional Details:

- Availability: API available to all Plus users
- Performance: 40% faster than previous version
- New features: JSON mode, improved function handling

━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ Conflicting Information:

Some sources indicate different release dates.
Official date: November 6, 2024.
```

## Working Without All Tokens

The plugin will work even without some tokens:

- **Without tokens**: Uses only built-in web_search
- **With Brave or Tavily**: Significantly improves result quality
- **With Bright Data**: Adds web scraping capabilities
- **All tokens**: Maximum efficiency and source coverage

## Usage Tips

1. **Be specific with queries**: "Best React practices 2024" is better than "React"
2. **Specify timeframes**: "Latest news", "2024 trends"
3. **Request comparisons**: "Compare X and Y" for detailed analysis
4. **Ask for numbers**: "Usage statistics", "Performance benchmarks"

## Configuration

MCP servers are pre-configured in `.mcp.json`. No manual setup needed after setting environment variables.

## Requirements

- Claude Code v1.0+
- Node.js 18+ (for MCP servers)
- Python 3.8+ (for Reddit MCP, if using uvx)

## Security

**Important**: Never commit API keys to repositories!

- ✅ Use environment variables
- ✅ Add `.env` to `.gitignore`
- ✅ Store tokens securely
- ❌ Don't hardcode tokens in code
- ❌ Don't publish tokens in public repositories

## Troubleshooting

If you encounter issues:

1. Check that all environment variables are set
2. Ensure Claude Code is restarted after setting variables
3. Verify free tier limits on APIs
4. Confirm API keys are valid

## What Makes It Different

Unlike simple search:
- ✅ **Multiple sources** (not just one search engine)
- ✅ **Credibility evaluation** (assesses source reliability)
- ✅ **Structured output** (organized by sections)
- ✅ **Cross-referencing** (identifies conflicting information)
- ✅ **Source citations** (provides references for all facts)

## Use Cases

- **Research**: Latest technology trends, scientific findings
- **Comparisons**: Framework comparisons, tool evaluations
- **News**: Current events, industry updates
- **Statistics**: Market data, usage metrics
- **Best Practices**: Current recommendations, expert opinions
- **Community Insights**: Reddit discussions, user experiences

## Example Queries

### Technology Research
```
@info-researcher What are the main differences between Next.js 14 and Remix?
@info-researcher Latest security vulnerabilities in Node.js packages
@info-researcher Best practices for React Server Components
```

### Market Research
```
@info-researcher Current adoption rates of TypeScript in 2024
@info-researcher Most popular VS Code extensions for Python development
@info-researcher Salary trends for frontend developers
```

### General Research
```
@info-researcher Explain quantum computing recent breakthroughs
@info-researcher Climate change data from the last 5 years
@info-researcher Space exploration missions planned for 2025
```

## Agent Behavior

The Info Researcher agent:
- Makes multiple searches with different phrasings
- Cross-references information from multiple sources
- Flags when sources disagree
- Provides direct quotes when available
- Always cites sources
- Admits when information is not found or uncertain

**Important**: The agent does NOT make up information. If data is unavailable or uncertain, it will explicitly state this.

---

**Note**: This plugin performs research only. It doesn't modify code automatically.
