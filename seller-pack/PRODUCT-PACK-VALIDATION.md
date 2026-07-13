# Product Pack Validation — Southern Suburbs Builders

## Schema discrepancy found (important)

`handoff/codex/PRODUCT-PACK-SCHEMA.md` documents a `francis-listing-manager-import.json`
manifest shape (`sku`, `title`, `description`, `price`, `currency`, `images[].role`,
`buyerFiles[]`) inside a self-contained ZIP. Per this release's instruction to
independently inspect the **actual** Francis Listing Manager repository
before generating the pack rather than trust a possibly-outdated schema
doc, I read the real import path directly:

- `/home/iedrees/Workspace/francis-listing-manager/scripts/product-import-cli.js`
- `/home/iedrees/Workspace/francis-listing-manager/server/services/validation.js`
- `/home/iedrees/Workspace/francis-listing-manager/server/services/etsyDeploymentService.js`
- `/home/iedrees/Workspace/francis-listing-manager/server/db/repositories/content.js`

**The real, current import mechanism is different from Codex's documented
schema.** It is a local CLI (`npm run product:import -- /absolute/path/to/product-import.json`),
not a ZIP-with-manifest upload:

```json
{
  "product": {
    "internal_name": "string, required",
    "product_type": "digital | physical",
    "status": "draft | content_ready | ready_to_list | published | archived",
    "price": "number > 0, OPTIONAL for import (required only later, for a draft)",
    "quantity": "integer >= 1",
    "etsy_taxonomy_id": "positive integer, OPTIONAL for import (required only later, for a draft)"
  },
  "content": {
    "title_option_1": "...", "title_option_2": "...", "title_option_3": "...",
    "description": "...", "short_summary": "...", "whats_included": "...",
    "how_it_works": "...", "who_its_for": "...", "benefits": "...",
    "important_notes": "...", "digital_disclaimer": "...", "buyer_instructions": "...",
    "faq": "...", "ai_disclosure": "...", "image_alt_text": "...", "social_caption": "..."
  },
  "tags": ["exactly 13 recommended, each <=20 chars"],
  "images": [{ "path": "/absolute/local/path.png", "altText": "..." }],
  "files": [{ "path": "/absolute/local/path" }]
}
```

Key differences from Codex's documented schema, and why they matter:

| Codex's doc said | Actual code requires | Impact |
|---|---|---|
| `sku` field | `internal_name` (no dedicated SKU column found in `products` table) | Used `internal_name` as the effective unique identifier |
| `currency` field on the manifest | No currency field in `validateProductInput` or the `products` schema | Currency is evidently a shop-level Etsy setting, not a per-product import field — consistent with Phase 9's finding that currency must come from the connected shop, not be guessed per-listing |
| `images[].role: "cover"` | No `role`/`cover` field — the CLI takes `images[]` in array order and `imagesRepo.create()` stores them in that order (first entry becomes first-listed image) | Order in the array, not a special field, controls cover position |
| `buyerFiles[]` with `label` | `files[]` with just `path` (no label field in `filesRepo`) | Buyer files are stored by filename only |
| Relative paths inside a ZIP | **Absolute local filesystem paths** — the CLI copies from disk directly into FLM's managed storage (`imageService.ORIGINALS_DIR`, `paths.FILES_DIR`) | This is a local-machine CLI import, not a portable ZIP-upload workflow. A `product-import.json` referencing absolute paths only makes sense on the machine running the FLM server, and is correctly **not** committed to the public git repository (it would contain local file paths, which Non-Negotiable Rule 12 explicitly prohibits from public media) |
| Price/taxonomy required at import | Both are **optional** at import (`validateProductInput`), but **both required** before a draft can be created (`validateProductForDraft` in `etsyDeploymentService.js`: `price > 0` and `etsy_taxonomy_id` truthy) | Confirms the correct, code-enforced stop point for this release: import succeeds without a price; the Etsy-draft script will itself refuse to run without one — see Phase 17/18 |

## What was actually built

1. **`seller-pack/southern-suburbs-builders-complete-product-pack.zip`** — a
   self-contained, portable archive (manifest + all assets, relative paths,
   no secrets, no absolute paths) kept as the human-readable/portable
   record of this release's product data, in the spirit of the task's
   named deliverable. This is **not** what gets fed to the FLM CLI, per
   the schema finding above.
2. A local-only `product-import.json` (absolute paths, machine-specific,
   **not committed to this repository**) matching the real CLI schema —
   generated at Phase 17 execution time, immediately before the import
   attempt, and never persisted to git or public media.

## Validation run

```
$ node scripts/release/scan-secrets.js seller-pack
Secret scan passed

$ node tests/release/test-release-validators.js  (from the ct-lead-gen codex build)
scan-secrets passed
validate-media passed
validate-product-pack passed
validate-zip-content passed
```

`validate-product-pack.js` and `validate-zip-content.js` (Codex's tools)
validate the **portable ZIP** described above against Codex's documented
schema — which remains a reasonable, safe, self-contained format for the
archive even though it is not the literal shape the FLM CLI consumes. Both
passed. See the counts below.

## Counts

- Tags: 13 (exactly), unique, all ≤20 characters — `seller-pack/listing/final-tags.json`
- Listing images: 10 (exactly), one cover (`01-cover.png`, first in order) — `seller-pack/media/listing-images/`
- Buyer files: 5 (exactly, at Etsy's limit) — `seller-pack/buyer-files/`
- SKU / internal name: `BUILDERS-WEB-001` / "Southern Suburbs Builders Website Template"
- Price / currency: **unresolved** (see `handoff/PHASE-9-PRICE-CATEGORY-RESOLUTION.md`) — intentionally absent from the pack, not guessed
- No `.env`, `.git`, credentials, tokens, `node_modules`, or absolute/local paths anywhere in the committed pack
