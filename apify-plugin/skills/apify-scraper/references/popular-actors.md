# Popular Apify Actors Quick Reference

Quick access to frequently used Actors and their key configuration patterns.

## Social Media

### Twitter/X: `xtdata/twitter-x-scraper`
**Rating:** 5.0/5 ⭐ | **Success Rate:** 99.8% | **Pricing:** ~$0.0002/tweet

**Common patterns:**
```json
// By username
{"twitterHandles": ["username"], "maxItems": 50, "sort": "Latest"}

// By search
{"searchTerms": ["keyword"], "maxItems": 50, "sort": "Latest"}

// By URL
{"startUrls": ["https://twitter.com/username"], "maxItems": 50}
```

**Key fields:**
- `twitterHandles`: Array of usernames (without @)
- `searchTerms`: Array of search queries (mutually exclusive with handles)
- `startUrls`: Array of Twitter URLs
- `maxItems`: Number of tweets
- `sort`: "Latest" or "Top"
- `tweetLanguage`: ISO code ("en", "es", etc.)
- `onlyVerifiedUsers`, `onlyImage`, `onlyVideo`: Boolean filters
- `start`, `end`: Date strings "YYYY-MM-DD"

**Important:** Cannot use `twitterHandles` and `searchTerms` together.

---

### Instagram: `apify/instagram-scraper`
**Popular:** High usage | **Best for:** Posts, profiles, hashtags

**Common patterns:**
```json
// By username
{"usernames": ["username"], "resultsLimit": 50}

// By hashtag
{"hashtags": ["hashtag"], "resultsLimit": 50}

// By URL
{"directUrls": ["https://instagram.com/p/POST_ID/"], "resultsLimit": 50}
```

**Key fields:**
- `usernames`: Array of Instagram usernames
- `hashtags`: Array of hashtags (with or without #)
- `directUrls`: Specific post/profile URLs
- `resultsLimit`: Number of items

---

### LinkedIn Scrapers
**Note:** Often requires authentication
**Popular actors:** `voyager/linkedin-profile-scraper`, `dSero/linkedin-profile-scraper`

**Common pattern:**
```json
{"profileUrls": ["https://linkedin.com/in/username"], "maxResults": 10}
```

---

## E-commerce

### Amazon: `junglee/amazon-crawler`
**Best for:** Product data, prices, reviews

**Common patterns:**
```json
// Search products
{"searchKeywords": ["laptop"], "maxItems": 100, "country": "US"}

// Specific products
{"productUrls": ["https://amazon.com/dp/ASIN"], "maxItems": 50}

// Category scraping
{"categoryUrls": ["https://amazon.com/s?k=category"], "maxItems": 200}
```

**Key fields:**
- `searchKeywords`: Product search terms
- `productUrls`: Specific product URLs or ASINs
- `categoryUrls`: Category page URLs
- `maxItems`: Result limit
- `country`: Country code ("US", "UK", etc.)

---

## Content & Generic Scrapers

### Google Search: `apify/google-search-scraper`
**Best for:** Search results, organic listings

**Common pattern:**
```json
{
  "queries": ["search term"],
  "maxPagesPerQuery": 1,
  "resultsPerPage": 10,
  "languageCode": "en",
  "countryCode": "us"
}
```

---

### Web Browser (RAG): `apify/rag-web-browser`
**Built-in tool:** `apify-slash-rag-web-browser`
**Best for:** RAG pipelines, content extraction as Markdown

**Common pattern:**
```json
{
  "query": "search term or URL",
  "maxResults": 3,
  "outputFormats": ["markdown"]
}
```

**Key fields:**
- `query`: Google search keywords OR direct URL
- `maxResults`: Number of pages to scrape (default: 3)
- `outputFormats`: Array with "text", "markdown", or "html"

**Note:** This Actor has a dedicated MCP tool - prefer using that.

---

### Generic Scrapers

**`apify/cheerio-scraper`**
- Best for: Fast HTML scraping without JavaScript
- Use when: Target site doesn't require JS rendering

**`apify/playwright-scraper`**
- Best for: JavaScript-heavy sites
- Use when: Site requires browser rendering

**`apify/web-scraper`**
- Best for: Custom web scraping with CSS/XPath
- Use when: No dedicated scraper exists
- Complexity: Requires configuration

---

## Quick Selection Guide

**Social Media?**
- Twitter → `xtdata/twitter-x-scraper`
- Instagram → `apify/instagram-scraper`
- LinkedIn → Search for LinkedIn actor

**E-commerce?**
- Amazon → `junglee/amazon-crawler`
- Other → Search for platform-specific actor

**Generic Website?**
- Static HTML → `apify/cheerio-scraper`
- JavaScript-heavy → `apify/playwright-scraper`
- For RAG/Markdown → `apify/rag-web-browser`
- Custom needs → `apify/web-scraper`
