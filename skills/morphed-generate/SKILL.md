---
name: morphed-generate
description: Create AI images or videos in Morphed. Use when the user asks to generate, edit, animate, or iterate on visual media with their Morphed workspace and credits.
---

# Morphed Generate

Use Morphed's current model catalog and credit balance to queue generation jobs safely.

## Workflow

1. Call `list_models` for the requested media type. Never invent a model ID, capability, duration, resolution, aspect ratio, or credit price.
2. Call `get_credits`. If the requested work may exceed the balance, explain that before generating.
3. Resolve missing creative details from the request: subject, setting, composition, style, lighting, aspect ratio, and motion. Keep supplied references and brand constraints intact.
4. Select the simplest available model that satisfies the request. State the model and applicable credit price before an expensive or multi-output run.
5. Create a stable unique `idempotency_key`. Reuse that exact key if the same tool call is retried.
6. Call `generate_image` or `generate_video`. Treat the returned job ID as queued work, not a completed asset.
7. Call `get_generation` when the user asks for progress or when the host supports waiting. Report the real status and output URL; do not claim completion early.

## Iteration

- For a variation, preserve the user's locked details and change only the requested dimension.
- For image-to-video, use the selected image URL as `input_image_url` and choose a model that explicitly supports image input.
- For reference-based work, pass only URLs the user supplied or assets returned by Morphed.
- If a tool rejects an input, refresh `list_models` and correct the request. Do not silently switch models.

## Safety

- Generation spends the authenticated user's credits. Do not hide that or fabricate discounts, bonus credits, or guarantees.
- Do not expose access tokens, internal provider URLs, or data from another workspace.
