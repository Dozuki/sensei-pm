# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. For example, `~~project tracker` might mean Linear, Asana, Jira, or any other tracker with an MCP server.

Plugins are **tool-agnostic** — they describe workflows in terms of categories (project tracker, design, product analytics, etc.) rather than specific products. The `.mcp.json` pre-configures specific MCP servers, but any MCP server in that category works.

## Connectors for this plugin

| Category | Placeholder | Included servers | Other options |
|----------|-------------|-----------------|---------------|
| Calendar | `~~calendar` | Google Calendar | Microsoft 365 |
| Chat | `~~chat` | Slack | Microsoft Teams |
| Design | `~~design` | Figma | Sketch, Adobe XD |
| Email | `~~email` | Gmail | Microsoft 365 |
| Knowledge base | `~~knowledge base` | Notion | Confluence, Guru, Coda |
| Customer call transcription | `~~customer call transcription` | Gong | Dovetail, Otter.ai |
| Internal meeting transcription | `~~internal meeting transcription` | Granola, Notion | Gong, Dovetail, Otter.ai |
| Product analytics | `~~product analytics` | Pendo | Mixpanel, Heap, FullStory |
| Project tracker | `~~project tracker` | Atlassian (Jira) | Shortcut, Basecamp |
| User feedback | `~~user feedback` | Productboard | Canny, UserVoice |