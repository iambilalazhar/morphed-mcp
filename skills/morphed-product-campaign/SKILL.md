---
name: morphed-product-campaign
description: Build a coherent product image and video campaign in Morphed. Use for launch assets, ads, social variants, product photography, or a campaign system that must preserve the same product and visual direction.
---

# Morphed Product Campaign

Turn a product brief into a small, coherent campaign without losing product identity between assets.

## Brief

Extract or ask for only information that materially changes the output:

- product and reference image URLs
- audience and desired action
- offer or approved message
- channels and required aspect ratios
- brand colors, art direction, and non-negotiable product details
- number of final images and videos

Do not invent testimonials, performance claims, prices, discounts, guarantees, or bonus offers.

## Campaign workflow

1. Call `get_workspace_context`. Reuse saved products, brand assets, characters, and an existing relevant project.
2. If no relevant project exists, call `create_project` with a clear campaign name. Use its ID for every generation in this campaign.
3. Call `list_models`, then `estimate_generation` for the complete planned asset set. Surface the expected spend before generation.
4. Define one campaign spine: product truth, audience, promise, visual world, and repeated motifs.
5. Plan the smallest useful asset set: a hero visual, product-detail or benefit image, contextual image, and one short motion concept derived from an approved image.
6. Generate image directions first with the campaign `project_id`. Use reference-image-capable models when product fidelity matters.
7. Show completed outputs and let the user select a direction before spending credits on video, unless they explicitly requested an autonomous full run.
8. Animate the selected frame with `generate_video`; preserve the product, composition anchors, and campaign motifs.
9. Use stable, distinct idempotency keys per planned asset. Poll each returned job with `get_generation`.
10. Deliver an asset manifest with the project ID, job IDs, output URLs, aspect ratios, channel roles, total credits spent, and any failed or pending jobs.

## Consistency rules

- Repeat concrete camera, lighting, palette, texture, environment, and product-placement constraints.
- Prefer variations of approved outputs to unrelated restarts.
- Never claim a pending job is complete.
- Never silently substitute a model when fidelity or price changes.
