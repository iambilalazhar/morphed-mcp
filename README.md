# Morphed agent plugin

This open-source agent plugin connects Cursor, Claude Code, or Codex to Morphed's remote MCP server and adds two reusable workflows:

- `morphed-generate` for image and video generation
- `morphed-product-campaign` for coherent campaign asset sets

The MCP server uses the authenticated user's Morphed workspace and credits. Agents can reuse saved brand, product, character, and project context, estimate exact costs, and keep generations grouped in durable projects.

## Cursor

Install the plugin from Cursor Marketplace when the listing is approved, or add the remote MCP server directly:

```json
{
  "mcpServers": {
    "morphed": {
      "type": "streamable-http",
      "url": "https://api.morphed.app/mcp"
    }
  }
}
```

Cursor opens Morphed OAuth so each user authorizes their own workspace and credit balance. No API key belongs in this repository.

## Claude Code

From the Morphed repository:

```sh
claude plugin marketplace add .
claude plugin install morphed@morphed
```

For one-session development:

```sh
claude --plugin-dir ./plugins/morphed
```

## Codex

From the Morphed repository:

```sh
codex plugin marketplace add .
codex plugin add morphed@morphed
```

## Claude.ai and OpenAI

Add `https://api.morphed.app/mcp` as a custom connector. OpenAI also supports Morphed as an MCP-only Plugin; custom UI is optional. Hosted clients use the remote MCP server directly and do not install this repository.

## Links

- Website: https://morphed.app/mcp
- Support: https://morphed.app/support
- Privacy: https://morphed.app/privacy-policy
- Terms: https://morphed.app/tos

## Requirements

- The production web and API deployments must expose Morphed's OAuth discovery, authorization, token, JWKS, and MCP endpoints.
- The user must sign in to Morphed and approve the requested read and generation scopes.
- Generation tools spend the user's Morphed credits.
