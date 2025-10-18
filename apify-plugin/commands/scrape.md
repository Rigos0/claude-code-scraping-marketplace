---
description: Quick command to scrape a website using Apify
---

# Scrape Website

ARGUMENTS: {{ARGUMENTS}}

Use the apify-scraper skill to intelligently handle web scraping requests.

The skill will:
1. Analyze the scraping request from ARGUMENTS
2. Find and select the appropriate Apify Actor
3. Intelligently configure input fields (only auto-fill obvious ones, ask for clarification when needed)
4. Ask user to choose between MCP retrieval (load into chat) or API retrieval (save to file)
5. Execute the scraping and present results

Invoke the skill by using the Skill tool with command "apify-plugin:apify-scraper".