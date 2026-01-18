# EasyTeX

**The Symbolic Workspace for Serious Mathematics**

A LaTeX-native workspace that thinks like mathematicians do. Transparent derivations, expression-first design, and zero hand-holding.

![EasyTeX Banner](https://via.placeholder.com/1200x400/0d9488/ffffff?text=EasyTeX)

---

## Table of Contents

- [Overview](#overview)
- [Design Philosophy](#design-philosophy)
- [Core Principles](#core-principles)
- [Features](#features)
- [Project Structure](#project-structure)
- [Technical Implementation](#technical-implementation)
- [Accessibility](#accessibility)
- [Screenshots](#screenshots)
- [Getting Started](#getting-started)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

EasyTeX is a symbolic mathematics workspace designed specifically for researchers, mathematicians, and academics who demand precision, transparency, and power from their tools.

Unlike traditional math software that prioritizes accessibility over capability, EasyTeX treats users as experts. It provides:

- **LaTeX-first input** — type expressions directly, no clicking symbols
- **Transparent derivations** — every step shown, every assumption explicit
- **Expression-centric design** — manipulate, transform, compare, version
- **Keyboard-first interaction** — everything reachable without a mouse
- **Immutable history** — Git-like branching for mathematical reasoning

---

## Design Philosophy

### The Problem

Every existing mathematical tool fails in the same way: they prioritize accessibility over power, polish over transparency, and features over composability. The result is software that treats mathematicians like beginners who need hand-holding.

### Our Solution

EasyTeX is built on a fundamental belief: **mathematicians distrust black boxes**. Any tool that hides the math isn't a tool—it's an obstacle.

> "If your tool feels like a research notebook, a symbolic reasoning partner, and a transparent algebra system… then mathematicians will love it."

### Target Users

| Level | Description |
|-------|-------------|
| Undergraduate | Advanced math/physics students |
| Graduate | PhD candidates and researchers |
| Professional | Academic faculty, research mathematicians |

---

## Core Principles

### 1. Transparency Over Automation

```
✓ Show intermediate steps
✓ Show assumptions
✓ Show branching cases
✗ Never hide the math
```

**Anti-pattern:** "Answer: 3.14159" with no derivation.

### 2. Composability Over Features

Small, orthogonal primitives that combine:

- **Define** — create named expressions
- **Transform** — apply operations
- **Prove** — verify properties
- **Visualize** — graph and plot
- **Export** — LaTeX, PDF, code

### 3. Density Over Decoration

- Monochrome or restrained color
- High contrast math typography
- No decorative gradients, shadows, or animations
- If it feels like a scientific paper, we're doing it right

### 4. Precision Over Friendliness

| Do | Don't |
|----|-------|
| Precise language | "Friendly" tips |
| Formal terminology | Cartoon icons |
| Explicit error messages | Over-simplified explanations |

Example error message:
```
Expression undefined for x < 0 due to branch cut
```

---

## Features

### Math-Native Input

```latex
f := x^3 - 2x + 1
\int_0^\infty e^{-x^2} dx
diff(f, x)
```

- LaTeX-first input (not WYSIWYG)
- Structural editing (navigate sub-expressions)
- Instant parsing (<50ms latency)

### Expression-Centric Design

Everything revolves around **expressions as first-class objects**:

```
f := x^3 - 2x + 1    # Define
factor(f)             # Transform
roots(f)              # Analyze
plot(f, x=-2..2)      # Visualize
```

No forms. No wizards. No step-by-step constraints.

### Transparent Derivations

Toggle between views:

| View | Description |
|------|-------------|
| Full | Complete step-by-step derivation |
| Condensed | Key steps only |
| Result | Final answer |

Example derivation:
```
① Substitution    u = x² → ½∫ u^{-½} e^{-u} du
② Gamma function  = ½ Γ(½)
③ Known value     = ½ · √π = √π/2
```

### Multiple Representations

A single object has synchronized views:

- **Symbolic** — algebraic expression
- **Numeric** — computed values
- **Graphical** — plots and visualizations
- **Logical** — proof/constraint representation

Hover over part of the equation → corresponding part highlights in the graph.

### Keyboard-First Design

| Shortcut | Action |
|----------|--------|
| `Ctrl+K` | Command palette |
| `Shift+Enter` | Execute cell |
| `Ctrl+/` | Toggle derivation steps |
| `Ctrl+B` | Create branch |

- Vim/Emacs-style navigation
- Custom keybindings
- Macro recording

### Immutable History & Versioning

**Git for reasoning:**

- Every transformation is reversible
- Branch computations ("what if I assume continuity?")
- Compare derivation paths side-by-side
- Full audit trail

```
14:23  factor(f)
14:21  ⎇ assume x ∈ ℂ     ← branch point
14:19  diff(f, x)
14:15  f := x³ - 2x + 1
```

### Explicit Assumptions

Always visible in the sidebar:

```
☑ x ∈ ℝ          Domain
☑ x > 0          Constraint
☐ x ∈ ℤ          (disabled)
☑ Continuous     Property
```

**Silent assumptions destroy trust. We never hide the context.**

---

## Project Structure

```
easytex/
├── workspace/
│   ├── math-workspace.html           # Original dark theme workspace
│   ├── math-workspace-accessible.html # Accessible neutral colorways
│   └── easytex-landing.html          # Marketing landing page
├── docs/
│   └── README.md                     # This file
├── assets/
│   └── (screenshots, logos)
└── design/
    └── ux-principles.md              # Original UX specification
```

### File Descriptions

| File | Purpose |
|------|---------|
| `math-workspace.html` | Core workspace UI with dark theme, LaTeX input, cell-based layout, derivation steps, graph panel |
| `math-workspace-accessible.html` | Accessible version with 3 themes (light, dark, high-contrast), WCAG compliance, ARIA labels |
| `easytex-landing.html` | Startup landing page with hero, demo, features, philosophy, pricing, CTA |

---

## Technical Implementation

### Tech Stack

| Component | Technology |
|-----------|------------|
| Markup | Semantic HTML5 |
| Styling | CSS3 with CSS Variables |
| Math Rendering | KaTeX |
| Fonts | Cormorant Garamond (serif), IBM Plex Mono (mono), DM Sans (sans) |
| Icons | Unicode symbols |

### CSS Architecture

```css
:root {
  /* Color system */
  --bg-primary: #fafaf8;
  --bg-secondary: #f5f4f1;
  --text-primary: #1a1918;
  --accent: #0d9488;
  
  /* Typography */
  --font-serif: 'Cormorant Garamond', Georgia, serif;
  --font-mono: 'IBM Plex Mono', monospace;
  --font-sans: 'DM Sans', system-ui, sans-serif;
}
```

### Theme System

Three built-in themes with localStorage persistence:

```javascript
const themes = ['light', 'dark', 'high-contrast'];

function setTheme(theme) {
  if (theme === 'light') {
    document.documentElement.removeAttribute('data-theme');
  } else {
    document.documentElement.setAttribute('data-theme', theme);
  }
  localStorage.setItem('theme', theme);
}
```

### Layout Structure

```
┌─────────────────────────────────────────────────────────┐
│ Header (nav, command palette, actions)                  │
├────────────┬────────────────────────────┬───────────────┤
│            │                            │               │
│  Sidebar   │      Main Workspace        │  Inspector    │
│            │                            │               │
│ • Env      │  ┌──────────────────────┐  │ • Properties  │
│ • Assume   │  │ Cell [1]             │  │ • Transforms  │
│ • History  │  │ f := x^3 - 2x + 1    │  │ • Related     │
│            │  └──────────────────────┘  │               │
│            │                            │               │
│            │  ┌──────────────────────┐  │               │
│            │  │ Cell [2]             │  │               │
│            │  │ ∫₀^∞ e^{-x²} dx      │  │               │
│            │  └──────────────────────┘  │               │
│            │                            │               │
├────────────┴────────────────────────────┴───────────────┤
│ Footer (status, domain, keybinds)                       │
└─────────────────────────────────────────────────────────┘
```

---

## Accessibility

### WCAG 2.1 AA Compliance

| Feature | Implementation |
|---------|----------------|
| Color contrast | Minimum 4.5:1 for text, 3:1 for UI |
| Focus indicators | 2px solid outline on all interactive elements |
| Screen readers | ARIA labels, roles, live regions |
| Keyboard nav | Full functionality without mouse |
| Reduced motion | Respects `prefers-reduced-motion` |

### Accessibility Features

```html
<!-- Skip link -->
<a href="#main-workspace" class="skip-link">Skip to main content</a>

<!-- ARIA labels -->
<button aria-pressed="true" aria-label="x is in real numbers">

<!-- Live regions -->
<div class="cell-output" aria-live="polite">

<!-- Semantic structure -->
<article class="cell" aria-label="Cell 1">
```

### Theme Options

| Theme | Use Case |
|-------|----------|
| Light (default) | Warm neutral, reduced eye strain |
| Dark | Low-light environments |
| High Contrast | Visual impairments, WCAG AAA |

---

## Screenshots

### Workspace (Dark Theme)
```
┌─────────────────────────────────────────┐
│ ● ● ●  easytex — workspace.etx          │
├─────────────────────────────────────────┤
│ [1] f := x^3 - 2x + 1                   │
│     ─────────────────                   │
│     f(x) = x³ - 2x + 1                  │
│                                         │
│ [2] \int_0^\infty e^{-x^2} dx           │
│     ─────────────────────               │
│     ∫₀^∞ e^{-x²} dx = √π/2              │
│                                         │
│     ① Substitution  u = x² → ...        │
│     ② Gamma         = ½ Γ(½)            │
│     ③ Known         = √π/2              │
└─────────────────────────────────────────┘
```

### Landing Page Sections

1. **Hero** — Value proposition, CTA, social proof
2. **Demo** — Interactive workspace preview
3. **Features** — 6 core capabilities
4. **Philosophy** — Manifesto and principles
5. **Pricing** — 3-tier (Free / Team / Enterprise)
6. **CTA** — Email waitlist signup

---

## Getting Started

### Quick Start

1. Open `easytex-landing.html` in a browser to see the marketing site
2. Open `math-workspace-accessible.html` for the full workspace UI
3. Try the theme toggle (◐ button) to switch between light/dark/high-contrast

### Local Development

```bash
# Clone the repository
git clone https://github.com/easytex/easytex.git
cd easytex

# No build step required — just open HTML files
open workspace/math-workspace-accessible.html

# Or serve locally
python -m http.server 8000
# Visit http://localhost:8000
```

### Dependencies

All dependencies are loaded via CDN:

```html
<!-- KaTeX for math rendering -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.9/katex.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.9/katex.min.css">

<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond...&display=swap" rel="stylesheet">
```

---

## Roadmap

### Phase 1: Foundation ✅
- [x] Core workspace UI
- [x] LaTeX input with KaTeX rendering
- [x] Cell-based computation model
- [x] Derivation step display
- [x] Accessible theme system
- [x] Landing page

### Phase 2: Computation Engine
- [ ] Symbolic math backend (SymPy/Mathematica integration)
- [ ] Real-time expression parsing
- [ ] Step-by-step derivation generation
- [ ] Assumption propagation

### Phase 3: Collaboration
- [ ] Cloud sync
- [ ] Shared workspaces
- [ ] Real-time collaboration
- [ ] Comments and annotations

### Phase 4: Advanced Features
- [ ] Proof assistant integration
- [ ] Custom notation definitions
- [ ] Plugin system
- [ ] LMS integration

---

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Principles

1. **Semantic HTML** — Use appropriate elements
2. **Progressive enhancement** — Works without JS
3. **Accessibility first** — WCAG 2.1 AA minimum
4. **Performance** — No unnecessary dependencies
5. **Simplicity** — Vanilla CSS/JS where possible

### Code Style

```css
/* Use CSS variables for theming */
.element {
  color: var(--text-primary);
  background: var(--bg-secondary);
}

/* BEM-like naming */
.cell {}
.cell-input {}
.cell-output {}
.cell-status {}
```

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

## Acknowledgments

- Design principles inspired by Mathematica, Lean, Coq, and the broader CAS community
- Typography guidance from Butterick's Practical Typography
- Accessibility patterns from WAI-ARIA Authoring Practices

---

<p align="center">
  <strong>EasyTeX</strong> — Built for mathematicians who refuse to compromise.
</p>

<p align="center">
  <a href="https://easytex.io">Website</a> •
  <a href="https://docs.easytex.io">Documentation</a> •
  <a href="https://twitter.com/easytex">Twitter</a> •
  <a href="https://github.com/easytex/easytex">GitHub</a>
</p>
