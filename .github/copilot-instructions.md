## Purpose
Short, actionable onboarding for AI coding agents working on this repo (single-page static portfolio).

Keep edits minimal and obvious: this repository is a plain HTML/CSS static site with assets under `images/` and `icons/`. There is no build system, package.json, or tests.

## Big picture
- Single-file site: primary source is `index.html` (inline CSS in the <head>). Layout uses Bootstrap 4.5 (CDN). Static assets live in `images/` and `icons/`.
- No server code or components. Changes are edits to `index.html` and static assets.

## Key files & structure (examples)
- `index.html` — main and only page. Sections: `#about`, `#projects`, `#skills`, `#contact`. CSS sits in the document head.
- `images/` — photos used by About/Projects/Skills. Follow existing naming (e.g. `images/projects/1.jpg`).
- `icons/` — small social icons (e.g. `icons/github.png`, `icons/linkedin.png`).

## External integrations
- Bootstrap CSS: https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css
- jQuery, Popper, Bootstrap JS included by CDN (see `index.html`).

Notes: if you edit Bootstrap markup, stick to v4 classes. Upgrading to v5 will likely require class changes (collapsing navbar, utilities, spacing).

## Project-specific patterns & conventions
- Cards: Project cards use `.card` with `.card-img-top` and `.card-body`. Images are constrained by `max-height: 180px` and `object-fit: cover`.
- Skills images use `object-fit: contain` and a fixed height of `180px` (see `.skills-section .card-img-top`). Keep new skill icons consistent with this sizing.
- Navigation is a sticky navbar (`.fixed-top`); the document adds `body { padding-top: 56px }` to avoid overlap — preserve this when changing navbar height.
- All links to external profiles are in the Contact section and use `target="_blank"`.
- Accessibility: every image has an `alt` attribute. Keep that pattern when adding new assets.

## Concrete examples (how to perform common edits)
- Add a project card: duplicate one of the `.col-md-4` blocks inside `#projects` row and update `img src`, `card-title`, `card-text`, and the two buttons.
  Example snippet to mirror (paste into `index.html` within the `.row`):

```html
<div class="col-md-4 mb-4">
  <div class="card">
    <img src="images/projects/NEW.jpg" class="card-img-top" alt="Project X">
    <div class="card-body">
      <h5 class="card-title">Project X</h5>
      <p class="card-text">Short project description.</p>
      <a href="#" class="btn btn-primary">Blog Post</a>
      <a href="#" class="btn btn-secondary">Source Code</a>
    </div>
  </div>
</div>
```

- Add a new icon: place the PNG in `icons/` and reference it like `<img src="icons/new.png" alt="New">` inside the Contact section.

## Local preview / developer workflow
- No build step — open `index.html` directly in a browser for a quick preview.
- For a local server (recommended to avoid mixed content/relative path quirks), run from the repo root:

```powershell
# From PowerShell (Windows)
python -m http.server 8000
# then open http://localhost:8000/index.html
```

or, if developing with Node tooling available, `npx serve` is an alternative.

## Known issues & gotchas discovered in code
- Duplicate `id` attributes on a couple of sections (e.g. `section id="projects" class="projects-section bg-light" id="projects"`). Remove the duplicate `id` attribute to avoid invalid HTML and unpredictable JS behavior.
- CSS is inline in `index.html`. If you add many styles, prefer extracting to `css/styles.css` and updating the `<link>` tag rather than leaving large inline blocks.
- Because CDNs are used, offline development will look broken; prefer running a local server with network access, or vendor the bootstrap/jQuery files if offline work is needed.

## Commit & review hints
- Keep commits focused (one visual or content change per commit). Use conventional short messages: `feat: add project card`, `fix: remove duplicate id`, `chore: add new icon asset`.
- When changing layout, include a screenshot in the PR description to speed visual review.

## When in doubt
- Small changes: edit `index.html` directly and preview in the browser.
- Larger refactors (extract CSS, add JS): open a short PR and note the reason (performance, maintainability). Keep Bootstrap v4 semantics or update all corresponding classes if upgrading to v5.

---
If any section above is unclear or you want me to expand examples (e.g., a sample `css/styles.css` extraction or automated preview task), tell me which area and I will iterate.
