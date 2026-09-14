# Writ — Rebuild 2 mockup

**This is a visual mockup only. It is not the Writ product, and it is not connected to it in any way.**
Nothing here is a working editor: there is no document store, no branching engine and no merge. It
reproduces the explainer animation that Writ showed at the hackathon, and nothing else.

## What Writ is

Writ is version control for writing. It replaces the single shared draft — where edits collide and
ideas get watered down to keep the peace — with branches: everyone writes their version in peace,
then merges. A semantic merge compares what each edit *means* rather than which characters changed,
so tidied wording is accepted automatically while a change that alters the meaning is flagged for
discussion. Conflicts resolve once and merge for everyone, and the document's whole history stays
readable on one map.

## What this repo is

Writ was one of six prototypes built in 48 hours at **Rebuild 2** in Helsinki, 30 August – 1 September
2026. The prototypes are collected at
[rebuild-digital/Rebuild-2-Prototypes](https://github.com/rebuild-digital/Rebuild-2-Prototypes).

This repo rebuilds the explainer animation from that collection's `gifs/writ.gif` as a live page. It
was built from the gif alone — frames, layout and colours — not extracted from any Writ source. Two
scenes play in sequence, the same two the gif shows:

1. **Two ways to write together** — one shared draft, where author cursors collide and edits
   overwrite each other, against a branch-and-merge diagram where versions develop apart and then
   come back together.
2. **A big team, one document** — one source sentence, two edits of it, and a semantic merge that
   decides which one changed the meaning.

## Running it

Open `index.html`. That is all — no server, no install, no build.

## Stack

One self-contained HTML file: inline CSS, inline SVG for the diagrams, and about 40 lines of vanilla
JavaScript to sequence the scenes.

The original is a fourteen-second animated diagram with no interaction and no data, so a framework
would have added a build step, a `node_modules`, and a lockfile to go stale, in exchange for nothing.
A single file also stays readable and runnable years from now, which matters more for a hackathon
artefact than for a product.

Two details worth naming:

- **Motion is CSS, timing is data.** Every animated element carries its own `--d` delay in the
  markup; the script only swaps an `is-live` class per scene. Re-timing the explainer means editing
  numbers, not code.
- **It reflows rather than scales.** The gif is a fixed 900×506 frame. Shrinking that to phone width
  would make the text unreadable, so the layout stacks to one column below 760px and the curved
  connectors become straight stems. `prefers-reduced-motion` is honoured: the animation does not
  autoplay, and the scene dots step through it instead.

## Licence

MIT — see [LICENSE](LICENSE).
