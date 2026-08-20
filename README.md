# Melithea's Bakes

A small, static three-page site for a one-bake-a-day neighbourhood bakery. No build
step, no dependencies, no framework — three hand-written HTML files with their CSS and
JavaScript inline. Open `index.html` in a browser and it runs.

## The pages

| File | What it is | Reached from |
| --- | --- | --- |
| `index.html` | Home: today's bake, bench notes, where to find us, whole-cake pitch | — |
| `cake-builder.html` | Five-step whole-cake order builder with a live drawing and a docket | Nav doors, hero button, cake strip, footer |
| `lemon-curd-tart.html` | Product page for the lemon curd tart: viewer, options, how it's made | Tart card on the home page, footer |

Every page links back to the home page from the plaque in the top bar, and every page is
reachable from `index.html` — there are no orphans and no `href="#"` placeholders.

## Running it

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening the files directly with `file://` works too, though the shared box (below) needs
`localStorage`, which some browsers withhold from `file://` pages. The code degrades
quietly if that happens — the box just stops carrying between pages.

## How it fits together

**Filter deep links.** The shop grid on the home page filters by category. Any page can
link straight into a filtered view with `index.html#f-<category>`, where `<category>` is
one of `all`, `cake`, `cupcake`, `loaf` or `small`. The home page reads that hash on load
and on `hashchange`, sets the matching chip and scrolls to the shop. Unknown categories
are ignored rather than blanking the grid.

**The box.** The item count and running total live in `localStorage` under
`melitheas-box`, so adding a tart on the product page and then going back to the shop
shows the same count in the top bar. Every read and write is wrapped in a `try` so a
blocked storage API can't take the page down. "Check out" clears the box; it does not
talk to a server.

**The cake builder.** `DATA` at the top of the script holds the sizes, sponges, fillings
and finishes — name, note, price and swatch colour. Everything else derives from it: the
option cards, the running price, the SVG drawing and the docket lines. To change the
menu, edit `DATA` and nothing else. `DEFAULTS` is what "Start again" resets to.

**Type.** Google Fonts (Caveat, Karla, Permanent Marker, Amatic SC) with a real fallback
stack behind each one, so the site still reads correctly offline or with the CDN blocked.

## Conventions

- Colours come from the CSS custom properties in `:root` — `--jam`, `--butter`,
  `--kraft`, `--paper`, `--ink`, `--pistachio`, `--plum`. Use them instead of new hex
  values so the three pages stay in step.
- Illustrations are inline SVG, no image files.
- Prices and stock counts are duplicated between the home page cards and the product
  page. If one changes, change the other — the lemon curd tart is currently $28 with
  four left.
- Everything is responsive down to 320px, and `prefers-reduced-motion` is respected.
