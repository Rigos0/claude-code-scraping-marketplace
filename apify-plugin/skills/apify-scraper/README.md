# Apify Scraper Skill

Intelligent web scraping using Apify Actors with automatic input handling and dual-mode data retrieval.

## Features

✅ **Smart Input Configuration**
- Automatically fills obvious fields from context
- Asks for clarification only when needed
- Supports all major Apify Actor patterns

✅ **Dual Retrieval Modes**
- **MCP Mode**: Load data directly into conversation (good for <100 items)
- **API Mode**: Save to file in multiple formats (JSON, CSV, Excel, XML, HTML, RSS)

✅ **Intelligent Actor Selection**
- Searches and recommends best Actor for the task
- Prioritizes high-rated, well-maintained Actors
- Supports social media, e-commerce, and generic web scraping

✅ **Comprehensive References**
- Common scraper field patterns
- Popular Actor quick reference
- Field prioritization logic

## Usage

The skill is automatically invoked by the `/scrape` slash command:

```bash
/apify-plugin:scrape x.com tweets by rmladek
/apify-plugin:scrape Instagram posts tagged with #cats
/apify-plugin:scrape Amazon search for laptops under $500
```

You can also invoke it directly:

```
Scrape the latest tweets from @elonmusk
Get Instagram posts from nasa
Extract product data from this Amazon URL
```

## Workflow

1. **Analyze Request** - Understands target platform, data type, and parameters
2. **Find Actor** - Searches and selects the best Apify Actor
3. **Configure Input** - Smart field filling with clarification when needed
4. **Choose Mode** - Asks user: MCP (in-context) or API (file export)
5. **Execute** - Runs the scraper and retrieves data
6. **Present Results** - Summarizes findings or confirms file save

## Retrieval Modes

### MCP Mode (Load into Chat)
- ✅ Immediate analysis and interaction
- ✅ Good for datasets up to ~100 items
- ⚠️ 25,000 token limit for responses
- 📊 Data appears directly in conversation

### API Mode (Save to File)
- ✅ Supports large datasets (millions of items)
- ✅ Multiple formats: JSON, CSV, Excel, XML, HTML, RSS
- ✅ Persistent storage on disk
- 📁 User specifies format and save location

## Supported Platforms

**Social Media:**
- Twitter/X
- Instagram
- LinkedIn
- TikTok
- Facebook

**E-commerce:**
- Amazon
- eBay
- Shopify
- Generic product sites

**Content:**
- News websites
- Blogs
- Forums
- Generic web pages

## Examples

### Example 1: Twitter Scraping (MCP Mode)
```
User: Get 20 recent tweets from @NASA

Skill:
1. Finds xtdata/twitter-x-scraper
2. Auto-configures: {"twitterHandles": ["NASA"], "maxItems": 20, "sort": "Latest"}
3. Asks: "Load into chat or save to file?"
4. User: "Load into chat"
5. Executes and presents tweet summaries
```

### Example 2: Instagram Scraping (API Mode)
```
User: Scrape Instagram posts tagged with #travel, save as CSV

Skill:
1. Finds apify/instagram-scraper
2. Auto-configures: {"hashtags": ["travel"], "resultsLimit": 50}
3. Detects user wants file export
4. Asks: "Where should I save the CSV file?"
5. User: "./instagram_travel.csv"
6. Downloads data using curl and confirms save
```

### Example 3: Ambiguous Request (Needs Clarification)
```
User: Scrape Twitter for AI content

Skill:
1. Finds xtdata/twitter-x-scraper
2. Detects ambiguity: could be search terms OR usernames
3. Asks: "Should I search by keywords ('AI content') or specific Twitter accounts?"
4. User: "Search by keywords"
5. Auto-configures: {"searchTerms": ["AI content"], "maxItems": 50}
6. Continues with mode selection
```

## File Structure

```
apify-scraper/
├── SKILL.md                          # Main skill instructions
├── README.md                         # This file
└── references/
    ├── common-scraper-fields.md     # Field patterns and defaults
    └── popular-actors.md             # Quick reference for common Actors
```

## Reference Documentation

### Common Scraper Fields
Comprehensive guide to input fields across Apify Actors:
- Universal fields (maxItems, startUrls, proxy)
- Social media specific fields (handles, hashtags, search terms)
- E-commerce fields (products, prices, categories)
- Clarification question templates

### Popular Actors
Quick reference for frequently used Actors:
- Social media scrapers (Twitter, Instagram, LinkedIn)
- E-commerce scrapers (Amazon, general)
- Content scrapers (Google Search, RAG browser)
- Actor selection decision tree
- Pricing estimates

## Best Practices

1. **Respect Token Limits**: For >100 items, use API mode
2. **Field Selection**: Only request relevant fields with `get-actor-output`
3. **Cost Awareness**: Check Actor pricing, estimate costs for large scrapes
4. **Privacy**: Remind users about scraping ToS when relevant
5. **Pagination**: Handle large datasets with proper offset/limit

## Troubleshooting

**Token limit exceeded:**
- Skill automatically switches to API mode
- Saves data to file instead

**Actor run fails:**
- Skill provides clear error message
- Suggests alternatives or input adjustments

**Missing required fields:**
- Skill never guesses values
- Always asks for clarification with examples

## Contributing

To improve this skill:
1. Add new common field patterns to `references/common-scraper-fields.md`
2. Update popular Actors in `references/popular-actors.md`
3. Enhance decision logic in `SKILL.md`
4. Submit improvements to the repository

## License

MIT
