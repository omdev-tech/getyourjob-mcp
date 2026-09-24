<p align="center"><img src="logo.png" width="96" alt="GetYourJob"></p>

# GetYourJob MCP server

Official [Model Context Protocol](https://modelcontextprotocol.io) server for
[GetYourJob](https://getyourjob.pro), the IT job platform for France. Connect it to Claude,
ChatGPT, Gemini CLI, Cursor, VS Code, Cline or any MCP client to:

- **search** IT job and freelance mission offers (technology, role, city, remote, contract, seniority), with pay positioned against the market;
- **run AI matching** between your profile and active offers, with the score breakdown;
- **track applications**: save offers, update their status, review your pipeline;
- **write** a cover letter or an action plan tailored to one offer.

It is a hosted (remote) server: nothing to install or run locally.

| | |
|---|---|
| Endpoint | `https://getyourjob.pro/api/mcp` |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 (dynamic client registration, PKCE) - or an API key |
| Docs | https://getyourjob.pro/mcp |
| MCP Registry | `pro.getyourjob/getyourjob` |

You need a free GetYourJob account: https://getyourjob.pro/auth/register

## Connect

**Claude (claude.ai / Desktop)** - Settings > Connectors > Add custom connector, paste the
endpoint, then sign in with your GetYourJob account.

**ChatGPT** - Settings > Apps & Connectors > Advanced settings > enable developer mode, create a
connector with the endpoint and OAuth authentication.

**Claude Code**

```bash
claude mcp add --transport http getyourjob https://getyourjob.pro/api/mcp
```

**Claude Code plugin** - the connector plus two skills (job search, application prep):

```bash
claude plugin marketplace add omdev-tech/getyourjob-mcp
claude plugin install getyourjob@getyourjob
```

**Gemini CLI** - install this repository as an extension:

```bash
gemini extensions install https://github.com/omdev-tech/getyourjob-mcp
```

or add the server directly: `gemini mcp add --transport http getyourjob https://getyourjob.pro/api/mcp`

**Cursor** (`~/.cursor/mcp.json`), **VS Code** and other clients:

```json
{
  "mcpServers": {
    "getyourjob": { "url": "https://getyourjob.pro/api/mcp" }
  }
}
```

**Clients without OAuth** - create an API key at https://getyourjob.pro/profile/developer/mcp and
send it as a header:

```json
{
  "mcpServers": {
    "getyourjob": {
      "url": "https://getyourjob.pro/api/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

## Tools

29 tools, each annotated as read-only or data-changing so clients ask before a change:
job search and details, company details, offer comparison, market insights, profile and skills,
personas, application pipeline, AI matching and quota, cover letters, action plans, CV analysis
and interview-training progress. The full list is on https://getyourjob.pro/mcp.

AI matching, cover letters and action plans follow the quotas of your GetYourJob plan.

## Try

- "Find me fully remote React offers in Paris."
- "Run AI matching on my profile."
- "Show me my ongoing applications."
- "Compare these 3 offers and tell me which one fits me best."

## Privacy & support

Privacy policy: https://getyourjob.pro/privacy - Support: https://getyourjob.pro/faq

---

**FR** - Serveur MCP officiel de GetYourJob : recherche d'offres et de missions IT en France,
matching IA, suivi de candidatures et lettres de motivation depuis votre assistant IA.
Guide d'installation : https://getyourjob.pro/mcp
