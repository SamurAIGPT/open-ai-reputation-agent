# Mine Google Business Reviews for Recurring Themes

This walkthrough summarizes Google Business Profile reviews using the live review-search scope documented by the [Review Mining skill](../agents/review-mining/SKILL.md). Other review sources, including Amazon and app stores, are not implied by this guide.

## Example request

> Summarize recurring complaints in our Google reviews and tell me whether any theme appears more often in the newer period.

## Workflow

1. Confirm the exact business/listing, date range, comparison periods, and whether positive themes should be included. Verify the listing identity before pulling data.
2. Check that the live Google review capability is available and read its current schema. Record the request, filters, timestamp, and number of reviews returned.
3. Preserve the source review and date for each item. Deduplicate only exact/repeated records; do not collapse different customers' reports into one review.
4. Group text into themes. Require repeated independent reviews before describing a theme as recurring; report isolated comments as individual observations. Keep direct quotes short and linked to their review when available.
5. Compare periods only when both pulls use the same listing, source, filters, and comparable date windows. State counts and sample sizes. Without comparable prior data, describe themes in the current sample without claiming they are rising or falling.
6. Flag safety, billing, privacy, or service issues for human review with the source evidence. Give recommendations as suggestions only.
7. Return a concise risk-first summary, theme table, sample counts, representative evidence, scope, and limitations.

## Report template

| Theme | Review count | Period comparison | Evidence | Suggested follow-up |
|---|---:|---|---|---|
| Use only a theme supported by the retrieved reviews | Count from the returned sample | Comparable / not comparable | Review links or short excerpts | Human-review suggestion |

## Coverage and response boundaries

The documented live scope is Google Business Profile reviews via `reputation.review_search` (backed by Muapi's `seo-business-reviews` endpoint). If the user asks for Amazon, app-store, or other platform reviews, report that coverage gap or ask for an export. This workflow never replies to reviews, edits a listing, or contacts a reviewer; draft any public response only through the separate PR workflow and with human review.
