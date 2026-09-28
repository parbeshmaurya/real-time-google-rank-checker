A Claude Skill that checks live Google organic rankings for a target domain and a supplied list of keywords using browser/Chrome access.

It captures the actual organic position and exact Ranking URL for each keyword and exports the complete results to CSV.

**The user must provide:**

- Target domain
- Country/location
- Language
- Device
- Keywords
- Ranking depth

### Recommended Batch Size

For reliable browser processing, recommend **20 keywords per batch**.

For larger keyword lists, process them in multiple batches while
maintaining the complete keyword list and producing one consolidated
CSV when requested.

**How**

Provide:
Target domain
Country/location
Language
Device
Keywords
Ranking depth


The skill searches each keyword on Google, checks the organic results, identifies the first result from the target domain, records its position and URL, and consolidates all results into one CSV file.

Chat shows only a summary.

**Output**

# | Keyword | Position | Ranking URL

If the domain is not found within the top 100:
Not in Top 100

If the result cannot be verified:
Unable to Verify

**TC — Trust & Control**
Checks every supplied keyword
Uses live Google results only
Records exact organic position
Captures the exact Ranking URL
Ignores ads and SERP features
Never estimates rankings
Never uses historical ranking data
Never substitutes Ahrefs, Semrush, or GSC data
Maintains one CSV row per keyword
Reports only rankings that were actually verified

Benefits
Save time — automate manual Google rank checks
Scale easily — process large keyword lists
Improve accuracy — use observed live results
Track ranking URLs — know which page is ranking
Easy reporting — receive a structured CSV
Client-ready — useful for SEO audits and reporting
Actionable insights — identify ranking opportunities by keyword and page
