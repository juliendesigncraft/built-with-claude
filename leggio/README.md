# Leggio

Leggio is the app I study with. Every subject is a folder on my Mac, every text opens in the same reader: PDF, Word or Markdown. I highlight, write notes on the page, keep a lecture video next to the text, and Leggio keeps track of what I've read. It runs on my computer, no account, no cloud.

**This folder is not the app.** It's the prompt and the resources to build your own Leggio with Claude Code. You get the code, it's yours, and you can change anything. It won't come out identical to mine: the finished app, with the subject dashboards, the video queue, the themes and the Spazio integration, is sold ready to use (see the end of this page).

## What's in this folder

| File | What it is |
| --- | --- |
| `README.md` | This page, with the prompt. |
| [`DESIGN.md`](DESIGN.md) | The look: typefaces, colors, the highlighter palette, page tones. Claude reads it before drawing anything. |
| [`example-library/`](example-library) | A tiny library with two subjects, to try the reader from the first step. |

## How to use it

1. Copy the prompt below.
2. Open an empty folder in Claude Code, on Mac or Windows, and put `DESIGN.md` and `example-library/` inside it.
3. Paste the prompt. Claude shows you a plan first and waits for your OK. Build one step at a time and try each one before the next.

You need [Claude Code](https://claude.com/claude-code) and Python 3 (on a Mac, macOS offers to install it the first time you run `python3`).

**Prompt, for Claude Code**

````text
Build me a local study app called Leggio. It runs on my computer: a small Python server (standard library only, no pip installs) that serves one HTML file on http://127.0.0.1:7333, and opens it in my browser. No accounts, no cloud, no analytics. Read DESIGN.md before you draw anything and follow it.

Work in small steps. Before writing code, show me a short plan and wait for my OK. After every step, tell me how to try it on example-library/.

1. The library
- The library is a folder I choose. Every folder inside it is a subject, every folder inside a subject is a text, named "Author - Title". Files are never moved or renamed by Leggio.
- The home is a desk: one card per subject, with its texts as covers. A cover is drawn from the title (no images needed).
- The server lists the folders and serves the files, only inside the library. It refuses any path that leaves it.

2. One reader for every text
- PDF with pdf.js, Word (.docx) with mammoth, Markdown with a small converter. Keep the libraries in a local lib/ folder so Leggio works offline.
- Zoom with - and +, click the page number to jump to any page.
- Markdown and Word open as a clean page in a serif, readable like a book.

3. Highlight like in Figma
- A toolbar at the bottom center, always visible: arrow, six highlighter colors, underline, a note pinned on the page, a pen, an eraser, undo and redo.
- The selected tool must be obvious: a ring in its own color around the chosen highlighter, a filled button for the others. The cursor takes the color of the highlighter.
- Selecting text with a highlighter chosen highlights it at once. With the arrow, a small menu appears over the selection: colors, note, copy.
- The eraser works by clicking or by dragging over highlights, like a real eraser. One undo brings back everything it erased in one pass.
- Undo and redo with Cmd-Z and Shift-Cmd-Z, also when the cursor is inside the text.
- Highlights and notes are saved as JSON in a hidden _Leggio/ folder inside the library, never inside the original files.

4. Know what I've read
- A page counts as read when it stays on screen for 15 seconds. The last page counts after 5.
- In the reader bar: a small ring with the percentage, and a page map with one segment per page (read, unread, where I am). Clicking the map jumps to that page.
- When I open a text again, it goes back to the page where I left it.

5. Side by side
- Open a second text next to the first, and swap them.
- A video window for the lecture: a YouTube link or a local video file. It can float or dock to the left or right edge, and its title bar has the same height and color as the reader bar.
- Full screen with the F key: the top bar hides and comes back when the mouse reaches the top edge. Esc leaves.

6. A page per subject
- For each subject, a dashboard: its texts with their pages (read from the PDF) and progress, plus chapters I add by hand and tick as I go.

7. Look a word up
- Select a word or a short term: "What is it" shows a card with the definition and the pictures from Wikipedia (in the language of the text), plus buttons for Google and Google Images.
- Select a whole passage I don't understand: "Explain" opens a panel on the right. The server asks Claude Code (the one installed on my computer, run with claude -p, no API key in Leggio) for a JSON answer: a title, one simple sentence, the passage in plain words, an everyday comparison, the steps if it describes a process, and up to four key things with an English search for a picture. Show the steps as a numbered line and the key things with their pictures (the lead image of the Wikipedia article, Wikimedia Commons as a fallback). "Save as a note" keeps it next to the highlight.

8. Themes
- A settings panel: color theme, background, page tone (light, sepia, slate, almost black), sounds on or off, language (English and Italian).

Things that will trip you up
- pdf.js text layers are a little narrower than the printed glyphs, so a fast selection leaves half a letter out. Before saving a highlight, extend the selection to whole words and trim the spaces at the edges.
- In Word and Markdown, never wrap a whole selection in one <mark> with extractContents: a selection that crosses two list items or paragraphs splits them in two, and the eraser can't put them back. Wrap every text node the selection touches in its own <mark>, all with the same id, and remove them all together.
- The browser's own undo doesn't know about the highlights you add with code. Keep your own undo stack of snapshots (annotations + the HTML of the page) and only let the browser undo when I typed text after the last highlight.
- On dark page tones a multiply highlighter disappears into the black. There, blend it with screen and keep the highlighted text white.
- A short last page never reaches the reading line at one third of the screen. If the reader is scrolled to the bottom, I'm on the last page.
- A YouTube embed needs the page to be served from http://127.0.0.1, not opened as a file.

Rules
- Nothing leaves my computer, except the Wikipedia and Google lookups I ask for.
- A README that says how to start Leggio, where my highlights live, and how to back them up.
````

You'll get a working reader in a session or two. Then use it every day and ask Claude for one detail at a time.

## Want the finished Leggio?

Mine does more, already built and tested: covers, a desk with widgets and a timer, the video queue, Verify (questions on the pages you just read), Word and Markdown editing, the pen on PDFs, saving a highlighted copy of a PDF, and the Dark Matte look when it runs inside Spazio, my AI system. The finished Leggio will be sold ready to use. Coming soon on [juliendesigncraft.gumroad.com](https://juliendesigncraft.gumroad.com).
