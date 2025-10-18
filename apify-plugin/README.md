# Apify Plugin for Claude Code

Integrate Apify's powerful web scraping and automation platform directly into Claude Code.

## Features

- 🔍 Search and discover Apify actors for web scraping
- 🚀 Run actors directly from Claude Code
- 📊 Retrieve and download scraped data
- 📖 Access Apify documentation
- 💰 Pay-per-result pricing for most actors

## Prerequisites

**Apify Account**: Sign up at [apify.com](https://apify.com)

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

## Support

- [Apify Documentation](https://docs.apify.com)
- [Apify Store](https://apify.com/store)
- [GitHub Issues](https://github.com/Rigos0/scraping-marketplace/issues)

## License

MIT
