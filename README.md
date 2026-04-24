# A Short Book on Context Fundamentals

This repository contains the source for *A Short Book on Context Fundamentals*, a short EPUB companion to my Context Fundamentals workshop.

The book is about why AI sessions drift and what to do about it. The short version is that drift is usually a context problem, not a model problem. The longer version is the practice: how to write durable rules, shape better commands, retrieve knowledge just in time, carry context across tools, and build the small habits that make AI work more reliable.

I wrote it because I kept giving a sixty-minute talk to engineers, designers, product managers, and other people who use AI tools seriously, and the useful part always started just as the clock ran out. This is the longer, more practical version of that talk.

## Download

The easiest way to read the book is to download the latest EPUB from the [Releases](https://github.com/dereksmart/a-short-book-on-context-fundamentals/releases) page.

The EPUB is generated from the markdown source in this repo. It is published as a release asset rather than committed to Git, so the source history stays readable while the book remains easy to grab.

## Layout

- `src/` - publication inputs: chapters, back matter, and assets referenced by the manuscript.
- `src/assets/images/` - generated cover and part-opener artwork.
- `src/assets/diagrams/` - source SVG diagrams.
- `src/assets/diagrams/png/` - Kindle-friendlier diagram exports used by the manuscript.
- `references/` - research notes and original workshop script used while drafting.
- `dist/` - generated EPUB output; ignored by git.
- `outline.md`, `style-guide.md`, `asset-notes.md` - production notes, not bound into the EPUB.

## Build Locally

From this directory:

```sh
bookbind src \
  -o dist/context-fundamentals.epub \
  -t "A Short Book on Context Fundamentals" \
  -a "Derek Smart" \
  -c src/assets/images/cover-lit-window.png
```

The `src/` directory is intentionally clean, so bookbind can bind it directly without `--include` / `--exclude` filters.
