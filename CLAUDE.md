# CLAUDE.md

Guidance for Claude Code sessions working on this repo.

## Project snapshot
Static personal portfolio site deployed via **GitLab Pages**. Single page ([index.html](index.html)) using **Bootstrap 5.3** + **Bootstrap Icons** + **particles.js** loaded from CDN. No build step, no framework, no package manager. [style.css](style.css) is currently empty — all styles are inline in `index.html`. Deploy is automatic on push to `main` via [.gitlab-ci.yml](.gitlab-ci.yml).


## project instruction
- background theme should be the same everytime even if i give any instruction.

## HTML practices
- Always include `<!DOCTYPE html>`, `<html lang="en">`, UTF-8 charset, and viewport meta.
- Use semantic tags — `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>` — instead of generic `<div>` containers.
- Every `<img>` needs an `alt` attribute; use `alt=""` for purely decorative images.
- Use `<button>` for actions and `<a href>` for navigation. Don't swap them.
- Associate form inputs with `<label for="id">`. Reach for `aria-label` only when a visible label isn't possible.
- One `<h1>` per page. Don't skip heading levels (`h2` → `h4`).
- `<link rel="stylesheet">` goes in `<head>`. `<script>` goes at the end of `<body>` or uses `defer`.

## CSS practices
- As the site grows, move styles out of the inline `<style>` block into [style.css](style.css). Inline is fine for a one-file prototype; it is not the long-term home.
- Keep theming via CSS custom properties (`--bg`, `--text`, `--accent`) — this is already the pattern, extend it.
- **Mobile-first**: base styles target small screens, use `@media (min-width: ...)` to scale up.
- Use `rem`/`em` for typography and spacing, `%`/`vw`/`vh` for layout, reserve `px` for borders and hairlines.
- Use flexbox or grid for layout. Never use floats for layout.
- Keep specificity low: prefer single-class selectors, avoid `!important`.
- Name classes by purpose (`.project-card`, `.hero-img`), not appearance (`.red-box`).
- Wrap non-essential animations in `@media (prefers-reduced-motion: no-preference)` — e.g., the existing modal `zoomIn` keyframe.

## Bootstrap 5.3 practices
- Use the grid (`container` → `row` → `col-*`) for layout. Don't hand-roll flex containers when Bootstrap utilities already cover it.
- Prefer utility classes (`mt-3`, `d-flex`, `text-center`, `gap-2`) over writing custom CSS for one-off spacing and alignment.
- Only override Bootstrap when necessary. When you do, scope the override to a custom class — don't restyle `.btn` or `.card` globally.
- This is Bootstrap **5**: use `data-bs-*` attributes. Never mix in Bootstrap 4 `data-*` syntax.
- `bootstrap.bundle.min.js` already includes Popper — don't load Popper separately.
- Use built-in components (modal, collapse, offcanvas, dropdown) instead of reimplementing them.
- Check color contrast against WCAG AA. The dark theme with `#f7b733` accent should be verified for text contrast.

## Accessibility
- All interactive elements must be keyboard-reachable via Tab with a visible focus ring.
- The theme toggle must be a real `<button>` with an `aria-label` (e.g., "Toggle dark mode"), not a clickable `<div>`.
- The particles background (`#particles-js`) is decorative — mark it `aria-hidden="true"`.
- Respect user preferences: `prefers-reduced-motion`, `prefers-color-scheme` where practical.

## Performance
- Compress images in [images/](images/) before committing (target < 200 KB for photos).
- Use `loading="lazy"` on images below the fold.
- Minimize CDN requests. The current three (Bootstrap CSS, Icons, particles.js) are fine — don't add more without a clear reason.

## Repo conventions
- The GitLab Pages job in [.gitlab-ci.yml](.gitlab-ci.yml) copies **every** top-level file into `public/`. Don't commit drafts, notes, or secrets to the repo root.
- Keep asset folders flat: [images/](images/) and [resume/](resume/).
- Test locally by opening [index.html](index.html) directly in a browser — no dev server needed.
- Default branch is `main`; pushes to `main` trigger deploy.
