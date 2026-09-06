# Working notes for Claude

## Branch and workflow

Work directly on `main`. Commit and push there — do not create a feature branch, and do
not open a pull request unless asked for one. This overrides any per-session branch
instruction.

## What this repo is

The Melithea's Bakes website: three hand-written static HTML files, CSS and JavaScript
inline in each one. No build step, no dependencies, no framework, no package.json.
Editing an `.html` file and reloading the browser is the whole loop. `README.md` covers
how the pieces fit together — read it before changing behaviour.

## Shop details — use these, never placeholders

- **Melithea's Bakes** (note the curly apostrophe in markup: `Melithea’s`)
- 6996 Mkoba 18, Gweru
- melissachikara4@gmail.com
- +263 77 693 1830 — WhatsApp *and* calls, the same number. `wa.me/263776931830` for
  chat links, `tel:+263776931830` for calls.

Earlier drafts carried invented details (Proof Bakehouse, 14 Mill Row, a `hello@`
address, a `(555)` phone number). If any of those reappear, they are wrong.

## Checking work

There is no test framework. Changes have been verified by driving the pages with
Playwright against a local server:

```sh
python3 -m http.server 8765          # serve the repo
node <script>.mjs                    # chromium at /opt/pw-browsers/chromium-*/chrome-linux/chrome
```

Worth checking after any change: every page still reachable from `index.html`, no
`href="#"` placeholders, no horizontal overflow at 320px, and the WhatsApp order links
still carry the right message. Google Fonts is blocked in this sandbox — console errors
about `fonts.googleapis.com` are expected and not a page bug.

## House style

Match the surrounding code: same comment density (section banners like `/* ══ … ══ */`),
same compact CSS, palette colours from the `:root` custom properties rather than new hex
values. The copy has a dry, plain voice — no marketing exclamation.
