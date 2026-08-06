---
name: morphed-generate
description: Create AI images or videos in Morphed. Use when the user asks to generate, edit, animate, or iterate on visual media with their Morphed workspace and credits.
---

# Morphed Generate

Use Morphed's current model catalog and credit balance to queue generation jobs safely.

## Workflow

1. Call `get_workspace_context` and reuse relevant brand, product, character, and project context instead of asking for information Morphed already knows.
2. Call `list_models` for the requested media type. Never invent a model ID, capability, duration, resolution, aspect ratio, or credit price.
3. Resolve missing creative details from the request: subject, setting, composition, style, lighting, aspect ratio, and motion. Keep supplied references and brand constraints intact.
4. Call `estimate_generation` with the intended settings. Explain the model, exact credit cost, and insufficient balance before generating.
5. Reference media must already have a public HTTPS URL. If the user only has a local file or connector attachment, explain that direct MCP ingestion is not yet available.
6. Create a stable unique `idempotency_key`. Reuse that exact key if the same tool call is retried.
7. Call `generate_image` or `generate_video`, passing `project_id` when the work belongs to a saved project. Treat the returned job ID as queued work, not a completed asset.
8. Call `get_generation` when the user asks for progress or when the host supports waiting. Report the real status and output URL; do not claim completion early.

## Iteration

- For a variation, preserve the user's locked details and change only the requested dimension.
- For image-to-video, use the selected image URL as `input_image_url` and choose a model that explicitly supports image input.
- For reference-based work, pass only URLs the user supplied or assets returned by Morphed.
- If a tool rejects an input, refresh `list_models` and correct the request. Do not silently switch models.

## Safety

- Generation spends the authenticated user's credits. Do not hide that or fabricate discounts, bonus credits, or guarantees.
- Do not expose access tokens, internal provider URLs, or data from another workspace.
