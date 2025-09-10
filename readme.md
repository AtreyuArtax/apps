
# The Science Bench

*Interactive tools and simulations for physics, math, and beyond.*

This repo hosts a lightweight, single-file landing page (`index.html`) that links out to your physics/math simulations and supporting tools across multiple GitHub repositories. It’s fast, responsive, accessible, and works on GitHub Pages with no build step.

## ✨ Features

* **Search & filter**: Type to search by title/tags; quick category chips.
* **Light / Dark / Auto** theme: Remembers your preference (localStorage).
* **Reorder by drag & drop**: Drag a card by its **title** to re-arrange; order persists locally.
* **“Download” button**: Pulls a raw `index.html` from another repo and downloads it with a friendly name.
* **Keyboard niceties**: Focus search with **⌘/Ctrl + K**; press **Enter** on a focused card to open it.
* **Accessible & responsive**: Works well with keyboard and screen readers; scales down gracefully.

## 🚀 Getting Started

### 1) Use it on GitHub Pages

1. Push `index.html` to your repo (e.g., `the-science-bench`).
2. In **Settings → Pages**, set **Branch: `main` /root** (or your default branch).
3. Your site will be served at `https://<username>.github.io/<repo>/`.

### 2) Run locally (optional)

* Just open `index.html` in a browser, **or**
* Use a simple server (e.g., VS Code “Live Server” or `python -m http.server`), especially handy for testing downloads and drag behavior.

## 🧩 Adding or Editing Cards

Each app/tool is an `<article class="card">` in the `<main id="grid">` grid. Duplicate an existing card and edit:

```html
<article class="card" tabindex="0"
  data-category="physics"
  data-tags="kinematics graphs position-time velocity-time slope">
  <h3>Kinematics Calculator</h3>
  <p>A comprehensive web-based calculator for 1D/2D kinematics and projectiles.</p>

  <div class="tags">
    <span class="tag">Physics</span><span class="tag">Graphs</span>
  </div>

  <div class="actions">
    <!-- Public app link (GitHub Pages for that repo) -->
    <a class="btn primary" href="https://username.github.io/kinematics_calculator" rel="noopener">Open</a>

    <!-- Optional: robust cross-repo download -->
    <a class="btn download-btn"
       data-raw="https://raw.githubusercontent.com/username/kinematics_calculator/main/index.html"
       data-filename="kinematics_calculator.html">Download</a>
  </div>
</article>
```

**Notes**

* `data-category` should be one of: `physics`, `math`, `tools`, `lab` (used by filter chips).
* `data-tags` is free-form; included in search.
* The **Download** button uses:

  * `data-raw`: the **raw** file URL (from the other repo).
  * `data-filename`: the suggested filename users will save (e.g., `my_tool.html`).


## ⬇️ How “Download” Works (cross-repo, robust)

* The page fetches the **raw** content from another repo (e.g. `https://raw.githubusercontent.com/<user>/<repo>/main/index.html`), builds a Blob, then triggers a download with your `data-filename`.
* If fetching fails (e.g., rate-limited, CORS), it falls back to opening the raw URL in a new tab so the user can save manually.

**Get a raw URL:** In the source repo, open the file → click **“Raw”** → copy the URL.


## 🧱 Reordering Cards (drag & drop)

* Drag by the **card title** (`<h3>`) to move a card anywhere in the grid.
* Order is stored in `localStorage` under `pmhub-card-order` so it persists **for that browser**.
* You can change the handle to allow dragging from anywhere on the card by modifying the SortableJS `handle` option.

**Tip:** The CSS shows a **grab** cursor on the title and keeps a normal arrow elsewhere for a clean look.


## 🎨 Theming & UI Polish

* Theme tokens live in `:root` (light) and are overridden in `[data-theme="dark"]`.
* Users can toggle **Auto / Light / Dark**; the choice is saved under `pmhub-mode`.
* Subtle hover states on cards and buttons; small scale lift on button hover for a modern feel.

If you want a small logo next to the title, drop the inline SVG (e.g., a simple bench + flask) before the “The Science Bench” text and add the small `.logo` styles (see prior commits or ask your favorite AI assistant again 😉).


## ♿ Accessibility & Keyboard

* **Search** has an accessible label and is focused via **⌘/Ctrl + K**.
* **Enter** on a focused card activates its primary “Open” button.
* Buttons and filters have visible focus outlines (with theme-aware ring color).


## 🧪 Structure & Dependencies

* Single file: `index.html` (contains HTML, CSS, JS).
* One tiny external dependency for sorting:

  ```html
  <script src="https://cdn.jsdelivr.net/npm/sortablejs@1.15.2/Sortable.min.js"></script>
  ```

  You can self-host it if preferred; just download and reference locally.


## 🛠 Troubleshooting

* **Downloads don’t start automatically**
  Some browsers block programmatic downloads on strict settings. The code will open the **raw** URL in a new tab as a fallback.

* **Raw URL 404**
  Check the repo path/branch/file name. Make sure the file exists on that branch and you copied the **Raw** link.

* **Order reset**
  Order is saved per-browser via `localStorage`. Clearing site data or using a different browser/device resets the order.

* **Theme not sticking**
  The preference is saved under `pmhub-mode` (values: `auto`, `light`, `dark`). Clearing storage resets it.


## 📝 Editing the Title & Byline

Update the header block:

```html
<div class="title">The Science Bench</div>
<div class="subtitle">Interactive tools and simulations for physics, math, and beyond.</div>
```

You can swap in a brand SVG (e.g., a science bench icon) before the title text and add spacing via CSS.


## 📄 License

MIT — do whatever you like, just keep the license and attribution notices.


## 🙏 Credits

* Drag & drop powered by [SortableJS](https://github.com/SortableJS/Sortable).
* Icons are inline SVGs (no external icon set required).
