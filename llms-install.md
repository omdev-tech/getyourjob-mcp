# Installing the GetYourJob MCP server

GetYourJob is a hosted remote MCP server. There is nothing to clone, build or run.

1. Add this entry to the MCP settings file (for Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "getyourjob": {
      "type": "streamableHttp",
      "url": "https://getyourjob.pro/api/mcp"
    }
  }
}
```

2. On first use the server answers 401 and the client starts the OAuth flow: the user signs in
   with their GetYourJob account in the browser. A free account can be created at
   https://getyourjob.pro/auth/register.

3. If the client cannot complete OAuth, ask the user to create an API key at
   https://getyourjob.pro/profile/developer/mcp and add it as a header:

```json
"headers": { "Authorization": "Bearer <the user's API key>" }
```

Never invent or hardcode a key. Verify the setup by calling the `get_auth_status` tool.
