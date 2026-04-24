# A Short Book on Context Fundamentals

Markdown source for the EPUB companion to the Context Fundamentals workshop.

## Layout

- `src/` - publication inputs: chapters, back matter, and assets referenced by the manuscript.
- `src/assets/images/` - generated cover and part-opener artwork.
- `src/assets/diagrams/` - source SVG diagrams.
- `src/assets/diagrams/png/` - Kindle-friendlier diagram exports used by the manuscript.
- `references/` - research notes and original workshop script used while drafting.
- `dist/` - generated EPUB output; ignored by git.
- `outline.md`, `style-guide.md`, `asset-notes.md` - production notes, not bound into the EPUB.

## Build

From this directory:

```sh
bookbind src \
  -o dist/context-fundamentals.epub \
  -t "A Short Book on Context Fundamentals" \
  -a "Derek Smart" \
  -c src/assets/images/cover-lit-window.png
```

The `src/` directory is intentionally clean, so bookbind can bind it directly without `--include` / `--exclude` filters.
