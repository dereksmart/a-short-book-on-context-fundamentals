# Book Image Assets

Generated raster art lives in `src/assets/images/`. Deterministic SVG diagrams live in `src/assets/diagrams/`, with Kindle-friendlier PNG exports in `src/assets/diagrams/png/`.

## Raster Art

- `cover-lit-window.png` - recommended cover background, with no embedded title text.
- `part-01-library-dark.png` - Part I opener.
- `part-02-rules-card.png` - Part II opener.
- `part-03-command-form.png` - Part III opener.
- `part-04-directed-reconnaissance.png` - Part IV opener.
- `part-05-context-travels.png` - Part V opener.
- `part-06-tool-landscape.png` - Part VI opener.
- `part-07-context-assembler.png` - Part VII opener.

## SVG Diagrams

- `context-window.svg`
- `lost-in-the-middle.svg`
- `compaction-loss.svg`
- `three-scopes.svg`
- `command-anatomy.svg`
- `just-in-time-context.svg`
- `context-assembler-role.svg`

Use the PNG versions in chapter markdown unless the EPUB pipeline has been verified against the target reader's SVG support.

The generated art intentionally avoids embedded typography, vendor UI, logos, robots, and screenshots so the book can stay durable through tool changes.
