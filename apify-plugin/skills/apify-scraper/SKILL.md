---
name: apify-scraper
description: Intelligent web scraping using Apify Actors with automatic input handling and dual-mode data retrieval (MCP or API). Use when users request scraping websites, extracting data from social media, e-commerce, or any web source.
---

# Apify Scraper Skill

## Purpose

Provide intelligent web scraping capabilities using the Apify platform. Handle Actor selection, input configuration, execution, and data retrieval with minimal user friction. Support both MCP-based (direct context) and API-based (file export) workflows.

## When to Use

Use this skill when:
- User requests scraping a website or extracting data
- User mentions specific platforms (Twitter/X, Instagram, LinkedIn, e-commerce, etc.)
- User wants to collect data, posts, profiles, products, or structured information from the web
- User provides a URL or search query to scrape

## Skill Announcement

**At the start of every response when using this skill, briefly announce skill usage to the user.**

Example announcements:
- "Reading Rigos' Apify scraper skill..."
- "Using Rigos' Apify scraper skill"
- "[Rigos' Apify scraper skill]"

Keep it short (5-10 words max). This helps the user know the skill is being used correctly.

## Core Workflow

### 1. Understand Request
Analyze the user's request to determine:
- **Target**: Website/platform to scrape (e.g., Twitter, Instagram, generic URL)
- **Data type**: What to extract (tweets, profiles, products, articles)
- **Parameters**: Requirements (username, search terms, date ranges, limits)

### 2. Find Actor
Use `search-actors` to find suitable Actors. Selection criteria:
- High success rate (>95%)
- Good ratings (>4.0 stars)
- Reasonable pricing
- Active maintenance (high monthly users)

For well-known platforms, prioritize dedicated scrapers (e.g., `xtdata/twitter-x-scraper` for Twitter).

See `references/popular-actors.md` for quick reference of common Actors.

### 3. Fetch Schema
Use `call-actor` with `step="info"` to get:
- Input schema with all available fields
- Actor documentation
- **Pricing information** (needed for cost reporting)

### 4. Configure Input

**Parameter Resolution Strategy:**

**For URLs, account handles, or usernames:**
- User often won't know exact URLs or handles
- **Proactively suggest using RAG Web Browser** to find them
- Don't ask user for information they likely don't have

**Use RAG Web Browser (`apify/rag-web-browser`) to find:**
- Account URLs (e.g., "NASA's LinkedIn page", "SpaceX Twitter account")
- Profile links (e.g., "Elon Musk's Instagram handle")
- Company pages (e.g., "OpenAI's company page")
- Specific usernames when user only provides a name

**Example RAG resolution:**
```
User: "I wanna scrape nasa page from linkedin"
→ Agent: "I'll use RAG Web Browser to find NASA's LinkedIn URL first."
→ Use RAG to search: "NASA official LinkedIn company page"
→ Extract URL from results
→ Use URL with LinkedIn scraper
```

**For scraping parameters (maxItems, filters, etc.):**
- Ask user for clarification when ambiguous
- Use sensible defaults when not specified
- Only ask about parameters the user would reasonably know

**Auto-fill rules:**
- URLs/handles: Use RAG to find (don't ask user)
- `maxItems` / `resultsLimit`: Ask if ambiguous, default to 50
- Filters: Only fill if explicitly mentioned
- Required fields: Ask user if not obvious from context
- Optional fields: Skip unless clearly relevant

See `references/common-scraper-fields.md` for field patterns and defaults.

### 5. Choose Retrieval Mode
Ask user to choose between:

**Mode 1: MCP Retrieval (In-Context)**
- Data loaded directly into conversation context
- Suitable for small to medium datasets (up to ~100 items)
- Token limit: 25,000 tokens for tool response

**Mode 2: API Retrieval (File Export)**
- Data saved to file on disk
- Suitable for large datasets
- Supports formats: JSON, CSV, Excel, XML, HTML, RSS
- Ask user: format and file location

**Decision prompt:**
```
How would you like to retrieve the scraped data?

1. Load into chat - Data appears in conversation (good for <100 items)
2. Save to file - Export to disk (good for large datasets)

Which option do you prefer?
```

### 6. Execute Based on Mode

#### Mode 1: MCP Retrieval
1. Use `call-actor` with `step="call"` and configured input
2. Extract `datasetId` and `runId` from response
3. If preview data is sufficient, present it to user
4. If user needs specific fields or more data, use `get-actor-output` with:
   - `fields`: Comma-separated list of relevant fields
   - `limit`: Appropriate limit (default 50-100)

**If MCP response exceeds token limit:**
- DO NOT re-run the Actor with fewer items
- The run already completed successfully
- Switch to API retrieval workflow (see Mode 2, step 2-4)

#### Mode 2: API Retrieval
1. Use `call-actor` with `step="call"` and configured input
2. Extract `datasetId` from response metadata WITHOUT reading preview items
   - Response includes: `{"datasetId": "xxx", "id": "runId", "status": "SUCCEEDED", ...}`
   - **DO NOT attempt to read preview items** - they cause token errors for large datasets
3. Construct API URL: `https://api.apify.com/v2/datasets/{datasetId}/items?format={format}`
4. Use `Bash` with `curl` to fetch data:
   ```bash
   curl "https://api.apify.com/v2/datasets/{datasetId}/items?format={format}" -o "{output_path}"
   ```
5. Confirm file saved successfully

**Critical:** In API mode, workflow is:
- Run Actor → Get datasetId → Download via curl
- **NEVER** re-run the Actor if token limit error occurs

### 7. Report Cost
After each Actor run:
1. Use `get-actor-run(runId)` to fetch run metadata
2. Extract usage stats: `computeUnits`, `duration`, `status`
3. Calculate cost using pricing from `fetch-actor-details`
4. Report to user: **"✅ Scraped X items in Ys. Cost: $Z"**

**Example:**
```
✅ Scraped 100 posts in 45s. Cost: $0.02
File saved to ./instagram_travel.csv
```

### 8. Present Results

**For MCP mode:**
- Summarize key findings from data
- Present relevant statistics (count, date range, top items)
- Offer to filter, analyze, or export data

**For API mode:**
- Confirm file location and format
- Provide file size and record count if available
- Offer to read and analyze sample of data

## Error Handling

### General Rule: When call-actor Fails (Any Reason)

**If `call-actor` fails, has errors, or returns unexpected results:**
1. **FIRST: Check the run list** - Use `get-actor-run-list(desc=true, limit=1)` to get the most recent run
2. **Inspect run status** - Check if Actor actually ran despite the error:
   - Status `SUCCEEDED`: Actor completed successfully, just extract `datasetId` and continue
   - Status `RUNNING`: Wait or check again after a moment
   - Status `FAILED`: Actor actually failed, see recovery steps below
3. **If run succeeded:** Extract `datasetId` from run metadata and continue with data retrieval
4. **If run failed:** Provide clear error message and suggest alternatives

**Common failure scenarios:**

**Token Limit Exceeded (Response too large):**
- Actor succeeded, just response was too large for MCP
- Extract `datasetId` from error response metadata OR use `get-actor-run-list`
- Continue with curl download
- **NEVER re-run the Actor** - it already succeeded and consumed resources

**Actual Actor Failure:**
- Check run status using `get-actor-run(runId)` or `get-actor-run-list`
- Provide clear error message from run metadata
- Suggest alternatives (different Actor, adjusted input)
- Only re-run if Actor actually failed, not if response was too large

**Missing datasetId:**
- Use `get-actor-run-list(desc=true, limit=1)` to find most recent run
- Extract `datasetId` from run metadata
- Continue with data retrieval

### Missing Required Fields
- Never guess values
- Always ask user for clarification
- Provide clear explanation of what the field does

**Critical principle:** Always check the run list when things go wrong. The Actor may have succeeded even if the tool response indicates failure.

## Best Practices

1. **Proactive mode selection**: If user mentions "download" or "save", default to API mode
2. **Respect token limits**: For >100 items, suggest API mode upfront
3. **Field selection**: When using `get-actor-output`, only request relevant fields
4. **Cost transparency**: Always report cost after runs
5. **Privacy**: Remind users about scraping ToS when relevant

## References

- `references/common-scraper-fields.md` - Field patterns and auto-fill logic
- `references/popular-actors.md` - Quick reference for frequently used Actors
- `references/examples.md` - Complete workflow examples

See these files for detailed information on field configuration, Actor selection, and example scenarios.
