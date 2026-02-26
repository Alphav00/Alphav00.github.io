# CLAUDE.md — AI Assistant Guide for Alphav00.github.io

## Repository Overview

This is a **GitHub Pages** personal/project website hosted at `https://alphav00.github.io`. It is a static site repository using pure vanilla HTML, CSS, and JavaScript — no build tools, bundlers, or server-side infrastructure.

The repository previously hosted a gothic-themed interactive cocktail menu ("The Seven Deadly Shots") and may be repurposed for new content.

---

## Technology Stack

| Layer       | Technology                              |
|-------------|----------------------------------------|
| Markup      | HTML5 with semantic elements           |
| Styling     | CSS3 + Tailwind CSS (via CDN)          |
| Scripting   | Vanilla JavaScript (ES6+)              |
| Fonts       | Google Fonts (Inter, Playfair Display) |
| Hosting     | GitHub Pages (auto-deploy from master) |
| Build tools | None                                   |
| Package mgr | None                                   |

**There is no `package.json`, no `node_modules`, no bundler, and no build step.**

---

## Repository Structure

```
Alphav00.github.io/
├── CLAUDE.md         # This file
├── index.html        # Main entry point (GitHub Pages root)
└── (optional assets) # Images, additional CSS/JS files if added
```

Because GitHub Pages serves the `master` branch root directly:
- `index.html` is the site's homepage
- All asset paths should be relative to the repository root
- No `_site/`, `dist/`, or `build/` directories are used

---

## Development Workflow

### Editing the Site

1. Edit `index.html` (and any supporting files) directly
2. Preview locally by opening the file in a browser (`file://` protocol works for most features)
3. Commit changes to `master` — GitHub Pages deploys automatically within ~1 minute

### Local Preview

Since there is no build step, open the HTML file directly:

```bash
# On Linux
xdg-open index.html

# On macOS
open index.html

# Or use a simple local server to avoid CORS issues with some resources
python3 -m http.server 8080
# Then visit http://localhost:8080
```

### Deployment

```bash
# All commits to master are auto-deployed to GitHub Pages
git add .
git commit -m "Describe your changes"
git push origin master
```

The live site reflects changes at: `https://alphav00.github.io`

---

## Git Branch Conventions

| Branch pattern                      | Purpose                                  |
|-------------------------------------|------------------------------------------|
| `master`                            | Production branch — auto-deploys to Pages |
| `claude/<task-id>`                  | AI assistant working branches            |

- Never push directly to `master` without review when working on significant changes
- AI assistant branches follow the pattern `claude/claude-md-<session-id>`

---

## Coding Conventions

### HTML

- Use semantic HTML5 elements (`<header>`, `<main>`, `<section>`, `<nav>`, `<footer>`)
- All pages must include a proper `<meta charset="UTF-8">` and responsive viewport meta tag
- Self-close void elements optionally (`<img>`, `<br>`, `<hr>`, `<input>`)

### CSS / Tailwind

- Tailwind CSS is loaded via CDN — no installation needed
- Custom styles go in a `<style>` block in `<head>` or in a separate `.css` file
- Use Tailwind utility classes for layout and spacing; write custom CSS only for animations or things Tailwind can't handle cleanly
- Prefer CSS custom properties (`--variable-name`) for repeated theme values (colors, spacing)

### JavaScript

- Vanilla JavaScript only — no frameworks (no React, Vue, jQuery, etc.)
- Use `const` and `let`; avoid `var`
- Prefer `addEventListener` over inline `onclick` attributes
- Keep JS at the bottom of `<body>` or use `defer` attribute on `<script>` tags
- Data that drives the UI (e.g., menu items, card content) should be defined as a JavaScript object/array at the top of the script block, separate from DOM manipulation logic

### Naming

- HTML `id` and `class` attributes: use `kebab-case`
- JavaScript variables and functions: use `camelCase`
- CSS custom properties: use `--kebab-case`

---

## Styling & Theme Notes

The previous site used a **dark gothic theme** with the following design tokens (preserved here for reference if continuing that aesthetic):

```css
:root {
  --primary-red:   #B71C1C;
  --dark-bg:       #0a0a0a;
  --card-bg:       #111111;
  --text-primary:  #f5f5f5;
  --text-muted:    #9e9e9e;
  --accent-gold:   #ffd700;
}
```

Fonts used:
- **Inter** — body text, UI labels
- **Playfair Display** — headings, display text

If building a new design, feel free to replace these. If continuing the gothic/dark theme, use the tokens above for consistency.

---

## No Testing Infrastructure

There are currently **no automated tests** in this repository. This is typical for a simple static site.

If testing is added in the future, prefer:
- **Playwright** or **Cypress** for end-to-end browser tests
- **HTML validators** (e.g., W3C Validator) for markup correctness
- **Lighthouse** (via Chrome DevTools or CLI) for performance/accessibility audits

---

## Key Files Reference

| File          | Description                                     |
|---------------|-------------------------------------------------|
| `index.html`  | Site entry point, served by GitHub Pages at `/` |
| `CLAUDE.md`   | This guide for AI assistants                    |

---

## Common Tasks for AI Assistants

### Adding a new section to index.html

1. Read `index.html` in full first to understand the current structure
2. Add the new `<section>` using existing class/style conventions
3. If using Tailwind, check what breakpoints/utilities are already in use
4. Test by viewing in browser before committing

### Changing the color scheme or theme

1. Identify existing CSS custom properties or Tailwind config in `<style>` or `tailwind.config`
2. Update color values globally — avoid one-off color changes scattered through the markup
3. Check contrast ratios for accessibility (WCAG AA minimum: 4.5:1 for body text)

### Adding interactivity (JavaScript)

1. Define data separately from DOM logic
2. Use `document.querySelector` / `querySelectorAll` for element selection
3. Attach events via `addEventListener` — never inline handlers
4. Keep the script self-contained within the `<script>` block at bottom of `<body>`

---

## Out of Scope

The following are **not used** in this project and should not be introduced without explicit discussion:

- Node.js / npm / yarn / pnpm
- React, Vue, Angular, Svelte, or any JS framework
- Webpack, Vite, Parcel, or any bundler
- TypeScript
- Backend servers or APIs
- Databases
- CSS preprocessors (Sass, LESS)
