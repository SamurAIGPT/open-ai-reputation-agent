# AI Reputation Agent

An AI agent for brand reputation — news monitoring, social sentiment tracking, review mining, and PR response drafting — backed by real news, social, and review-data APIs.

Part of [Agency Agents OS](https://github.com/Anil-matcha/agency-agents-os), an open ecosystem of specialized AI agents for real business work.

## What this covers

This repo is the umbrella for anything an agency or in-house team would call "the AI reputation agent": watching news, social, and review channels for brand mentions, surfacing sentiment shifts and reputation risks, and drafting (never publishing) the response when something needs one.

## Sub-agents

| Agent | Does | Status |
|---|---|---|
| [News Monitoring](agents/news-monitoring/SKILL.md) | Tracks news and press mentions of a brand and flags anything requiring a response | Coming Soon |
| [Social Sentiment](agents/social-sentiment/SKILL.md) | Tracks sentiment trends about a brand across social platforms over time | Coming Soon |
| [Review Mining](agents/review-mining/SKILL.md) | Aggregates and summarizes themes from reviews (Amazon, Google, app stores) to flag reputation risks | Coming Soon |
| [PR & Communications](agents/pr-communications/SKILL.md) | Drafts response statements and talking points for a flagged reputation event, for human review before publishing | Coming Soon |

## Required Muapi APIs

- `reputation.news_search` — search and monitor news/press coverage for brand mentions.
- `social.sentiment_analysis` — sentiment scoring and trend tracking across social platforms.
- `reputation.review_search` — search and aggregate reviews across review platforms.

See each sub-agent's `SKILL.md` for the specific capabilities it uses.

## Setup

1. Create a Muapi account and API key at [muapi.ai](https://muapi.ai).
2. Review the [Muapi API quickstart](https://muapi.ai) and [OpenAPI schema](https://api.muapi.ai/openapi.json) for the reputation, social, and review endpoints.
3. Load the `SKILL.md` for the sub-agent you need into your agent runtime (hosted agent, MCP client, or custom LLM app), or follow it manually.


## Using with an AI agent

Every sub-agent's `SKILL.md` is model- and runtime-agnostic — it's plain Markdown, so it works with any LLM agent, not just Claude. Two integration paths:

**As an MCP connection (the agent gets live Muapi tools):**

Muapi runs an MCP server at `https://api.muapi.ai/mcp` that any MCP-compatible client can connect to — Cursor, Windsurf, Claude, or your own custom agent.

- **Cursor / Windsurf / other clients with a header field:** connect to `https://api.muapi.ai/mcp` with an `Authorization: Bearer YOUR_MUAPI_KEY` header.
- **claude.ai / Claude Cowork / other connector UIs with no header field:** use the URL-embedded key form instead, `https://api.muapi.ai/mcp/YOUR_MUAPI_KEY`, via Settings → Connectors → Add custom connector.
- **Claude Code / Claude Desktop:** `claude mcp add muapi -e MUAPI_API_KEY=YOUR_MUAPI_KEY -- muapi mcp serve` (uses the muapi CLI's stdio transport — Claude Code's HTTP MCP client doesn't reliably inject tools).

Full setup details for every client: [muapi.ai/docs/mcp](https://muapi.ai/docs/mcp).

**As agent instructions (any LLM follows the workflow directly):**

Drop a sub-agent's `SKILL.md` into a Claude Code project's `.claude/skills/` directory, paste it into a custom-GPT/Project's system instructions, hand it to an autonomous agent framework as a tool spec, or attach it directly in a chat conversation — then ask the agent to follow it.

## Read-only vs. write actions

News monitoring, social sentiment, and review mining are `read-only` — they observe and summarize, never post or reply anywhere. PR & Communications is `draft-only`: it produces a statement or talking points as text for review. Publishing any statement is `requires-approval-to-publish` — no sub-agent in this repo sends, posts, or publishes on its own; a human signs off first.

## Status and limitations

All four sub-agents are Coming Soon. They depend on news-search, social-sentiment, and review-data capabilities that are not yet live on Muapi. Once those capabilities ship, each `SKILL.md` will be updated from Blueprint/Coming Soon to a working spec.

## Contributing

See [Agency Agents OS CONTRIBUTING.md](https://github.com/Anil-matcha/agency-agents-os/blob/main/CONTRIBUTING.md).

## License

[MIT](LICENSE)
