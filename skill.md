# Real-Time Google Rank Checker

## Purpose

Check the **current Google organic ranking** of a target domain for a user-provided list of keywords using live browser/Chrome access.

The skill must inspect the actual Google search results for every supplied keyword and record the **exact organic position and Ranking URL**.

Never estimate rankings or substitute historical, third-party, or estimated ranking data.

---

## Required Inputs

Collect the following before starting:

* **Target domain**
* **Country / location**
* **Language**
* **Device** — Desktop or Mobile
* **Keywords**
* **Ranking depth** — for example Top 10, Top 50, or Top 100

If country/location, language, device, or ranking depth is missing, ask the user before starting.

### Keyword Limit

There is **no keyword limit**.

The user may provide:

* 10 keywords
* 50 keywords
* 100 keywords
* 500 keywords
* 1,000+ keywords

For large lists, process keywords in manageable batches internally, but always produce **one consolidated final CSV**.

---

## Workflow

For **every supplied keyword**:

1. Open Google using browser/Chrome access.
2. Search the **exact keyword**.
3. Use the specified:

   * Country/location
   * Language
   * Device
4. Inspect the live Google search results.
5. Identify the first organic result belonging to the target domain.
6. Record the actual organic position.
7. Record the **exact Ranking URL** shown in Google.
8. Ignore paid advertisements.
9. Do not count non-organic SERP features as organic positions.
10. If the target domain is not found within the specified ranking depth, record the appropriate not-ranking result.
11. If the result cannot be reliably inspected, record **Unable to Verify**.
12. Never estimate a ranking.
13. Never use historical ranking data.
14. Never use Ahrefs, Semrush, Google Search Console, or other third-party ranking data as a substitute.
15. Check **every supplied keyword**.

---

## Organic Ranking Rules

Only standard organic web results count toward the ranking position.

Do **not** count:

* Paid advertisements
* AI Overviews
* Featured Snippets
* Local Packs / Maps
* People Also Ask
* Videos
* Images
* Shopping results
* Knowledge Panels
* Other SERP features

Example:

```text
AI Overview              → Not counted
Sponsored Result        → Not counted
Featured Snippet        → Not counted

Organic Result #1       → Position 1
Organic Result #2       → Position 2
Organic Result #3       → Position 3

People Also Ask         → Not counted

Organic Result #4       → Position 4
```

If the target domain appears multiple times, record the **first organic result** belonging to that domain.

---

## Domain Matching

Match results against the supplied target domain.

Example target domain:

```text
example.com
```

Valid ranking URLs may include:

```text
https://example.com/
https://example.com/products/
https://example.com/products/product-a/
```

The Ranking URL must belong to the target domain.

Do not replace a ranking URL with the homepage.

Do not record a URL from another domain.

---

## Ranking URL

When the target domain ranks:

* Capture the **exact URL of the first organic result**.
* Preserve the actual ranking page URL.
* Do not substitute the homepage.
* Do not use a different URL from the same website.
* Do not infer the URL from the keyword or website structure.

The Ranking URL must be based on the live Google result that was actually inspected.

---

# Output

## Chat Summary

Keep the chat response to a **concise summary only**.

Do not display the complete keyword-by-keyword ranking table in chat.

Example:

```text
Google Rank Check Complete

Target Domain: example.com
Keywords Checked: 250

Top 3: 18
Top 10: 47
11–20: 39
21–50: 62
51–100: 41
Not in Top 100: 35
Unable to Verify: 8

Complete ranking results have been exported to CSV.
```

The summary must be calculated from the final ranking results.

Do not show the full ranking table in the chat response.

---

# CSV Output

Generate **one consolidated CSV file** containing exactly one row for every supplied keyword.

Use these columns only:

|  # | Keyword | Position | Ranking URL |
| -: | ------- | -------: | ----------- |

### Example

|  # | Keyword                   |         Position | Ranking URL                        |
| -: | ------------------------- | ---------------: | ---------------------------------- |
|  1 | medical alert system      |                3 | https://example.com/medical-alert/ |
|  2 | medical alert for seniors |               17 | https://example.com/senior-alert/  |
|  3 | best medical alert system |               64 | https://example.com/               |
|  4 | emergency alert system    |   Not in Top 100 |                                    |
|  5 | senior safety device      | Unable to Verify |                                    |

---

## CSV Rules

* There is **no keyword limit**.
* Process every keyword supplied by the user.
* Return exactly **one row for every supplied keyword**.
* Preserve each keyword exactly as supplied.
* Maintain the original keyword order.
* Do not add keywords.
* Do not remove keywords.
* Do not silently skip keywords.
* Record the first organic position where the target domain appears.
* Record the exact Ranking URL shown in Google.
* Ignore paid advertisements.
* Ignore non-organic SERP features when counting positions.
* If the target domain is not found within positions 1–100, write:
  **Not in Top 100**
* If the Google result cannot be reliably inspected, write:
  **Unable to Verify**
* Leave Ranking URL blank for:

  * `Not in Top 100`
  * `Unable to Verify`
* Never estimate a ranking.
* Never use historical ranking data.
* Never substitute third-party ranking data.

---

# Position Rules

Record the **actual organic position number**.

For example:

```text
Position: 3
Position: 7
Position: 18
Position: 46
Position: 87
```

Do not record categories such as:

```text
Top 10
Top 20
Top 50
```

The position field must contain the actual observed ranking number.

### Top 100

When checking Top 100:

* Position 1–100 → record the exact position
* Not found in positions 1–100 → `Not in Top 100`
* Result cannot be verified → `Unable to Verify`

If the user specifies a different ranking depth, follow that requested depth.

---

# Bulk Processing

There is **no keyword limit**.

For large keyword lists:

1. Divide the keywords into manageable internal batches.
2. Use the same search settings for every batch.
3. Check every supplied keyword.
4. Maintain the original keyword order.
5. Combine all results into **one consolidated CSV**.
6. Do not create separate CSV files for individual batches.
7. Do not ask the user to manually split the keyword list.

The final CSV must contain exactly one row for every supplied keyword.

---

# Quality Control

Before delivering the final CSV, verify:

1. CSV row count equals the number of supplied keywords.
2. Every supplied keyword was processed.
3. No keyword was silently skipped.
4. No keyword was added.
5. Keyword order is preserved.
6. Every reported position was observed in the live Google results.
7. Every Ranking URL belongs to the target domain.
8. Only organic results were counted.
9. Paid advertisements were excluded.
10. SERP features were excluded from organic position counting.
11. Keywords outside the checked depth are correctly marked.
12. Unverifiable results are marked `Unable to Verify`.
13. No ranking was estimated.
14. No historical ranking data was used.
15. No third-party ranking data was substituted.
16. Chat summary totals match the final CSV.

---

# Error Handling

### Google Search Blocked

If Google blocks the search or prevents reliable inspection:

```text
Unable to Verify
```

Do not guess or use another ranking source as a replacement.

### Timeout / Page Loading Failure

If the Google result cannot be reliably inspected:

```text
Unable to Verify
```

### Domain Not Found

If the target domain is not found within the requested ranking depth:

```text
Not in Top 100
```

when checking Top 100.

For another specified depth, use the equivalent:

```text
Not in Top [specified depth]
```

---

# Final Reporting

The final response must contain:

1. A concise ranking summary in chat.
2. The generated CSV file.

Do not reproduce the complete ranking dataset in chat.

The ranking results represent the **live Google search environment at the time of the check**.

Google rankings may vary based on:

* Location
* Language
* Device
* Personalization
* Search settings
* Google data centers
* Time of search

Only rankings that were actually observed and verified should be reported.
