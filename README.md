# Rigos0's Web Scraping Marketplace for Claude Code

An opinionated, community-created marketplace for web scraping with Claude Code.

## Installation

1. Add this marketplace to Claude Code:
   ```bash
   /plugin marketplace add Rigos0/claude-code-scraping-marketplace
   ```

2. Install the plugin you need:
   ```bash
   /plugin install apify-plugin
   ```

3. **Restart Claude Code** (exit and reopen)

4. Authenticate with Apify:
   - Run the command: `/mcp`
   - Find "apify" in the MCP servers list
   - Select it and click "Authenticate"
   - Your browser will open - sign in to your Apify account
   - Click "Authorize" when prompted
   - Return to Claude Code - authentication complete!

You only need to authenticate once. Claude Code will maintain the authentication.

## What This Marketplace Provides

This marketplace provides curated integrations with web scraping platforms, specifically optimized for Claude Code workflows.

### Apify Plugin

An opinionated integration with the Apify platform that handles web scraping intelligently.

**What makes this opinionated:**
- Intelligent Actor discovery with curated recommendations
- Smart input handling with automatic field resolution
- Dual-mode data retrieval (in-context MCP or file export)
- Built-in cost tracking and transparency
- Proactive URL/handle resolution using RAG

**Key Features:**
- Search 1000+ ready-to-use Apify Actors
- Scrape any website (Twitter/X, Instagram, LinkedIn, e-commerce, etc.)
- OAuth authentication - no API keys to manage
- Transparent pay-per-result pricing (free tier available)
- Flexible data export (JSON/CSV/Excel/XML)
- Smart workflow automation with minimal user input

[View Apify Plugin Documentation](./apify-plugin/README.md)

## Use Cases

- Social Media Analysis: Scrape tweets, posts, profiles, and engagement metrics
- Market Research: Extract product data, prices, reviews from e-commerce sites
- Lead Generation: Gather business contacts, emails, company information
- Content Monitoring: Track news, articles, competitor content
- Data Collection: Build datasets for AI/ML training

## Philosophy

This marketplace is opinionated by design:

- Claude Code First: Workflows optimized specifically for Claude Code's capabilities
- Smart Defaults: Intelligent parameter resolution to minimize user friction
- Cost Transparency: Always show what you're paying for
- Curated Quality: Recommended tools are tested and proven
- Progressive Complexity: Simple tasks are simple, complex tasks are possible

## Contributing

This is a community-maintained marketplace. Contributions are welcome!

- Found a bug? [Open an issue](https://github.com/Rigos0/scraping-marketplace/issues)
- Have a feature request? [Start a discussion](https://github.com/Rigos0/scraping-marketplace/discussions)
- Want to contribute? Fork and submit a PR

## Important Notes

- Not Official: This marketplace is not affiliated with or endorsed by Apify or Anthropic
- Community Maintained: Created and maintained by [@Rigos0](https://github.com/Rigos0)
- OAuth Authentication: Uses secure OAuth flow - no API keys to manage
- Free Tier Available: Apify offers a free tier to get started
- Use Responsibly: Always respect website Terms of Service and robots.txt
- Costs Apply: Apify Actors consume compute units - check pricing before running

## License

This marketplace configuration and documentation are provided as-is. Individual plugins may have their own licenses.

---

**Created by [@Rigos0](https://github.com/Rigos0)** | [GitHub](https://github.com/Rigos0/scraping-marketplace)
