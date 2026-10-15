---
name: scalable
description: "Use when creating or improving Amazon listing images or A+ content with Scalable. Not for generic image editing without Scalable, non-Amazon marketplaces, or Scalable app bugs and support."
user_invocable: true
version: 0.1.0
trust-level: confirm-then-execute
last-reviewed: "2026-10-14"
owner: matthias-scale
category: integration
---
# Scalable — Amazon listing images and A+ content

Use the `scalable` MCP tools for the product workflow. Follow the server session rules in [references/session-rules.md](references/session-rules.md) on every turn; they are generated from the MCP server source and are authoritative. This skill adds workflow guidance and never relaxes those rules.

## Workflow

1. **Product.** Start with `products list` and `product get` for an existing product. For an untracked Amazon product, `product create` accepts its ASIN or SKU and country, then submits it for analysis. This is a paid action: quote with `credits-quote` using `product-create`, explain the returned cost, and get explicit consent first. Product management is also in the Scalable app at **`/products/{id}`**; new products can be started from **`/studio`**.
2. **Brand kit.** Inspect `brand-kit list` and `brand-kit get`; adjust permitted details with `brand-kit update`. `brand-kit create` is paid, but `credits-quote` does not support it, so do not call it over MCP. Direct the user to **`/brand-kits`** to review the app's displayed cost and create the kit there; then continue with `brand-kit list` or `brand-kit get`. If the user wants the kit applied to the product, use `product set` with the returned kit ID and the advertised `brand-kit` and `use-brand-kit` fields; kit creation alone does not attach it.
3. **Brief.** Read the product settings and save product-wide or brand-wide creative rules with `product brief set`. State only values returned by the tool; empty strings clear a field. If the user wants copy for an existing strategy, use `product copy set` with that strategy's stable ID.
4. **Image set.** Inspect existing product images and analysis with `product get` and `product analysis get`. Upload user-provided references with `asset upload` attached to the product. Choose the requested Amazon image role and dimensions using the tool's supported fields; retain the product's Amazon-safe guardrail unless the user explicitly asks to change it.
5. **Generate or edit.** Use `generate` for a listing image from a product and strategy; `variation create` for a scene variation; `aplus strategy` then `aplus generate` for A+ content. Use `aplus generate-mobile` only when a mobile rendition is requested. For supported edits, use `edit erase`, `edit text`, or `edit change-format` on the source image handle. Before each paid action, call `credits-quote` with the matching action and count, explain the returned cost, and wait for explicit consent. `edit text enhance` has no matching `credits-quote` action; use the app's **`/studio/{productId}/listing`** to inspect its cost before editing there. Pass only advertised fields. Resume a returned job with `job wait` or its documented `jobId` continuation; do not resubmit a completed or pending write.
6. **Review.** Read the result, then use `image get` with `download: true` for each generated listing or edited image so its image content is available in chat. Display each with its session number, returned `image_type`, `width` × `height`, and authoritative `credits.charged` from the generation result. After a paid action, show `Credits: <charged> spent; <remaining> remaining.` using the returned `credits.charged` and `credits.remaining`; if either is absent or listed in `credits.unknowns`, say `unknown` rather than estimating. Keep a session ledger mapping image IDs to numbers: re-reading the same image keeps its number; each edited or regenerated image gets the next number and names its source number(s). A+ results are a known exception: `aplus generate` and `aplus list` return proxy paths and dimensions, while `image get` downloads only generated-image IDs. Do not present those paths as images or links; use `product-images-export` for the supported download links and tell the user that A+ inline display is unavailable in this server contract. The app product view is **`/products/{id}`**.
7. **Export.** For product image files or links, call `product-images-export`; it groups main, listing, A+, ads, and other images and returns download links valid for 300 seconds. It costs zero credits. A+ history and available actions can be read with `aplus list`; for interactive A+ review or editing not exposed by these MCP tools, use **`/studio/{productId}/a-plus?aplus=seamless`** or **`/studio/{productId}/a-plus?aplus=sections`** in the Scalable app.

## Image numbering and feedback examples

Keep numbering stable across the conversation, including when a user asks to see an image again. Include the exact role and size returned by the tool, and the exact charged-credit result; if spend is unknown, say it is unknown.

- `#1 — Main listing image — 2000 × 2000 — 12 credits spent` followed by displaying the returned image.
- The user asks to see the same image again: display it as `#1` again, not as a new result.
- `#2 — Gallery lifestyle image — 1600 × 2000 — 12 credits spent (edited from #1)` followed by displaying the returned image.
- Multi-source feedback: `#3 — A+ desktop module — 1464 × 600 — 18 credits spent (generated using references #1 and #2)`. The source numbers refer to the inputs; #3 is a new output. A+ inline image content is unavailable in the current server contract, so provide the supported export link and state that limitation.

For a completed action, report the returned result and next step. For a failed or unclear result, state what the tool actually returned and offer a retry only after a new cost quote and consent. Never claim that an image was saved, exported, or published unless the corresponding tool result confirms it.

## Tool names used

This list is pinned against the live MCP registry in the repository tests. Tool names and argument schemas can change; use the current tool descriptions and returned fields at runtime. `brand-kit create` exists, but its paid action has no matching `credits-quote` action; follow the app path above instead.

`products list`, `product get`, `product create`, `product set`, `product analysis get`, `product brief set`, `product copy set`, `asset upload`, `brand-kit list`, `brand-kit get`, `brand-kit create`, `brand-kit update`, `generate`, `variation create`, `edit erase`, `edit text`, `edit change-format`, `edit text enhance`, `credits-quote`, `job wait`, `image get`, `product-images-export`, `aplus strategy`, `aplus generate`, `aplus generate-mobile`, `aplus list`
