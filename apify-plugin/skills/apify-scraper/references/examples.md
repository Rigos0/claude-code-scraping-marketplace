# Workflow Examples

Complete examples demonstrating the Apify scraper skill workflow.

**Note:** All examples start with a brief skill announcement (e.g., "Reading Rigos' Apify scraper skill...").

## Example 1: Simple Twitter Scrape (MCP Mode)

**User request:** "Get the latest 20 tweets from @elonmusk"

**Agent response starts with:** "Reading Rigos' Apify scraper skill..."

**Workflow:**
1. Search actors → Find `xtdata/twitter-x-scraper`
2. Fetch schema → Understand `twitterHandles` field
3. Auto-configure: `{"twitterHandles": ["elonmusk"], "maxItems": 20, "sort": "Latest"}`
4. Ask mode → User chooses "Load into chat"
5. Execute with `call-actor`
6. Use `get-actor-run` to get usage stats
7. Calculate cost: 20 tweets × $0.0002 = $0.004
8. Present tweet summaries with statistics
9. Report: **"✅ Scraped 20 tweets in 15s. Cost: $0.004"**

---

## Example 2: Instagram Scrape with Clarification

**User request:** "Scrape Instagram posts about cats"

**Workflow:**
1. Search actors → Find Instagram scrapers
2. Fetch schema → See multiple input options (hashtags, urls, usernames)
3. **Ask:** "Should I search by hashtag (#cats) or specific user account?"
4. User responds: "hashtag"
5. Auto-configure: `{"hashtags": ["cats"], "resultsLimit": 50}`
6. Ask mode → User chooses "Save to file"
7. Ask format → User chooses "csv"
8. Ask location → User provides "./instagram_cats.csv"
9. Execute `call-actor` → Extract `datasetId` and `runId`
10. Download with curl: `curl "https://api.apify.com/v2/datasets/{datasetId}/items?format=csv" -o "./instagram_cats.csv"`
11. Use `get-actor-run(runId)` to get usage stats
12. Calculate cost and report: **"✅ Scraped 50 posts in 32s. Cost: $0.025"**
13. Confirm: "File saved to ./instagram_cats.csv"

---

## Example 3: Large Dataset (API Mode)

**User request:** "Get all products from this Amazon search URL"

**Workflow:**
1. Search actors → Find `junglee/amazon-crawler`
2. Fetch schema → Understand `startUrls` field and pricing
3. Auto-configure: `{"startUrls": [user_url], "maxItems": 1000}`
4. Detect large dataset → **Suggest API mode upfront**
5. User confirms
6. Ask format → User chooses "json"
7. Ask location → User provides "./amazon_products.json"
8. Execute `call-actor` → Extract `datasetId` from response metadata (don't read preview!)
9. Download with curl: `curl "https://api.apify.com/v2/datasets/{datasetId}/items?format=json" -o "./amazon_products.json"`
10. Use `get-actor-run(runId)` to get usage stats
11. Calculate cost and report: **"✅ Scraped 1000 products in 4m 23s. Cost: $1.50"**
12. Confirm save and summarize file info (file size, record count)

---

## Example 4: Handling Token Limit (API Mode - CORRECT)

**User request:** "Scrape NASA LinkedIn, save to disk as HTML"

**Workflow:**
1-5. [Actor selection and configuration steps]
6. User chooses API mode
7. Format: html
8. Location: ./nasa_linkedin_posts.html
9. Execute `call-actor` with `maxPosts: 100`
10. **Response arrives but exceeds 25K tokens** ⚠️
11. ✅ **CORRECT:** Extract `datasetId` from response metadata (e.g., "NDOvgUpViXsRKy701")
12. ✅ Download: `curl "https://api.apify.com/v2/datasets/NDOvgUpViXsRKy701/items?format=html" -o "nasa_linkedin_posts.html"`
13. ✅ Use `get-actor-run(runId)` to get usage stats
14. ✅ Report: **"✅ Scraped 100 posts in 2m 15s. Cost: $0.15"**
15. ✅ Confirm: "Saved 100 posts to nasa_linkedin_posts.html"

**❌ WRONG approach:**
- Do NOT re-run with `maxPosts: 10`
- The Actor already succeeded with 100 posts
- Re-running wastes money and gives incomplete data

---

## Example 5: Token Limit Fallback (MCP → API)

**User request:** "Get recent tweets from @NASA"

**Workflow:**
1. User chooses MCP mode (load into chat)
2. Execute `call-actor` with `maxItems: 100`
3. **Response exceeds 25K tokens** ⚠️
4. ✅ **CORRECT:** Inform user: "The dataset is too large for in-context loading. I'll save it to a file instead."
5. Ask for format and file location
6. User: "json", "./nasa_tweets.json"
7. Extract `datasetId` from the error response metadata
8. **If `datasetId` not available:** Use `get-actor-run-list(desc=true, limit=1)` to get most recent run
9. Download: `curl "https://api.apify.com/v2/datasets/{datasetId}/items?format=json" -o "./nasa_tweets.json"`
10. Use `get-actor-run(runId)` to get usage stats
11. Report: **"✅ Scraped 100 tweets in 38s. Cost: $0.02"**
12. Confirm: "File saved to ./nasa_tweets.json"

**Critical:** Never re-run the Actor - it already succeeded!

---

## Example 6: Clarification for Ambiguous Parameters

**User request:** "Get Instagram posts"

**Workflow:**
1. Find `apify/instagram-scraper`
2. Fetch schema → Multiple input methods available
3. **Ask:** "Which Instagram account should I scrape? Please provide the username or URL."
4. User responds: "nasa"
5. Auto-configure: `{"usernames": ["nasa"], "resultsLimit": 50}`
6. Continue with mode selection...

---

## Example 7: Twitter Search vs Handles

**User request:** "Scrape Twitter for web scraping content"

**Workflow:**
1. Find `xtdata/twitter-x-scraper`
2. Fetch schema → See both `searchTerms` and `twitterHandles` fields
3. **Ask:** "Should I search by:
   - Search terms (finds tweets containing keywords)
   - Twitter handles (finds tweets from specific users)
   - URLs (scrapes specific tweet or profile URLs)"
4. User responds: "Search terms"
5. Auto-configure: `{"searchTerms": ["web scraping"], "maxItems": 50, "sort": "Latest"}`
6. Continue with mode selection...

---

## Example 8: Parameter Resolution with RAG Web Browser

**User request:** "I wanna scrape nasa page from linkedin"

**Agent response:** "Reading Rigos' Apify scraper skill..."

**Workflow:**
1. Recognize ambiguous parameter: "nasa page from linkedin" (no specific URL)
2. **Proactively use RAG:** "I'll use RAG Web Browser to find NASA's LinkedIn URL first."
3. Use RAG Web Browser: Search for "NASA official LinkedIn company page"
4. Extract URL from results: `https://www.linkedin.com/company/nasa/`
5. Find LinkedIn scraper: `voyager/linkedin-profile-scraper`
6. Configure input: `{"profileUrls": ["https://www.linkedin.com/company/nasa/"], "maxResults": 50}`
7. Ask mode → User chooses "Save to file"
8. Ask format → User chooses "json"
9. Execute and download data
10. Report: **"✅ Scraped 50 posts in 1m 30s. Cost: $0.05"**

**Note:** Agent doesn't ask permission first - it proactively uses RAG because user likely doesn't know the exact URL.

---

## Example 9: Finding Account Handles with RAG

**User request:** "Get posts from Elon Musk on Instagram"

**Workflow:**
1. Recognize uncertainty: User didn't provide Instagram handle
2. **Ask first:** "Do you know Elon Musk's Instagram username?"
3. User responds: "No, can you find it?"
4. **Use RAG Web Browser:** "I'll use RAG Web Browser to find his Instagram account."
5. Search: "Elon Musk official Instagram account"
6. Extract username from results: `@elonmusk`
7. Find Instagram scraper: `apify/instagram-scraper`
8. Configure: `{"usernames": ["elonmusk"], "resultsLimit": 50}`
9. Continue with mode selection and execution...
10. Report: **"✅ Scraped 50 posts in 42s. Cost: $0.025"**

---

## Example 10: General Error Recovery

**User request:** "Scrape Amazon products"

**Workflow:**
1-5. [Configuration steps]
6. Execute `call-actor` with configured input
7. **❌ call-actor returns an error or unexpected response**
8. ✅ **FIRST: Check run list** - `get-actor-run-list(desc=true, limit=1)`
9. ✅ Inspect most recent run:
   - `status: "SUCCEEDED"` ← Actor actually completed!
   - `datasetId: "abc123"`
   - `computeUnits: 0.5`
10. ✅ Continue with data retrieval using the datasetId
11. ✅ Report: **"✅ Scraped 150 products in 1m 12s. Cost: $0.75"**

**Key principle:** When ANY error occurs with call-actor, always check the run list first. The Actor may have succeeded even if the tool response indicates failure.

---

## Cost Reporting Examples

**After every Actor run, report cost using this format:**

```
✅ Scraped 50 tweets in 22s. Cost: $0.01
```

```
✅ Scraped 200 Instagram posts in 1m 45s. Cost: $0.10
File saved to ./instagram_data.csv
```

```
✅ Scraped 1500 products in 8m 12s. Cost: $2.25
File saved to ./amazon_products.json (45.2 MB, 1500 records)
```

**How to calculate cost:**
1. Use `get-actor-run(runId)` after Actor completes
2. Extract `computeUnits` from response
3. Use pricing info from `fetch-actor-details` (step="info")
4. Calculate: `cost = computeUnits × pricePerComputeUnit`
5. Format duration in human-readable format (Xs, Xm Ys, Xh Ym)
