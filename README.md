# Morphed agent plugin

This plugin connects Claude Code or Codex to Morphed's remote MCP server and adds two reusable workflows:

- `morphed-generate` for image and video generation
- `morphed-product-campaign` for coherent campaign asset sets

The MCP server uses the authenticated user's Morphed workspace and credits.

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

## Claude.ai and ChatGPT

Add `https://api.morphed.app/mcp` as a custom connector. These hosted clients use the remote MCP server directly; they do not install the Claude Code or Codex plugin package.

## Requirements

- The production web and API deployments must expose Morphed's OAuth discovery, authorization, token, JWKS, and MCP endpoints.
- The user must sign in to Morphed and approve the requested read and generation scopes.
- Generation tools spend the user's Morphed credits.
