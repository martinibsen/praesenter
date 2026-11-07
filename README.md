# Presenter

Making slides in HTML? Presenter lays out every deck and every slide on one canvas. Drag the order, edit the text, nudge a thing. The file is the truth, and it is written the moment you let go.

**Mac:** [download Praesenter.dmg](https://produktland.dk/praesenter/hent/Praesenter.dmg) (macOS 12 or newer, Intel and Apple Silicon), open it and drag Presenter to Applications. The app is signed and notarised.

**Windows (beta):** [download Praesenter-Setup.exe](https://produktland.dk/praesenter/hent/Praesenter-Setup.exe).

Free while Presenter is in beta.

**Developers, any platform:**

```sh
npx praesenter ./slides
```

This repository holds the releases, the licence and the readme; the source lives in the produktland.dk codebase. More at [trypresenter.com/](https://trypresenter.com/).

![Presenter: a slide is dragged to a new place, Cmd+Z puts it back, and a slide is opened large where the heading is moved](https://trypresenter.com/laerred-en.gif)

## What it does

- **Overview.** Every HTML deck under the folders you give it, as cards with the first slide. Click a deck, and each slide stands on the canvas as a live copy with the deck's own CSS, not a picture. Zoom, or lay the slides out freely like on a whiteboard.
- **Order.** Drag a slide to a new place. Presenter moves the whole `<section>` block in the HTML file, comments and all, and leaves the rest of the file byte for byte. Cmd+Z (Ctrl+Z) undoes. If another program writes to the file meanwhile, the canvas redraws.
- **Editing.** Click a slide, and it opens large in the deck's own editor: click a text and type, click an element to move it, resize it or reset it. Changes are saved to the file as inline style.

The first run comes with an example deck of six slides, one per thing you can do; it is copied into your user folder, so play with it. The rest sits behind **Help** at the bottom of the sidebar.

Your decks stay on your machine. The server listens on 127.0.0.1 only, and the positions on the free canvas are kept in your user folder (`~/Library/Application Support/Praesenter` on macOS, `~/.config/praesenter` on Linux, `%APPDATA%\Praesenter` on Windows), never in the deck.

## Which decks

| Engine | Recognised by | Canvas and order | Editing |
| --- | --- | --- | --- |
| [Slides™](https://github.com/noskillish/slides) | `class="deck"` with `<section class="slide">` | yes | yes (the deck's `?edit` editor) |
| [reveal.js](https://revealjs.com) | `class="reveal"` with `class="slides"` | yes (vertical stacks travel as one block) | no, a click opens the slide in the deck |

No design system is required: a deck is shown with its own CSS, whatever it is. Other HTML decks are not found yet. The engines live in `motorer.js`; adding one is a regex, a selector and a size.

## Usage

```
npx praesenter [folder ...] [options]

  -p, --port <n>   Port to listen on (default 8765; the next free one if busy)
      --no-open    Do not open the browser
  -v, --version    Print the version
  -h, --help       This text
```

Without a folder the current folder is used. Several folders are mounted side by side. Stop with Ctrl+C.

The UI is in English or Danish, following the browser's language; switch at the bottom of the sidebar.

## With Claude Code

Let the AI write the deck and watch it on the canvas while it writes: Presenter redraws a deck within three seconds when its file changes on disk, so you and Claude Code (or Cursor, or anything that writes HTML) work on the same file. The **For Claude Code** button in the sidebar copies a section for your `CLAUDE.md` with the folders, the address and the rules that matter:

```md
## Slides (Presenter)
- Slide decks are single HTML files in ./slides, one file per deck.
- Engine: Slides™ (github.com/noskillish/slides): `<div class="deck">` with one `<section class="slide">` per slide, 1600×900, every size in cqw/cqh. reveal.js decks (`class="reveal"`) are shown too.
- Presenter runs at http://127.0.0.1:8765/ and redraws a deck within 3 seconds when its file changes. Edit the file; never restart the server.
- Keep each slide in its own `<section>` block (Presenter reorders by moving whole blocks), and keep inline `style` in cqw/cqh that the user has set in Presenter.
- To show the user a deck, give the link http://127.0.0.1:8765/?deck=<path under ./slides>.
```

## Requirements

Node.js 20 or newer. Chrome, Edge, Safari or Firefox from 2024 or later (the canvas uses constructed stylesheets and container queries).

## Made by

[Produktland](https://trypresenter.com/) (Martin Ibsen). Siblings: [Point](https://produktland.dk/en/peg/), a Mac app for drawing on what the AI should fix, and [Lyt](https://produktland.dk/en/lyt/), which makes you better one meeting at a time.

Free to use, for personal and commercial work, while Presenter is in beta. Presenter is not open source: see [LICENSE](LICENSE). Versions up to and including 0.4.25 were released under the MIT licence. What leaves your machine (the AI you choose, the read-aloud voice, feedback, update checks) is described in the [privacy policy](https://produktland.dk/en/privatlivspolitik/).
