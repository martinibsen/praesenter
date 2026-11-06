---
name: praesenter
description: Use when the user wants slides, a deck or a presentation made or changed as HTML for Present (Præsenter) - "make a deck", "lav slides til", "add a slide", "tighten my slides", "et deck til", "tilføj et slide". Writes one self-contained HTML file per deck in the Slides engine format and shows it in Present.
---

# Slides for Present (Præsenter)

Dansk: Present (Præsenter) er lærredet til slide-decks i HTML. Hvert deck er én fil, hvert slide er en `<section class="slide">`, og Present tegner decket om, hver gang filen ændres. Resten af skillen er på engelsk, fordi den læses af modellen.

## Where things are

- Decks are single HTML files in {{STIER}}. Present runs at {{PORT}} and redraws a deck within three seconds of the file changing. Show a deck with `{{PORT}}?deck=<path>`.
- A new deck starts as a copy of the design guide: {{STIL}}. Keep everything in `<head>` (the theme) and the two `<script>` blocks at the bottom (the engine and the editor) exactly as they are; write new `<section>` blocks between `<div class="deck">` and `</div>`.
- Edit the same file. Never save a new version next to it (`deck-v2.html`, `deck-new.html`): Present has Undo, and extra copies show up as duplicates in the user's overview.
- Keep the inline `style` the user has set on an element in Present, and keep each slide in its own section block, indented two spaces, with `</section>` on its own line at the same indentation. The engine cuts the file into slides by that indentation.

## The format

```html
<div class="deck">

  <section class="slide active">
    <h1>One sentence that carries the slide.</h1>
    <p>At most one to three short lines under it.</p>
  </section>

  <section class="slide dark">
    <span class="step">2 · Section</span>
    <h2>A short heading.</h2>
    <p>Body text in the deck's own voice.</p>
  </section>

</div>
```

- Only the first slide has `active`.
- Sizes are in container units: `cqw` for widths and font sizes, `cqh` for vertical space. Never `vw`/`vh`: the deck is a 16:9 stage, and container units follow the stage, not the window.
- Use the classes the design guide already defines (`dark`, `step`, `cols`, `keys`, `cmd`, `mark` in the example deck; a company's guide has its own). Add a class to the theme only when no existing one fits, and add it inside the existing `<style>` block.
- Times for workshops: `data-minutter="10"` on a section, and `<meta name="praesenter-start" content="09:00">` in `<head>`. Present shows them on the canvas only.
- Speaker notes: a `<aside class="notes">` inside the section, if the theme has one; otherwise none.

## Four kinds of slide

1. **Statement**: a single `<h1>`, maybe one line under it. Opening, section breaks, the close.
2. **Structure**: `<h2>` and a short list or two columns (`.cols`). The workhorse.
3. **Quiet**: one quote or one principle, lots of space, the `dark` class if the guide has it.
4. **Photo**: a full-bleed image with a short text plate. Only with a real image the user gave you.

Each point in a talk gets one slide. A reading deck (sent, not presented) may carry more text per slide.

## Slide craft (follow these)

- Nothing may overflow or leave the slide. When there is too much, split it into more slides instead of shrinking the text.
- One idea per slide in a deck that is talked over; at most 1-3 short lines of body text. Only a reading deck may carry more.
- Not everything centred, and no grid of identical cards; give the slide one clear focal point and a deliberate layout from the deck's own patterns.
- Keep to the deck's fonts, colours and spacing. Never add Inter, Roboto, Arial, purple gradients, generic indigo (#6366f1), glassmorphism or drop shadows without a reason.
- Never negate a CSS function directly (`-clamp()`, `-min()`, `-max()` are silently ignored); write `calc(-1 * clamp(...))`.
- Short headings. Keep sentences under about twelve words. No em dashes in the text.

## When you are done

Say which file you wrote or changed and give the user the Present link `{{PORT}}?deck=<path>`. If Present is not installed, point them to https://produktland.dk/slides/ (Mac and Windows app, free in beta; `npx praesenter <folder>` runs it in the browser).
