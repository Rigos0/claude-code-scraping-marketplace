# Rigos0's Web Scraping Marketplace for Claude Code

**An opinionated, community-created marketplace for web scraping with Claude Code.**

> **Disclaimer:** This is an unofficial, community-maintained marketplace created by [@Rigos0](https://github.com/Rigos0). Not affiliated with or endorsed by Apify or Anthropic. Use at your own discretion.

This marketplace provides curated integrations with industry-leading web scraping platforms, specifically optimized for Claude Code workflows.

## 🚀 Available Plugins

### Apify Plugin

An opinionated integration with the Apify platform, designed specifically for Claude Code workflows.

**What makes this opinionated:**
- Intelligent Actor discovery with curated recommendations
- Smart input handling with automatic field resolution
- Dual-mode data retrieval (in-context MCP or file export)
- Built-in cost tracking and transparency
- Proactive URL/handle resolution using RAG

**Features:**
- 🔍 Search 1000+ ready-to-use Apify Actors
- 🌐 Scrape any website (Twitter/X, Instagram, LinkedIn, e-commerce, etc.)
- 🔐 OAuth authentication - no API keys to manage
- 💰 Transparent pay-per-result pricing (free tier available)
- 📊 Flexible data export (JSON/CSV/Excel/XML)
- 🤖 No API limits or rate restrictions
- 🧠 Smart workflow automation with minimal user input

[View Apify Plugin Documentation →](./apify-plugin/README.md)

## 📦 Installation

1. Add this marketplace to Claude Code:
   ```bash
   /plugin marketplace add Rigos0/scraping-marketplace
   ```

2. Install the plugin you need:
   ```bash
   /plugin install apify-plugin
   ```

3. Configure your API credentials (see individual plugin READMEs)

## 🎯 Use Cases

- **Social Media Analysis**: Scrape tweets, posts, profiles, and engagement metrics
- **Market Research**: Extract product data, prices, reviews from e-commerce sites
- **Lead Generation**: Gather business contacts, emails, company information
- **Content Monitoring**: Track news, articles, competitor content
- **Data Collection**: Build datasets for AI/ML training

## 🛠️ Coming Soon

- More scraping platform integrations
- Custom scraper templates
- Data transformation tools
- Scheduling and automation features

## 📖 Documentation

Each plugin has its own README with detailed setup instructions and usage examples.

## 💡 Philosophy

This marketplace is **opinionated** by design:

- **Claude Code First**: Workflows optimized specifically for Claude Code's capabilities
- **Smart Defaults**: Intelligent parameter resolution to minimize user friction
- **Cost Transparency**: Always show what you're paying for
- **Curated Quality**: Recommended tools are tested and proven
- **Progressive Complexity**: Simple tasks are simple, complex tasks are possible

## 🤝 Contributing

This is a community-maintained marketplace. Contributions are welcome!

- Found a bug? [Open an issue](https://github.com/Rigos0/scraping-marketplace/issues)
- Have a feature request? [Start a discussion](https://github.com/Rigos0/scraping-marketplace/discussions)
- Want to contribute? Fork and submit a PR

## ⚠️ Important Notes

- **Not Official**: This marketplace is not affiliated with or endorsed by Apify or Anthropic
- **Community Maintained**: Created and maintained by [@Rigos0](https://github.com/Rigos0)
- **OAuth Authentication**: Uses secure OAuth flow - no API keys to manage!
- **Free Tier Available**: Apify offers a free tier to get started
- **Use Responsibly**: Always respect website Terms of Service and robots.txt
- **Costs Apply**: Apify Actors consume compute units - check pricing before running

## 📄 License

This marketplace configuration and documentation are provided as-is. Individual plugins may have their own licenses.

---

**Created by [@Rigos0](https://github.com/Rigos0)** | [GitHub](https://github.com/Rigos0/scraping-marketplace)
