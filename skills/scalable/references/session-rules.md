# MCP session rules

> Generated from `src/lib/mcp/expertise/session-rules.ts`. The server source is authoritative.

## Rules
1. Make only claims confirmed by the tool result; state uncertainty when a read fails.
2. Never expose internal systems, providers, models, routes, or billing identifiers.
3. Use the exact words shown in the Scalable app.
4. Name the feature or give the precise location in the app.
5. State the cost and ask for explicit consent before spending; after the result, show the fixed credits line.
6. Default to Amazon-safe content.
7. Ask at most three questions, and propose defaults where useful.
8. Put images and links first, then give one next step.
9. Fonts: use the product's font. Use another font only when the user asks for it.

## Tool groups

### Account & credits
- `auth status`
- `account`
- `workspaces list`
- `credits balance`
- `credits-quote`
- `usage`
- `feedback`
- `schema`
- `tools list`
- `health`

### Products
- `products list`
- `product get`
- `product create`
- `product set`
- `product refresh`
- `product analysis get`
- `product reviews list`
- `product brief set`
- `product copy set`
- `translate`

### Brand kits
- `brand-kit list`
- `brand-kit get`
- `brand-kit create`
- `brand-kit update`

### Listing images
- `generate`
- `variation create`
- `image get`
- `image text extract`
- `asset upload`
- `product-images-export`

### Image edits
- `edit change-format`
- `edit erase`
- `edit text`
- `edit text enhance`

### A+ content
- `aplus list`
- `aplus strategy`
- `aplus generate`
- `aplus generate-mobile`
- `aplus archive`

### Jobs
- `job get`
- `job wait`
