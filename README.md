# Morphed for Claude

Generate AI images, videos, UGC-style ads, and full product campaigns without leaving Claude. Morphed connects Claude to your Morphed workspace, so it can reuse your saved brand, product, and character context, pick a fitting image or video model, show the exact credit cost up front, and keep every result organized in a project.

## What you can ask Claude

- "Make a square product shot of my serum on a marble counter in morning light."
- "Turn this image into a five-second vertical video with a slow push-in."
- "Plan and generate a launch campaign for our new sneaker: hero image, three social variants, and a short ad."
- "What will this cost in credits before you generate it?"

## What's included

- **Morphed MCP connector** (`https://api.morphed.app/mcp`): workspace context, model catalog, credit estimates, image and video generation, and job status.
- **`morphed-generate` skill**: image and video generation with cost checks and safe retries.
- **`morphed-product-campaign` skill**: coherent campaign asset sets that keep the same product and visual direction across every asset.

## How it works and what it sends

The plugin talks only to Morphed's remote MCP server at `api.morphed.app`. You sign in with Morphed OAuth and approve read and generation access for your own workspace. Prompts, settings, and any reference image URLs you provide are sent to Morphed to create your media. Generation spends your Morphed credits, and Claude shows the cost before it generates. No API key is stored in this repository.

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

Add the public Morphed marketplace and install the plugin:

```sh
claude plugin marketplace add iambilalazhar/morphed-mcp
claude plugin install morphed@morphed
```

In Claude Cowork, open **Customize → Plugins → Add marketplace** and enter
`https://github.com/iambilalazhar/morphed-mcp`.

For one-session development from a local clone:

```sh
claude --plugin-dir ./morphed-mcp
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

- Website: https://morphed.app
- Documentation: https://morphed.app/mcp
- Support: https://morphed.app/support
- Privacy: https://morphed.app/privacy-policy
- Terms: https://morphed.app/tos

## Requirements

- The production web and API deployments must expose Morphed's OAuth discovery, authorization, token, JWKS, and MCP endpoints.
- The user must sign in to Morphed and approve the requested read and generation scopes.
- Generation tools spend the user's Morphed credits.
