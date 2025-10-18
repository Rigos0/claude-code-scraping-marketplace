# Apify Plugin for Claude Code

**An opinionated Apify integration for Claude Code by [@Rigos0](https://github.com/Rigos0)**

> **Note:** This is an unofficial, community-created plugin. Not affiliated with or endorsed by Apify.

This plugin integrates Apify's powerful web scraping and automation platform directly into Claude Code with intelligent workflows designed to minimize friction and maximize efficiency.

## What Makes This Plugin Opinionated

This isn't just a wrapper around the Apify API - it's designed with specific workflows in mind:

- **Smart Actor Discovery**: Curated recommendations based on success rate, pricing, and maintenance
- **Automatic Input Handling**: Intelligent field resolution using RAG Web Browser for URLs/handles
- **Dual-Mode Data Retrieval**: Choose between in-context (MCP) or file export based on dataset size
- **Built-in Cost Tracking**: Always know what you're paying before and after Actor runs
- **Minimal User Friction**: Ask only for information users actually know, auto-resolve the rest

## Features

- 🔍 Search and discover 1000+ Apify Actors
- 🚀 Run Actors directly from Claude Code
- 📊 Flexible data retrieval (in-context or file export)
- 📖 Access Apify documentation and Actor schemas
- 💰 Transparent pay-per-result pricing with cost reports
- 🧠 Intelligent parameter resolution and smart defaults

## Prerequisites

- **Apify Account**: Sign up at [apify.com](https://apify.com) - free tier available
- **No API Keys Required**: Uses OAuth authentication - just sign in once through Claude Code!

## Installation

1. Add this marketplace to Claude Code:
   ```bash
   /plugin marketplace add Rigos0/scraping-marketplace
   ```

2. Install the Apify plugin:
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

## Usage Examples

### Quick Scrape Command
Use the `/scrape` slash command for quick website scraping:
```
/apify-plugin:scrape https://example.com
```

### Search for Actors
```
Find me an actor for scraping Instagram posts
```

### Run an Actor
```
Use the Twitter scraper to get tweets from @elonmusk
```

### Download Data
```
Download the scraped data to a JSON file
```

## Available Tools

- **search-actors**: Find actors by keywords
- **fetch-actor-details**: Get actor information and input schema
- **call-actor**: Run any Apify actor
- **get-actor-output**: Retrieve scraped data
- **search-apify-docs**: Search Apify documentation
- **apify/rag-web-browser**: Pre-configured web browser for RAG pipelines

## How It Works

This plugin includes:

1. **Apify Scraper Skill** (`skills/apify-scraper/`) - Intelligent workflow automation
2. **Quick Scrape Command** (`commands/scrape.md`) - Fast one-liner scraping
3. **MCP Integration** - Direct access to Apify's official MCP server

The skill provides opinionated workflows on top of the MCP tools, handling Actor selection, input configuration, data retrieval mode selection, and cost reporting automatically.

## Support

- **Plugin Issues**: [GitHub Issues](https://github.com/Rigos0/scraping-marketplace/issues)
- **Apify Platform**: [Apify Documentation](https://docs.apify.com) | [Apify Store](https://apify.com/store)
- **Discussions**: [GitHub Discussions](https://github.com/Rigos0/scraping-marketplace/discussions)

## Contributing

Improvements and feedback welcome! This is a community-maintained plugin.

## License

This plugin configuration and skill are provided as-is. Apify platform and Actors have their own terms of service.
