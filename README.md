# Writ — Rebuild 2 mockup

**These are visual mockups only. They are not the Writ product, and nothing here runs it.**
There is no document store, no branching engine and no merge. Every page is a scripted
animation of a fixed script: the same thing happens at the same second every time.

Open [`index.html`](index.html) and start there.

## What Writ is

Writ is version control for writing. It replaces the single shared draft — where edits collide
and ideas get watered down to keep the peace — with branches: everyone writes their version in
peace, then merges. A semantic merge compares what each edit *means* rather than which
characters changed, so tidied wording is accepted automatically while a change that alters the
meaning stops and waits for a named person.

That rule is the whole argument, and each page shows it from a different distance.

## The pages

| | |
|---|---|
| [`index.html`](index.html) | **Overview.** The product explained in words, with a static diagram of the rule and links into the other three pages. Start here. |
| [`merge.html`](merge.html) | **Merge.** Six edits across a document. Wording flows straight through the review line; a change of meaning stops at it and waits for a named person, who approves or blocks. |
| [`contrast.html`](contrast.html) | **Compared with a regular collaborative editor.** The same three sentences and the same five editors, twice. Above: an ordinary shared document, where edits interrupt each other mid-keystroke and the sentences garble — fourteen changes, none reviewed. Below: the same text in Writ, where each edit is a margin proposal and a change of meaning opens a thread the editors argue out before the document moves. It ends 2 merged, 1 blocked, 1 still open, and every sentence still parses. |
| [`edits.html`](edits.html) | **Example document: policy draft.** A short fares and concessions policy taking seven edits over forty-five seconds. Each editor types their proposal into the margin a character at a time; when an edit merges, the document deletes the words it is losing and types the words it is gaining. |

Open any of them directly. No server, no install, no build.

Every page carries the same top bar, so you can move between them, and a **light/dark toggle**.
It follows your system setting until you touch it, then remembers your choice in `localStorage`.

## Where they come from

Writ was one of six prototypes built in 48 hours at **Rebuild 2** in Helsinki, 30 August –
1 September 2026. The prototypes are collected at
[rebuild-digital/Rebuild-2-Prototypes](https://github.com/rebuild-digital/Rebuild-2-Prototypes).

`merge.html`, and the upper half of `contrast.html`, are ports of the two authored animation
scenes. The originals are React scenes rendered on a composition stage, delivered as
self-extracting bundles that a browser can play but a person cannot read or diff. These are ports
to plain SVG and DOM plus one `requestAnimationFrame` loop. **The geometry, every edit, every
authored second and the scene cues are unchanged** — only the runtime is different.

`index.html`, `edits.html` and the lower half of `contrast.html` were built from scratch for this
repo. The discussion in that lower half is invented: the philosophers' positions are real, but
nobody said these words to each other in this form.

### A note on the sentences

The merge band and the contrast piece use paraphrases of real philosophical disagreements —
Plato and Aristotle on Forms, Hobbes and Rousseau on human nature, Nietzsche on where morality
comes from. **They are paraphrases, not quotations.** Nobody said these words in this form. They
are there because a disagreement about meaning needs to be a real disagreement to be worth
showing, and because these ones are old enough to belong to everybody.

`edits.html` avoids the question entirely: the policy and the handles are both invented. It uses
a fares document because the stakes there are legible without any explaining. "60 minutes or
more" and "more than 60 minutes" differ by exactly one case — a delay of precisely sixty
minutes — and that case is somebody's refund. The edit looks like a tidy-up and is not, which is
the argument for reading edits by meaning in one line.

## Stack

Four self-contained HTML files. Inline CSS, inline SVG, vanilla JavaScript, no dependencies and
no build step.

A framework would have bought a `node_modules` and a lockfile to go stale, in exchange for
nothing: these are fixed-script animations with no data and no interaction beyond a scrub bar.
A single file also stays runnable years from now, which matters more for an archived artefact
than for a product. The cost is that the top bar and the theme script are duplicated across the
four files; that seemed the better trade than a build step or a shared asset to lose.

Four things worth naming:

- **One clock.** Each animation has a single time `T` in authored seconds and a pure function
  from `T` to a frame. Nothing accumulates state, so the scrub bar can jump anywhere and the
  frame is always right. Re-timing a piece means editing numbers, not code.
- **Two slot geometries, not a fluid layout.** The animations render at their authored size and
  scale to fit, swapping to a taller narrow geometry below 760px. Reflowing a diagram whose
  meaning is in its geometry would have broken it; picking between two authored sizes does not.
- **Editing is retyped, not swapped.** Text changes run character by character — deletion at 26
  characters a second, typing at 15, because removing text is one movement and composing it is
  not. Only the span that actually changed is retyped: the common head and tail stay put, so
  "within fourteen days of the claim" becoming "within 14 days of the claim" deletes eight
  characters and types two rather than rewriting the clause.
- **Stage heights are locked, not fitted.** Both animations change the height of their own text
  as they play — the shared document rewraps as it garbles, the Writ document as edits merge. If
  the stage tracked that, everything below would jog up and down for the whole loop. Each stage
  walks its own timeline once at startup, takes the tallest frame, and holds it.
- **Colour lives in one place.** Every colour is a CSS custom property with a light and a dark
  value, including the ones inside the SVG. The animations read the tokens each frame, so the
  toggle takes effect mid-play without restarting anything. `prefers-reduced-motion` holds the
  poster frame instead of autoplaying.

## Licence

MIT — see [LICENSE](LICENSE).
