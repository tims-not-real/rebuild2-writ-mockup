# Writ — Rebuild 2 mockup

**These are visual mockups only. They are not the Writ product, and nothing here runs it.**
There is no document store, no branching engine and no merge. Every page is a scripted
animation of a fixed script: the same thing happens at the same second every time.

## What Writ is

Writ is version control for writing. It replaces the single shared draft — where edits collide
and ideas get watered down to keep the peace — with branches: everyone writes their version in
peace, then merges. A semantic merge compares what each edit *means* rather than which
characters changed, so tidied wording is accepted automatically while a change that alters the
meaning is flagged for discussion.

That rule is the whole argument, and each page here shows it from a different distance.

## The pages

| | |
|---|---|
| [`index.html`](index.html) | **The merge band.** Six edits across a document. Wording flows straight through review; a change of meaning stops at the review line and waits for a named person, who approves it or blocks it. |
| [`contrast.html`](contrast.html) | **The same edits with no branches and no review.** Everyone types into one live document at once. Edits interrupt each other mid-keystroke and the sentences garble: fourteen changes, none reviewed. |
| [`edits.html`](edits.html) | **One sentence, edit by edit.** The rule slowed right down — four edits on a single fare rule, each classified and resolved in turn, with the document updating only when something actually merges. |
| [`explainer.html`](explainer.html) | **The hackathon explainer.** The two-scene animation Writ showed at Rebuild 2, rebuilt from the gif in the prototypes collection. |

Open any of them directly. No server, no install, no build.

## Where they come from

Writ was one of six prototypes built in 48 hours at **Rebuild 2** in Helsinki, 30 August –
1 September 2026. The prototypes are collected at
[rebuild-digital/Rebuild-2-Prototypes](https://github.com/rebuild-digital/Rebuild-2-Prototypes).

`index.html` and `contrast.html` are ports of the two authored animation scenes. The originals
are React scenes rendered on a composition stage, delivered as self-extracting bundles that a
browser can play but a person cannot read or diff. These are ports to plain SVG and DOM plus one
`requestAnimationFrame` loop. **The geometry, every edit, every authored second and the scene
cues are unchanged** — only the runtime is different.

`edits.html` was built from scratch for this repo. `explainer.html` was rebuilt from
`gifs/writ.gif` in the prototypes collection, frame by frame.

### A note on the sentences

The merge band and the contrast piece use paraphrases of real philosophical disagreements —
Plato and Aristotle on Forms, Hobbes and Rousseau on human nature, Nietzsche on where morality
comes from. **They are paraphrases, not quotations.** Nobody said these words in this form. They
are there because a disagreement about meaning needs to be a real disagreement to be worth
showing, and because these ones are old enough to belong to everybody.

`edits.html` uses the fare rule from the hackathon explainer instead, with invented handles.

## Stack

Four self-contained HTML files. Inline CSS, inline SVG, vanilla JavaScript, no dependencies and
no build step.

A framework would have bought a `node_modules` and a lockfile to go stale, in exchange for
nothing: these are fixed-script animations with no data and no interaction beyond a scrub bar.
A single file also stays runnable years from now, which matters more for an archived artefact
than for a product.

Three things worth naming:

- **One clock.** Each page has a single time `T` in authored seconds and a pure function from
  `T` to a frame. Nothing accumulates state, so the scrub bar can jump anywhere and the frame is
  always right. Re-timing a piece means editing numbers, not code.
- **Two slot geometries, not a fluid layout.** The animations render at their authored size and
  scale to fit, swapping to a taller narrow geometry below 760px. Reflowing a diagram whose
  meaning is in its geometry would have broken it; picking between two authored sizes does not.
- **Theme follows the reader.** Both token sets ship, and the pages follow
  `prefers-color-scheme`. `prefers-reduced-motion` holds the poster frame instead of autoplaying.

## Licence

MIT — see [LICENSE](LICENSE).
