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

1. Call `list_models` and `get_credits`.
2. Define one campaign spine: product truth, audience, promise, visual world, and repeated motifs.
3. Plan the smallest useful asset set: a hero visual, product-detail or benefit image, contextual image, and one short motion concept derived from an approved image.
4. Generate image directions first. Use reference-image-capable models when product fidelity matters.
5. Show completed outputs and let the user select a direction before spending credits on video, unless they explicitly requested an autonomous full run.
6. Animate the selected frame with `generate_video`; preserve the product, composition anchors, and campaign motifs.
7. Use stable, distinct idempotency keys per planned asset. Poll each returned job with `get_generation`.
8. Deliver an asset manifest with job IDs, output URLs, aspect ratios, channel roles, and any failed or pending jobs.

## Consistency rules

- Repeat concrete camera, lighting, palette, texture, environment, and product-placement constraints.
- Prefer variations of approved outputs to unrelated restarts.
- Never claim a pending job is complete.
- Never silently substitute a model when fidelity or price changes.
