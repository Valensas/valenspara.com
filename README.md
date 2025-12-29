# valenspara.com
Valenspara Web Sitesi

## Purpose
This repository is a Jekyll-based static website for Valenspara (Turkish).

## Build & Run (developer)
- Use the Ruby/Bundler flow: install dependencies then serve locally:

  ```bash
  bundle install
  bundle exec jekyll serve
  ```

- `Gemfile` pins `jekyll ~> 4.3` and includes the `jekyll-feed` plugin.
- `_config.yml` sets `host: 0.0.0.0` and uses `site.baseurl` for relative URLs.

## Project layout (important files)
- Content pages: top-level `.md` files (e.g. `about.md`, `contact.md`) generate their routes.
- Collection `projects`: files in `_projects/` (example: `_projects/01-kesinti.md`) use `layout: project_single`.
- Templates: `_layouts/` (e.g. `default.html`, `projects.html`, `project_single.html`).
- Includes: `_includes/` (e.g. `nav.html`, `head.html`, `footer.html`) — modify these for site-wide changes.
- Styles: `css/main.scss` and `_sass/` partials. Jekyll compiles SCSS to `_site/css/main.css`.
- Static assets: `img/`, `js/` (including `MultiCarousel.js`), and `files/`.
- Build output: `_site/` (do not edit directly).

## Conventions & patterns (repo-specific)
- Navigation is driven from `_config.yml` via `site.nav` (example lines near top of `_config.yml`). Edit there to add/remove nav links.
- Use Liquid filters consistently: `{{ '/path' | prepend: site.baseurl }}` and `{{ page.url | relative_url }}` are used across templates.
- Pages use front matter for metadata. Example project front matter includes `title`, `project_date`, `project_type`.
- Scripts: `MultiCarousel.js` and `main.js` are in `js/`. The `default.html` layout currently has script tags commented out — check intent before re-enabling.

## Editing guidance (examples)
- To add a new project announcement: create `_projects/08-new-event.md` with:

  ```yaml
  ---
  layout: project_single
  title: 08.08.2025 - Başlık
  project_date: 08.08.2025
  project_type: [Duyuru]
  ---
  İçerik...
  ```

- To change top navigation order or names, edit `site.nav` in `_config.yml` (the layout iterates `site.nav` in `_includes/nav.html`).
- For CSS fixes, prefer editing `_sass/_includes/*.scss` or `css/main.scss`.

## External integrations & deploy notes
- Uses CDN-hosted Bootstrap, jQuery, Popper (see `_includes/head.html`).
- `Gemfile` lists Ruby gems; no Node build pipeline is present.
- The site is served from the `gh-pages` branch in this workspace; `_site/` contains the generated output.

## Safety & common pitfalls
- Do not edit files in `_site/` — they are generated.
- Keep `site.baseurl` usage when referencing assets so paths work in production.
- When re-enabling JS includes in `_layouts/default.html`, verify that `MultiCarousel.js` is referenced at `js/MultiCarousel.js` and that `main.js` initialization in `main.js` points to an existing DOM element (e.g. `.logo-row`).

## Where to look for examples
- Navigation: `_includes/nav.html` and `_config.yml`.
- Project collection: `_projects/01-kesinti.md` and `_layouts/projects.html`.
- Global layout: `_layouts/default.html` and `_includes/head.html`.
- Styles: `css/main.scss` and `_sass/_includes/*.scss`.

## If you need to change build config
- Update `_config.yml` for site settings.
- Update `Gemfile` and run `bundle install` to change Jekyll or plugin versions.
