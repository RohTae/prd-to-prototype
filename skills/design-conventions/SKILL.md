---
name: design-conventions
description: Project-wide design and code conventions. Auto-referenced when writing wireframes, components, or prototypes. Covers HTML, Tailwind, markdown, and naming rules.
---

# Design & Code Conventions

## Markdown Deliverable Rules

### YAML Frontmatter (required on all .md deliverables)
```yaml
---
title: "Document Title"
phase: 1-6
created: YYYY-MM-DD
status: draft | review | approved
depends_on:
  - "prior phase output path"
---
```

### Diagrams
- All flow/structure diagrams use **Mermaid** syntax
- Node text wrapped in double quotes: `A["Text"]`
- Direction: Sitemaps use TD (Top-Down), User Flows use LR (Left-Right)

## HTML Code Rules

### File Structure
All wireframes and prototypes are .html files that open directly in the browser with a double-click.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>S-001 — Screen Name</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>tailwind.config = { /* ... */ }</script>
</head>
<body>
  <div class="mobile-frame">
    <!-- Content -->
  </div>
  <script>
    // Interactions (vanilla JS only)
  </script>
</body>
</html>
```

### Tech Stack Rules
- **No build tools**: No npm, webpack, vite, etc.
- **No frameworks**: No React, Vue, Angular, etc.
- **Allowed CDN**: Tailwind CSS (`cdn.tailwindcss.com`) only
- **Icons**: Emoji or inline SVG (Lucide CDN optionally allowed)
- **Interactions**: Vanilla JavaScript only

### Tailwind Usage
- No inline styles. Tailwind classes only.
- Responsive: Use `sm:`, `md:`, `lg:` prefixes (mobile-first)
- Custom colors defined in `tailwind.config` only (no hardcoded hex values)

## Naming Rules
- Filenames: kebab-case (`user-profile.html`, `design-tokens.html`)
- Wireframe files: `S-{NNN}-{screen-name}.html` (e.g., `S-001-home.html`)
- Prototype: `prototype.html` (single file)
- JS variables/functions: camelCase (`handleClick`, `userData`)
- CSS classes: Tailwind utilities (minimize custom classes)
- Screen IDs: `S-{NNN}` format (`S-001`, `S-012`)

## Icons
- Wireframe phase: Emoji or text labels instead of icons
- Prototype phase: Emoji or inline SVG (Lucide CDN optionally allowed)
