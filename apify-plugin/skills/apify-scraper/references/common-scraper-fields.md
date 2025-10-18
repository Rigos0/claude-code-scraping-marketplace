# Common Scraper Input Fields

Quick reference for common input fields across Apify Actors to help with automatic field filling.

## Universal Fields

**`maxItems` / `resultsLimit` / `maxResults`**
- Type: Integer
- Default: 50 (balance between cost and utility)
- When to ask: If user mentions "all" or needs large dataset (>100)

**`startUrls` / `urls`**
- Type: Array of strings or objects
- Auto-fill: When user provides explicit URLs
- Format: Simple strings or objects with `url` and `method`

**`proxy` / `proxyConfiguration`**
- Type: Object
- Skip: Auto-filled by Actor unless user mentions geo-location or blocking issues

## Social Media Fields

### Twitter/X

**`twitterHandles` / `handles` / `usernames`**
- Type: Array of strings (without @ symbol)
- Auto-fill: When user mentions "@username" or "from [username]"

**`searchTerms` / `queries`**
- Type: Array of strings
- Auto-fill: When user mentions searching for topics
- Mutually exclusive with `twitterHandles`

**`sort`**
- Type: String (enum: "Top", "Latest")
- Default: "Latest"

**`start` / `end`**
- Type: String (date format "YYYY-MM-DD")
- Auto-fill: Only when user mentions specific dates

**`tweetLanguage`**
- Type: String (ISO 639-1 code: "en", "es", "fr", etc.)
- Skip: Unless user explicitly mentions language

**`onlyVerifiedUsers` / `onlyTwitterBlue`**
- Type: Boolean
- Skip: Unless user explicitly mentions verification

**`onlyImage` / `onlyVideo` / `onlyQuote`**
- Type: Boolean
- Auto-fill: Only when user specifies content type

### Instagram

**`hashtags`**
- Type: Array of strings (with or without # symbol)
- Auto-fill: When user mentions hashtags

**`usernames` / `profiles`**
- Type: Array of strings
- Auto-fill: When user mentions specific accounts

### LinkedIn

**`searchQuery` / `keywords`**
- Type: String
- Auto-fill: From user's query

**`profileUrls`**
- Type: Array of strings
- Auto-fill: When user provides URLs

## E-commerce Fields

### Amazon/E-commerce

**`searchKeywords` / `search`**
- Type: String or Array
- Auto-fill: From user's intent

**`productUrls` / `asinList`**
- Type: Array of strings
- Auto-fill: When user provides URLs

**`minPrice` / `maxPrice`**
- Type: Number
- Auto-fill: Only when user specifies price range

**`categoryUrl`**
- Type: String
- Auto-fill: When user provides category URL

## Generic Web Scraper Fields

**`pageFunction`**
- Type: String (JavaScript code)
- Skip: Advanced users only

**`waitUntil`**
- Type: String (enum: "networkidle", "domcontentloaded", "load")
- Skip: Unless user reports loading issues

**`maxConcurrency`**
- Type: Number
- Skip: Unless user needs speed optimization

**`maxPagesPerCrawl` / `maxCrawlDepth`**
- Type: Number
- Auto-fill: Map from `maxItems` or user intent

## Performance Fields

**`memory`**
- Type: Number (MB)
- Valid values: Powers of 2 (128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768)
- Skip: Unless user has performance issues

**`timeout`**
- Type: Number (seconds)
- Default: 0 (no limit)
- Skip: Unless user needs to limit run time

## Field Prioritization Logic

When configuring Actor input, prioritize in this order:

1. **Required fields** (marked in schema) - Always ask if not obvious
2. **Primary data source** (URLs, handles, hashtags) - Auto-fill from context
3. **Result limits** (maxItems) - Use sensible defaults (50)
4. **Sorting/filtering** (sort, date ranges) - Auto-fill if mentioned
5. **Content filters** (verified, media type) - Only if explicitly mentioned
6. **Advanced options** (proxy, performance) - Skip unless needed
