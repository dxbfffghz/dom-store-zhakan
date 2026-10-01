# dom-store-zhakan

**Lab 5 — DOM, events, forms**
Author: Akerke Zhakan
Live: https://dxbfffghz.github.io/dom-store-zhakan/

An interactive product list built with **pure JavaScript and the DOM API**.
No frameworks, no libraries — only `document`, `addEventListener`, and my own
`Store` class carried over from Lab 4 (`js-core-zhakan`).

---


Because the project uses ES modules (`<script type="module">`), it must be served over HTTP, not opened as `file://`.

Easiest way — with VS Code + Live Server extension:

1. Install **Live Server** extension in VS Code.
2. Right-click `index.html` → **Open with Live Server**.

Or with Python:

```bash
python -m http.server 8000

Which events I handled and why
I attached three listeners. The first is on the <form> element for submit — I call preventDefault() there so the page never reloads, then validate the inputs in the DOM and show errors next to the fields. The second is a single click listener on the <tbody id="product-list"> — this is event delegation: instead of putting a listener on every Delete button, I put one on the parent and use event.target.closest('button[data-action="remove"]') to find which row was clicked. The third is a change listener on the same table for the quantity <input> — again delegation, one listener handles every row. Because all three react to user actions, the total is recalculated from scratch after each change, so the number always stays live. Delegation also means that newly added rows automatically get working buttons without re-binding.
## Screenshot

![DOM Store page](screenshots/page.png)

The page shows:

- the "Add product" form on top,
- the products table with two seeded rows (Book, Notebook),
- the Delete button and the quantity input on every row,
- the live total at the bottom.

---

## AI tools used

- **Claude (Anthropic)** — for help with the README structure and for
  a review of the event delegation pattern.
- Everything in `src/app.js` and `src/Store.js` was written, run and
  verified by me. I can explain any line at the defense.

---

## What I would improve next

- Persist the list in `localStorage` so it survives a page reload.
- Add an "edit name" mode for existing products.
- Replace `innerHTML` in `render()` with `document.createElement` for
  the whole row, to make the XSS protection explicit.
- Write a few DOM tests with Vitest + `jsdom`.