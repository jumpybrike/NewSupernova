# SF Supernova — Product Design Specification

# 1. Layout

**Site Width:** 1200px max | 700px content (articles)

| Breakpoint | Viewport | Grid |
|------------|----------|------|
| Mobile | 320–767px | 4-col, 16px gutter |
| Tablet | 768–1023px | 8-col, 16px gutter |
| Desktop | 1024px+ | 12-col, 24px gutter |

**Spacing:** 8px base — xs(8) sm(16) md(24) lg(32) xl(48) xxl(64)

---

## 1.1 Grid System Detail

### Container Widths

| Container | Max Width | Use Case |
|-----------|-----------|----------|
| `.container-site` | 1200px | Full site wrapper, centred with auto margins |
| `.container-content` | 700px | Article body, long-form reading, legal pages |
| `.container-narrow` | 540px | Forms, modals, authentication pages |
| `.container-full` | 100% | Hero sections, full-bleed imagery |

### Column Structure

| Breakpoint | Columns | Gutter | Margin (outer) |
|------------|---------|--------|----------------|
| Mobile (320–767px) | 4 | 16px | 16px |
| Tablet (768–1023px) | 8 | 16px | 24px |
| Desktop (1024–1439px) | 12 | 24px | 32px |
| Large Desktop (1440px+) | 12 | 24px | auto (centred) |

### Column Span Reference

| Layout Pattern | Mobile | Tablet | Desktop |
|----------------|--------|--------|---------|
| Full width | 4 | 8 | 12 |
| Content area | 4 | 8 | 8 |
| Sidebar | 4 | 8 | 4 |
| Product card | 4 | 4 | 3 |
| Featured card | 4 | 4 | 4 |
| Two-column split | 4 / 4 | 4 / 4 | 6 / 6 |
| Content + sidebar | 4 / 4 | 5 / 3 | 8 / 4 |

### CSS Implementation

```css
.container-site {
  width: 100%;
  max-width: 1200px;
  margin-left: auto;
  margin-right: auto;
  padding-left: 16px;
  padding-right: 16px;
}

@media (min-width: 768px) {
  .container-site {
    padding-left: 24px;
    padding-right: 24px;
  }
}

@media (min-width: 1024px) {
  .container-site {
    padding-left: 32px;
    padding-right: 32px;
  }
}

.container-content {
  width: 100%;
  max-width: 700px;
  margin-left: auto;
  margin-right: auto;
}

.container-narrow {
  width: 100%;
  max-width: 540px;
  margin-left: auto;
  margin-right: auto;
}
```

### Grid Behaviour

**Fluid scaling:** Columns scale proportionally within breakpoint ranges. No fixed column widths—use percentage-based spans.

**Gutter consistency:** Gutters remain constant within each breakpoint. Spacing between elements uses the 8px base scale, not column gutters.

**Nesting:** Nested grids inherit parent gutter size. Avoid nesting beyond two levels to prevent excessive complexity.

**Alignment:** All grid content aligns to column edges. Text and components should not float between columns.

---
Here's the complete Section 2:

---

## 2. Typography

### 2.1 Font Families

| Role | Font Family | Weights | Fallback Stack |
|------|-------------|---------|----------------|
| **Headings** | Outfit | 400, 500, 600, 700, 800 | system-ui, sans-serif |
| **Body** | Source Serif 4 | 400, 500, 600, 700 | Georgia, 'Times New Roman', serif |
| **UI / Accent** | Space Grotesk | 400, 500, 600 | system-ui, sans-serif |

**Outfit** is a geometric sans-serif with Art Deco sensibilities—bold, confident, and distinctly retro-futurist. Its tight letterspacing and range of weights make it ideal for headlines, navigation, and UI elements requiring visual authority.

**Source Serif 4** is a variable serif optimised for screen reading. Its optical sizing (8–60pt) ensures crisp rendering at both body and display sizes, while its traditional letterforms honour book typography conventions appropriate to a literary platform.

**Space Grotesk** provides technical contrast—a monospace-influenced sans used for metadata, labels, and UI chrome. Its geometric construction complements Outfit while signalling functional, secondary information.

#### Google Fonts Embed

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;500;600;700;800&family=Source+Serif+4:opsz,wght@8..60,400;8..60,500;8..60,600;8..60,700&family=Space+Grotesk:wght@400;500;600&display=swap" rel="stylesheet">
```

### 2.2 Type Scale

Base size: **16px** (1rem)

| Token | Size (px) | Size (rem) | Font | Weight | Use Case |
|-------|-----------|------------|------|--------|----------|
| `text-xs` | 12 | 0.75 | Space Grotesk | 600 | Section labels, tags, timestamps |
| `text-sm` | 14 | 0.875 | Source Serif 4 / Space Grotesk | 400 | Captions, citations, metadata |
| `text-base` | 16 | 1 | Source Serif 4 | 400 | Body text, form labels |
| `text-lg` | 18 | 1.125 | Source Serif 4 | 400 | Article body, lead paragraphs |
| `text-xl` | 20 | 1.25 | Outfit | 500–600 | H4, card titles, navigation |
| `text-2xl` | 24 | 1.5 | Outfit | 600–700 | H3, product titles, blockquotes |
| `text-3xl` | 28 | 1.75 | Outfit | 700 | H3 prominent |
| `text-4xl` | 36 | 2.25 | Outfit | 700 | H2, section headings |
| `text-5xl` | 48 | 3 | Outfit | 800 | H1, page titles |
| `text-6xl` | 56 | 3.5 | Outfit | 800 | Hero headings |

### 2.3 Line Heights & Spacing

| Context | Line Height | Letter Spacing |
|---------|-------------|----------------|
| **Hero / Display** (text-5xl, text-6xl) | 1.1 | -1px |
| **Headings** (text-3xl, text-4xl) | 1.2 | -0.5px |
| **Subheadings** (text-xl, text-2xl) | 1.3 | 0 |
| **Body** (text-base, text-lg) | 1.75 | 0 |
| **Small text** (text-sm, text-xs) | 1.5 | 0 |
| **Labels / Tags** (uppercase) | 1.2 | 2px |

**Paragraph spacing:** `margin-bottom: 1.5em` (24px at 16px base). No `margin-top` on paragraphs.

**Heading spacing:** `margin-top: 2em`, `margin-bottom: 0.75em`. Creates separation above while maintaining connection to following content.

**Maximum line length:** 65–75 characters. The `.container-content` (700px) achieves this at 18px body size.

### 2.4 Responsive Typography

| Token | Mobile (320–767px) | Tablet (768–1023px) | Desktop (1024px+) |
|-------|-------------------|---------------------|-------------------|
| `text-6xl` | 36px | 48px | 56px |
| `text-5xl` | 32px | 40px | 48px |
| `text-4xl` | 28px | 32px | 36px |
| `text-3xl` | 24px | 26px | 28px |
| `text-2xl` | 20px | 22px | 24px |
| `text-xl` | 18px | 20px | 20px |
| `text-lg` | 17px | 18px | 18px |
| `text-base` | 16px | 16px | 16px |
| `text-sm` | 14px | 14px | 14px |
| `text-xs` | 12px | 12px | 12px |

Display and heading sizes scale across breakpoints; body and small text remain constant.

### 2.5 Application Reference

| Element | Font | Weight | Size | Colour |
|---------|------|--------|------|--------|
| Logo | Outfit | 700 | 24px | Surface 200 on dark / Neutral 900 on light |
| Navigation | Outfit | 500 | 15px | Teal 200, hover Surface 200 |
| Hero H1 | Outfit | 800 | 56px (responsive) | Surface 200 |
| Hero tagline | Source Serif 4 | 400 italic | 20px | Teal 200 |
| Section label | Space Grotesk | 600 | 12px uppercase | Deep Teal |
| H2 | Outfit | 700 | 36px | Neutral 900 |
| H3 | Outfit | 700 | 28px | Neutral 900 |
| Body paragraph | Source Serif 4 | 400 | 18px | Neutral 600 |
| Blockquote | Outfit | 500 | 24px | Deep Teal |
| Blockquote citation | Space Grotesk | 400 | 14px | Neutral 500 |
| Product card title | Outfit | 600 | – | Neutral 900 |
| Product metadata | Source Serif 4 | 400 | – | Neutral 600 |
| Tag | Space Grotesk | 600 | 11px uppercase | Deep Teal / Amber |
| Button | Outfit | 600 | 16px | per button variant |
| Footer links | Outfit | 500 | 14px | Teal 200 |

### CSS Implementation

```css
:root {
  /* Font families */
  --font-heading: 'Outfit', system-ui, sans-serif;
  --font-body: 'Source Serif 4', Georgia, 'Times New Roman', serif;
  --font-ui: 'Space Grotesk', system-ui, sans-serif;
  
  /* Type scale (mobile-first) */
  --text-xs: 0.75rem;
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.0625rem;
  --text-xl: 1.125rem;
  --text-2xl: 1.25rem;
  --text-3xl: 1.5rem;
  --text-4xl: 1.75rem;
  --text-5xl: 2rem;
  --text-6xl: 2.25rem;
  
  /* Line heights */
  --leading-display: 1.1;
  --leading-heading: 1.2;
  --leading-subheading: 1.3;
  --leading-body: 1.75;
  --leading-small: 1.5;
}

@media (min-width: 768px) {
  :root {
    --text-lg: 1.125rem;
    --text-xl: 1.25rem;
    --text-2xl: 1.375rem;
    --text-3xl: 1.625rem;
    --text-4xl: 2rem;
    --text-5xl: 2.5rem;
    --text-6xl: 3rem;
  }
}

@media (min-width: 1024px) {
  :root {
    --text-2xl: 1.5rem;
    --text-3xl: 1.75rem;
    --text-4xl: 2.25rem;
    --text-5xl: 3rem;
    --text-6xl: 3.5rem;
  }
}

body {
  font-family: var(--font-body);
  font-size: var(--text-lg);
  line-height: var(--leading-body);
  color: var(--neutral-600);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-heading);
  color: var(--neutral-900);
  margin-top: 2em;
  margin-bottom: 0.75em;
}

h1 {
  font-size: var(--text-5xl);
  font-weight: 800;
  line-height: var(--leading-display);
  letter-spacing: -1px;
}

h2 {
  font-size: var(--text-4xl);
  font-weight: 700;
  line-height: var(--leading-heading);
  letter-spacing: -0.5px;
}

h3 {
  font-size: var(--text-3xl);
  font-weight: 700;
  line-height: var(--leading-heading);
}

h4 {
  font-size: var(--text-xl);
  font-weight: 600;
  line-height: var(--leading-subheading);
}

p {
  margin-bottom: 1.5em;
}

.section-label {
  font-family: var(--font-ui);
  font-size: var(--text-xs);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: var(--teal-600);
}

blockquote {
  font-family: var(--font-heading);
  font-size: var(--text-2xl);
  font-weight: 500;
  line-height: var(--leading-subheading);
  color: var(--teal-600);
  border-left: 4px solid var(--amber-500);
  padding-left: 24px;
  margin: 32px 0;
}

blockquote cite {
  display: block;
  font-family: var(--font-ui);
  font-size: var(--text-sm);
  font-weight: 400;
  color: var(--neutral-500);
  margin-top: 12px;
}
```

### Tailwind Extension

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    fontFamily: {
      heading: ['Outfit', 'system-ui', 'sans-serif'],
      body: ['Source Serif 4', 'Georgia', 'Times New Roman', 'serif'],
      ui: ['Space Grotesk', 'system-ui', 'sans-serif'],
    },
    extend: {
      fontSize: {
        'xs': ['0.75rem', { lineHeight: '1.5' }],
        'sm': ['0.875rem', { lineHeight: '1.5' }],
        'base': ['1rem', { lineHeight: '1.75' }],
        'lg': ['1.125rem', { lineHeight: '1.75' }],
        'xl': ['1.25rem', { lineHeight: '1.3' }],
        '2xl': ['1.5rem', { lineHeight: '1.3' }],
        '3xl': ['1.75rem', { lineHeight: '1.2' }],
        '4xl': ['2.25rem', { lineHeight: '1.2' }],
        '5xl': ['3rem', { lineHeight: '1.1' }],
        '6xl': ['3.5rem', { lineHeight: '1.1' }],
      },
    },
  },
}
```
---

## 3. Colour

The Cartographer palette establishes SF Supernova's visual identity—warm, scholarly, and evocative of aged paper, celestial navigation, and vintage pulp aesthetics. Full colour definitions are maintained in Pallette.md; this section specifies application patterns.

### 3.1 Core Palette Reference

| Name | Hex | Role |
|------|-----|------|
| **Star Chart** | #F4F1E8 | Primary background (Surface 200) |
| **Vellum** | #E8E3D6 | Cards, elevated surfaces (Surface 300) |
| **Deep Teal** | #1A4A4A | Primary brand, buttons, links (Teal 600) |
| **Amber** | #C9943A | Warm accent, featured actions (Amber 500) |
| **Night Sky** | #1A3535 | Primary text, dark surfaces (Teal 900) |

### 3.2 Colour Application

#### Backgrounds

| Context | Colour | Token |
|---------|--------|-------|
| Page background | #F4F1E8 | `--surface-200` / `--bg-page` |
| Card / elevated surface | #E8E3D6 | `--surface-300` / `--bg-card` |
| Modal overlay background | #FDFCF9 | `--surface-50` |
| Input fields | #FDFCF9 | `--surface-50` |
| Header / footer | #0F3333 | `--teal-900` |
| Hero sections | #0F3333 → #1A4A4A | gradient |
| Hover highlight | #F9F6F0 | `--surface-100` |

#### Text

| Context | Colour | Token | Contrast on Surface 200 |
|---------|--------|-------|-------------------------|
| Primary text (headings) | #1A2020 | `--neutral-900` | 12.4:1 (AAA) |
| Body text | #4D5858 | `--neutral-600` | 6.8:1 (AA) |
| Secondary text | #667272 | `--neutral-500` | 4.8:1 (AA large) |
| Muted text | #8A9494 | `--neutral-400` | 3.5:1 (decorative only) |
| Links | #1A4A4A | `--teal-600` | 7.2:1 (AAA) |
| Link hover | #153D3D | `--teal-700` | 8.9:1 (AAA) |

#### Text on Dark Backgrounds

| Context | Colour | Token | Contrast on Teal 900 |
|---------|--------|-------|----------------------|
| Primary text | #F4F1E8 | `--surface-200` | 10.1:1 (AAA) |
| Secondary text | #B8DADA | `--teal-200` | 7.8:1 (AAA) |
| Muted text | #7DBDBD | `--teal-300` | 5.2:1 (AA) |
| Accent | #C9943A | `--amber-500` | 6.4:1 (AA) |

#### Interactive Elements

| Element | Default | Hover | Active | Disabled |
|---------|---------|-------|--------|----------|
| **Primary button** | Teal 600 bg, Surface 200 text | Teal 700 bg | Teal 800 bg | Neutral 300 bg, Neutral 500 text |
| **Accent button** | Amber 500 bg, Teal 900 text | Amber 400 bg | Amber 600 bg | Neutral 300 bg, Neutral 500 text |
| **Secondary button** | Transparent bg, Teal 600 border/text | Teal 50 bg | Teal 100 bg | Neutral 300 border, Neutral 500 text |
| **Ghost button** | Transparent bg, Amber 300 border | Amber 50 bg | Amber 100 bg | Neutral 300 border, Neutral 500 text |
| **Text link** | Teal 600 | Teal 700, underline | Teal 800 | Neutral 400 |
| **Nav link (dark bg)** | Teal 200 | Surface 200 | Surface 200 | Teal 400 |

#### Borders & Dividers

| Context | Colour | Token |
|---------|--------|-------|
| Card border | #DDD5C4 | `--surface-400` |
| Input border | #C5CBCB | `--neutral-200` |
| Input border (focus) | #1A4A4A | `--teal-600` |
| Divider (light bg) | #E0E4E4 | `--neutral-100` |
| Divider (dark bg) | #264545 | `--teal-700` |
| Blockquote border | #C9943A | `--amber-500` |

### 3.3 Semantic Colour Usage

#### Status States

| State | Background | Border | Text | Icon |
|-------|------------|--------|------|------|
| **Success** | #ECF7F2 | #A8DCBE | #1A5C38 | #1A5C38 |
| **Warning** | #FDF8EB | #F0D49E | #7A4D15 | #7A4D15 |
| **Error** | #FDF2F2 | #F0B8B8 | #8B2020 | #8B2020 |
| **Info** | #E5F2F2 | #7DBDBD | #1A4A4A | #1A4A4A |

#### Form Validation

| State | Border | Background | Text |
|-------|--------|------------|------|
| Default | Neutral 200 | Surface 50 | Neutral 600 |
| Focus | Teal 600 (2px) | Surface 50 | Neutral 900 |
| Valid | Success border | Success bg | Success text |
| Invalid | Error border | Error bg | Error text |
| Disabled | Neutral 200 | Neutral 100 | Neutral 400 |

#### Tags & Badges

| Variant | Background | Text | Use Case |
|---------|------------|------|----------|
| Default | Teal 50 | Teal 700 | Categories, genres |
| Amber | Amber 100 | Amber 800 | Featured, highlights |
| Neutral | Neutral 100 | Neutral 700 | Metadata, counts |
| Success | Success bg | Success text | Available, in stock |
| Warning | Warning bg | Warning text | Limited, ending soon |
| Error | Error bg | Error text | Sold out, unavailable |

### 3.4 Dark Surface Patterns

Dark surfaces use Teal 800 (#153D3D) or Teal 900 (#0F3333) and appear in:
- Site header
- Site footer
- Hero sections
- Feature callout blocks
- Modal overlays (semi-transparent)

#### Dark Surface Colour Mapping

| Element | Colour | Token |
|---------|--------|-------|
| Background | #0F3333 | `--teal-900` |
| Background (elevated) | #153D3D | `--teal-800` |
| Primary text | #F4F1E8 | `--surface-200` |
| Secondary text | #B8DADA | `--teal-200` |
| Muted text | #7DBDBD | `--teal-300` |
| Border / divider | #264545 | `--teal-700` |
| Accent highlight | #C9943A | `--amber-500` |
| Primary button | Amber 500 bg, Teal 900 text | — |
| Secondary button | Teal 400 border, Surface 200 text | — |
| Link | Teal 200, hover Surface 200 | — |

#### Gradient Patterns

```css
/* Hero gradient */
.hero-gradient {
  background: linear-gradient(135deg, #0F3333 0%, #1A4A4A 100%);
}

/* Feature block gradient */
.feature-gradient {
  background: linear-gradient(180deg, #153D3D 0%, #0F3333 100%);
}

/* Overlay gradient (for text on images) */
.image-overlay {
  background: linear-gradient(180deg, transparent 0%, rgba(15, 51, 51, 0.9) 100%);
}
```

### 3.5 Decorative Colour

Filigree colours are strictly ornamental—used for borders, chapter dividers, and document embellishment. Never use for interactive elements, status indicators, or text.

| Token | Hex | Use |
|-------|-----|-----|
| `--filigree-50` | #FDF8EB | Subtle warm background tint |
| `--filigree-100` | #F8ECD0 | Decorative border fills |
| `--filigree-200` | #E5C87A | Ornamental line work |
| `--filigree-300` | #C9943A | Decorative accents (same as Amber 500) |

### 3.6 Colour Don'ts

- **Don't** use Amber for body text—contrast insufficient on light backgrounds
- **Don't** use Neutral 400 or lighter for essential text—fails WCAG AA
- **Don't** use pure white (#FFFFFF) for backgrounds—use Surface scale instead
- **Don't** use Filigree colours for buttons, links, or status indicators
- **Don't** mix warm and cool greys—stick to Neutral scale (umber-shifted)
- **Don't** use Teal 600 text on Teal backgrounds—insufficient contrast

### CSS Custom Properties

```css
:root {
  /* Core palette */
  --teal-900: #0F3333;
  --teal-800: #153D3D;
  --teal-700: #264545;
  --teal-600: #1A4A4A;
  --teal-500: #2D6B6B;
  --teal-400: #4A9999;
  --teal-300: #7DBDBD;
  --teal-200: #B8DADA;
  --teal-100: #D9EDED;
  --teal-50: #E5F2F2;

  --amber-900: #5C3A10;
  --amber-800: #7A4D15;
  --amber-700: #996520;
  --amber-600: #B87D2A;
  --amber-500: #C9943A;
  --amber-400: #D9A854;
  --amber-300: #E5BC70;
  --amber-200: #F0D49E;
  --amber-100: #F8E8C8;
  --amber-50: #FDF6EB;

  --surface-0: #FFFFFF;
  --surface-50: #FDFCF9;
  --surface-100: #F9F6F0;
  --surface-200: #F4F1E8;
  --surface-300: #E8E3D6;
  --surface-400: #DDD5C4;
  --surface-500: #C9BFA8;

  --neutral-900: #1A2020;
  --neutral-800: #262D2D;
  --neutral-700: #364040;
  --neutral-600: #4D5858;
  --neutral-500: #667272;
  --neutral-400: #8A9494;
  --neutral-300: #A8B0B0;
  --neutral-200: #C5CBCB;
  --neutral-100: #E0E4E4;
  --neutral-50: #F2F4F4;

  /* Semantic states */
  --success-bg: #ECF7F2;
  --success-border: #A8DCBE;
  --success-text: #1A5C38;

  --warning-bg: #FDF8EB;
  --warning-border: #F0D49E;
  --warning-text: #7A4D15;

  --error-bg: #FDF2F2;
  --error-border: #F0B8B8;
  --error-text: #8B2020;

  --info-bg: #E5F2F2;
  --info-border: #7DBDBD;
  --info-text: #1A4A4A;

  /* Filigree */
  --filigree-50: #FDF8EB;
  --filigree-100: #F8ECD0;
  --filigree-200: #E5C87A;
  --filigree-300: #C9943A;

  /* Semantic aliases */
  --color-primary: var(--teal-600);
  --color-primary-hover: var(--teal-700);
  --color-accent: var(--amber-500);
  --color-accent-hover: var(--amber-400);
  
  --bg-page: var(--surface-200);
  --bg-card: var(--surface-300);
  --bg-dark: var(--teal-900);
  
  --text-primary: var(--neutral-900);
  --text-secondary: var(--neutral-600);
  --text-muted: var(--neutral-500);
  --text-on-dark: var(--surface-200);
}
```
---

## 4. Iconography

### 4.1 Icon System

**Library:** Lucide Icons (https://lucide.dev)

Lucide is a fork of Feather Icons offering a consistent, open-source icon set with clean geometric construction. Its 1.5px stroke weight and rounded terminals complement Outfit's geometric forms and Space Grotesk's technical precision.

**Why Lucide:**
- Geometric, minimal aesthetic aligned with retro-futurist brand
- Consistent 24×24 grid with 1.5px stroke
- MIT licensed, actively maintained
- Tree-shakeable (import only icons used)
- Available as SVG, React, Vue, and web components

#### Installation

```bash
# npm
npm install lucide-react

# or CDN for static HTML
<script src="https://unpkg.com/lucide@latest"></script>
```

#### React Usage

```jsx
import { Search, ShoppingCart, User, ChevronDown } from 'lucide-react';

<Search size={20} strokeWidth={1.5} />
<ShoppingCart size={20} strokeWidth={1.5} />
```

#### SVG Usage

```html
<svg 
  xmlns="http://www.w3.org/2000/svg" 
  width="20" 
  height="20" 
  viewBox="0 0 24 24" 
  fill="none" 
  stroke="currentColor" 
  stroke-width="1.5" 
  stroke-linecap="round" 
  stroke-linejoin="round"
>
  <circle cx="11" cy="11" r="8"/>
  <path d="m21 21-4.3-4.3"/>
</svg>
```

### 4.2 Icon Sizes

| Token | Size | Stroke | Use Case |
|-------|------|--------|----------|
| `icon-xs` | 14px | 1.5px | Inline text, badges, tight spaces |
| `icon-sm` | 16px | 1.5px | Buttons (small), form hints, metadata |
| `icon-md` | 20px | 1.5px | Navigation, buttons (default), form fields |
| `icon-lg` | 24px | 1.5px | Section headers, feature highlights |
| `icon-xl` | 32px | 1.5px | Empty states, onboarding, hero elements |
| `icon-2xl` | 48px | 2px | Marketing features, large empty states |

**Sizing principle:** Icons should match the x-height or cap-height of adjacent text. When paired with `text-base` (16px), use `icon-md` (20px).

#### Touch Target Compliance

Icons used as interactive elements must meet 44×44px minimum touch target (WCAG AAA). Apply padding to achieve this:

```css
.icon-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 44px;
  min-height: 44px;
  padding: 12px; /* (44 - 20) / 2 = 12px padding for icon-md */
}
```

### 4.3 Icon Colour

Icons inherit `currentColor` by default, ensuring they match surrounding text.

| Context | Colour | Token |
|---------|--------|-------|
| Body text context | Neutral 600 | `--neutral-600` |
| Heading context | Neutral 900 | `--neutral-900` |
| Primary action | Deep Teal | `--teal-600` |
| On dark background | Surface 200 | `--surface-200` |
| Secondary (dark bg) | Teal 200 | `--teal-200` |
| Accent / highlight | Amber 500 | `--amber-500` |
| Success | Success text | `--success-text` |
| Warning | Warning text | `--warning-text` |
| Error | Error text | `--error-text` |
| Disabled | Neutral 400 | `--neutral-400` |

### 4.4 Core Icon Set

#### Navigation & UI

| Icon | Lucide Name | Use Case |
|------|-------------|----------|
| Search | `Search` | Global search, filter search |
| Menu | `Menu` | Mobile hamburger |
| Close | `X` | Modal close, dismiss |
| Chevron Down | `ChevronDown` | Dropdowns, accordions |
| Chevron Right | `ChevronRight` | Breadcrumbs, list navigation |
| Arrow Left | `ArrowLeft` | Back navigation |
| Arrow Right | `ArrowRight` | Forward, continue |
| External Link | `ExternalLink` | External URLs |
| Home | `Home` | Home navigation |

#### User & Account

| Icon | Lucide Name | Use Case |
|------|-------------|----------|
| User | `User` | Account, profile |
| Log In | `LogIn` | Sign in action |
| Log Out | `LogOut` | Sign out action |
| Settings | `Settings` | Account settings |
| Heart | `Heart` | Wishlist (outline) |
| Heart (filled) | `Heart` (fill prop) | Wishlisted item |
| Bookmark | `Bookmark` | Save for later |
| History | `History` | Reading history |

#### Commerce

| Icon | Lucide Name | Use Case |
|------|-------------|----------|
| Shopping Cart | `ShoppingCart` | Cart |
| Credit Card | `CreditCard` | Payment |
| Gift | `Gift` | Gift cards, gift membership |
| Tag | `Tag` | Pricing, discounts |
| Percent | `Percent` | Member discount |
| Download | `Download` | Download files |
| Package | `Package` | Orders |

#### Content & Media

| Icon | Lucide Name | Use Case |
|------|-------------|----------|
| Book Open | `BookOpen` | Ebooks, reading |
| Headphones | `Headphones` | Audiobooks |
| Radio | `Radio` | Radio dramas |
| File Text | `FileText` | Articles, documents |
| Image | `Image` | Cover art |
| Play | `Play` | Audio/video play |
| Pause | `Pause` | Audio/video pause |
| Volume 2 | `Volume2` | Audio volume |

#### Discovery & Filtering

| Icon | Lucide Name | Use Case |
|------|-------------|----------|
| Filter | `Filter` | Filter controls |
| Sliders | `SlidersHorizontal` | Advanced filters |
| Grid | `Grid3x3` | Grid view |
| List | `List` | List view |
| Calendar | `Calendar` | Era, date filtering |
| Clock | `Clock` | Reading time, recent |
| Sparkles | `Sparkles` | Featured, new |
| Star | `Star` | Ratings, essentials |
| Award | `Award` | Awards, accolades |

#### Communication & Feedback

| Icon | Lucide Name | Use Case |
|------|-------------|----------|
| Mail | `Mail` | Email, newsletter |
| Send | `Send` | Submit, send |
| Check | `Check` | Success, complete |
| Check Circle | `CheckCircle` | Confirmed, validated |
| Alert Circle | `AlertCircle` | Warning |
| Alert Triangle | `AlertTriangle` | Error, caution |
| Info | `Info` | Information, help |
| Help Circle | `HelpCircle` | Tooltips, FAQ |
| Loader | `Loader2` | Loading (animated) |

#### Social

| Icon | Lucide Name | Use Case |
|------|-------------|----------|
| Share | `Share2` | Share content |
| Twitter | `Twitter` | Twitter/X link |
| Facebook | `Facebook` | Facebook link |
| Rss | `Rss` | RSS feed |

### 4.5 Icon Usage Guidelines

#### Do

- **Use icons to support text**, not replace it (except universally understood: search, cart, close)
- **Maintain consistent sizing** within contexts—don't mix sizes arbitrarily
- **Use `currentColor`** to ensure icons adapt to text colour
- **Provide `aria-label`** for icon-only buttons
- **Align icons vertically** with text baseline or centre

#### Don't

- **Don't use icons decoratively** without clear meaning
- **Don't use multiple icon libraries**—stick to Lucide throughout
- **Don't modify stroke width** per-icon—maintain 1.5px consistency
- **Don't use filled icons** except for toggle states (e.g., wishlisted heart)
- **Don't rely on colour alone** to convey meaning—pair with text or shape

#### Icon + Text Pairing

```html
<!-- Button with icon -->
<button class="btn btn-primary">
  <svg class="icon-md"><!-- ShoppingCart --></svg>
  <span>Add to Cart</span>
</button>

<!-- Icon spacing: 8px gap between icon and text -->
```

```css
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px; /* --spacing-xs */
}
```

#### Icon-Only Buttons

Icon-only buttons require `aria-label` for accessibility:

```html
<!-- Accessible icon button -->
<button aria-label="Search" class="icon-button">
  <svg class="icon-md"><!-- Search --></svg>
</button>

<!-- With tooltip for sighted users -->
<button aria-label="Close modal" title="Close" class="icon-button">
  <svg class="icon-md"><!-- X --></svg>
</button>
```

### 4.6 CSS Implementation

```css
:root {
  /* Icon sizes */
  --icon-xs: 14px;
  --icon-sm: 16px;
  --icon-md: 20px;
  --icon-lg: 24px;
  --icon-xl: 32px;
  --icon-2xl: 48px;
}

/* Base icon styling */
.icon {
  display: inline-block;
  width: 1em;
  height: 1em;
  stroke: currentColor;
  stroke-width: 1.5;
  stroke-linecap: round;
  stroke-linejoin: round;
  fill: none;
  vertical-align: middle;
}

/* Size variants */
.icon-xs { width: var(--icon-xs); height: var(--icon-xs); }
.icon-sm { width: var(--icon-sm); height: var(--icon-sm); }
.icon-md { width: var(--icon-md); height: var(--icon-md); }
.icon-lg { width: var(--icon-lg); height: var(--icon-lg); }
.icon-xl { width: var(--icon-xl); height: var(--icon-xl); }
.icon-2xl { 
  width: var(--icon-2xl); 
  height: var(--icon-2xl); 
  stroke-width: 2;
}

/* Icon button (touch-target compliant) */
.icon-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 44px;
  min-height: 44px;
  padding: 10px;
  background: transparent;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  color: var(--neutral-600);
  transition: color 0.2s, background-color 0.2s;
}

.icon-button:hover {
  color: var(--teal-600);
  background-color: var(--surface-100);
}

.icon-button:focus-visible {
  outline: 2px solid var(--amber-500);
  outline-offset: 2px;
}

/* Loading spinner animation */
@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.icon-spinner {
  animation: spin 1s linear infinite;
}
```

### 4.7 Tailwind Extension

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      spacing: {
        'icon-xs': '14px',
        'icon-sm': '16px',
        'icon-md': '20px',
        'icon-lg': '24px',
        'icon-xl': '32px',
        'icon-2xl': '48px',
      },
    },
  },
}
```

Usage with Tailwind:

```html
<svg class="w-5 h-5 stroke-current stroke-[1.5]"><!-- 20px icon --></svg>
<svg class="w-6 h-6 stroke-current stroke-[1.5]"><!-- 24px icon --></svg>
```
---

## 5. Components

### 5.1 Buttons

#### Button Hierarchy

| Type | Background | Border | Text | Use Case |
|------|------------|--------|------|----------|
| **Primary** | Teal 600 | none | Surface 200 | Main CTA: Add to Cart, Checkout, Subscribe |
| **Accent** | Amber 500 | none | Teal 900 | Featured actions: Join Now, Get Started (use sparingly) |
| **Secondary** | transparent | 2px Teal 600 | Teal 600 | Secondary actions: Continue Shopping, Learn More |
| **Ghost** | transparent | 1px Surface 400 | Neutral 600 | Tertiary actions: Cancel, Back, Skip |
| **Danger** | Error bg | 1px Error border | Error text | Destructive: Remove, Delete, Cancel Membership |

#### Button Sizes

| Size | Height | Padding (x) | Font Size | Icon Size | Use Case |
|------|--------|-------------|-----------|-----------|----------|
| **Large** | 48px | 28px | 16px | 20px | Primary CTAs, mobile touch targets |
| **Medium** | 40px | 24px | 16px | 20px | Default desktop buttons |
| **Small** | 32px | 16px | 14px | 16px | Inline actions, table rows, tight spaces |

#### Button States

| State | Primary | Secondary | Ghost |
|-------|---------|-----------|-------|
| **Default** | Teal 600 bg | Teal 600 border | Surface 400 border |
| **Hover** | Teal 700 bg | Teal 50 bg | Surface 100 bg |
| **Active** | Teal 800 bg | Teal 100 bg | Surface 200 bg |
| **Focus** | 2px Amber 500 outline, 2px offset | 2px Amber 500 outline | 2px Amber 500 outline |
| **Disabled** | Neutral 300 bg, Neutral 500 text | Neutral 300 border, Neutral 400 text | Neutral 300 border, Neutral 400 text |
| **Loading** | Teal 600 bg, spinner icon, "Loading…" | — | — |

#### Button Anatomy

```
┌─────────────────────────────────────┐
│  [icon]  Label Text  [trailing]     │
│    ↑         ↑            ↑         │
│  8px gap   center     8px gap       │
└─────────────────────────────────────┘
     └──────── 24px padding ────────┘
```

#### CSS Implementation

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  font-family: var(--font-heading);
  font-weight: 600;
  font-size: 16px;
  line-height: 1;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.2s, border-color 0.2s, color 0.2s;
}

.btn:focus-visible {
  outline: 2px solid var(--amber-500);
  outline-offset: 2px;
}

/* Sizes */
.btn-lg { height: 48px; padding: 0 28px; }
.btn-md { height: 40px; padding: 0 24px; }
.btn-sm { height: 32px; padding: 0 16px; font-size: 14px; }

/* Primary */
.btn-primary {
  background-color: var(--teal-600);
  border: none;
  color: var(--surface-200);
}
.btn-primary:hover { background-color: var(--teal-700); }
.btn-primary:active { background-color: var(--teal-800); }

/* Accent */
.btn-accent {
  background-color: var(--amber-500);
  border: none;
  color: var(--teal-900);
}
.btn-accent:hover { background-color: var(--amber-400); }
.btn-accent:active { background-color: var(--amber-600); }

/* Secondary */
.btn-secondary {
  background-color: transparent;
  border: 2px solid var(--teal-600);
  color: var(--teal-600);
}
.btn-secondary:hover { background-color: var(--teal-50); }
.btn-secondary:active { background-color: var(--teal-100); }

/* Ghost */
.btn-ghost {
  background-color: transparent;
  border: 1px solid var(--surface-400);
  color: var(--neutral-600);
}
.btn-ghost:hover { background-color: var(--surface-100); }
.btn-ghost:active { background-color: var(--surface-200); }

/* Disabled (all variants) */
.btn:disabled {
  background-color: var(--neutral-300);
  border-color: var(--neutral-300);
  color: var(--neutral-500);
  cursor: not-allowed;
}

/* Loading state */
.btn-loading {
  pointer-events: none;
}
.btn-loading .btn-spinner {
  animation: spin 1s linear infinite;
}
```

#### Button on Dark Backgrounds

| Type | Background | Border | Text |
|------|------------|--------|------|
| **Primary** | Amber 500 | none | Teal 900 |
| **Secondary** | transparent | 2px Teal 400 | Surface 200 |
| **Ghost** | transparent | 1px Teal 600 | Teal 200 |

---

### 5.2 Form Inputs

#### Input Sizes

| Size | Height | Font Size | Use Case |
|------|--------|-----------|----------|
| **Large** | 48px | 16px | Mobile forms, prominent inputs |
| **Medium** | 40px | 16px | Default desktop inputs |
| **Small** | 32px | 14px | Compact forms, filters |

#### Input States

| State | Border | Background | Label | Helper/Error |
|-------|--------|------------|-------|--------------|
| **Default** | Neutral 200 | Surface 50 | Neutral 600 | Neutral 500 |
| **Hover** | Neutral 300 | Surface 50 | Neutral 600 | — |
| **Focus** | 2px Teal 600 | Surface 0 | Teal 600 | — |
| **Filled** | Neutral 200 | Surface 50 | Neutral 600 | — |
| **Valid** | Success border | Success bg (subtle) | Neutral 600 | Success text |
| **Invalid** | Error border | Error bg (subtle) | Error text | Error text |
| **Disabled** | Neutral 200 | Neutral 100 | Neutral 400 | Neutral 400 |

#### Input Anatomy

```
Label *                          ← Outfit 500, 14px, Neutral 700
┌─────────────────────────────┐
│ Placeholder text            │  ← Source Serif 4, 16px, Neutral 400
└─────────────────────────────┘
Helper text or error message     ← Space Grotesk, 12px, Neutral 500 / Error text
```

#### Field Types

**Text Input**
```html
<div class="form-field">
  <label for="email">Email Address <span class="required">*</span></label>
  <input type="email" id="email" placeholder="you@example.com" />
  <span class="helper">We'll never share your email</span>
</div>
```

**Textarea**
```html
<div class="form-field">
  <label for="message">Message</label>
  <textarea id="message" rows="4" placeholder="Your message..."></textarea>
  <span class="helper">Maximum 500 characters</span>
</div>
```

**Select**
```html
<div class="form-field">
  <label for="era">Era</label>
  <div class="select-wrapper">
    <select id="era">
      <option value="">Select an era...</option>
      <option value="1920s">1920s – Early Pulps</option>
      <option value="1930s">1930s – Golden Age Begins</option>
    </select>
    <ChevronDown class="select-icon" />
  </div>
</div>
```

**Checkbox**
```html
<label class="checkbox">
  <input type="checkbox" />
  <span class="checkbox-box"></span>
  <span class="checkbox-label">Subscribe to newsletter</span>
</label>
```

**Radio Group**
```html
<fieldset class="radio-group">
  <legend>Preferred format</legend>
  <label class="radio">
    <input type="radio" name="format" value="epub" />
    <span class="radio-dot"></span>
    <span class="radio-label">ePub</span>
  </label>
  <label class="radio">
    <input type="radio" name="format" value="pdf" />
    <span class="radio-dot"></span>
    <span class="radio-label">PDF</span>
  </label>
</fieldset>
```

#### Validation Pattern

**Inline validation:** Validate on blur (when user leaves field). Show error immediately.

```html
<div class="form-field is-invalid">
  <label for="email">Email Address <span class="required">*</span></label>
  <input 
    type="email" 
    id="email" 
    value="invalid-email"
    aria-invalid="true"
    aria-describedby="email-error"
  />
  <span id="email-error" class="error" role="alert">
    <AlertCircle size={14} />
    Please enter a valid email address
  </span>
</div>
```

#### CSS Implementation

```css
.form-field {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-field label {
  font-family: var(--font-heading);
  font-size: 14px;
  font-weight: 500;
  color: var(--neutral-700);
}

.form-field .required {
  color: var(--error-text);
}

.form-field input,
.form-field textarea,
.form-field select {
  font-family: var(--font-body);
  font-size: 16px;
  height: 40px;
  padding: 0 12px;
  background-color: var(--surface-50);
  border: 1px solid var(--neutral-200);
  border-radius: 6px;
  color: var(--neutral-900);
  transition: border-color 0.2s, background-color 0.2s;
}

.form-field textarea {
  height: auto;
  padding: 12px;
  resize: vertical;
}

.form-field input::placeholder,
.form-field textarea::placeholder {
  color: var(--neutral-400);
}

.form-field input:hover,
.form-field textarea:hover {
  border-color: var(--neutral-300);
}

.form-field input:focus,
.form-field textarea:focus {
  outline: none;
  border: 2px solid var(--teal-600);
  background-color: var(--surface-0);
}

.form-field .helper {
  font-family: var(--font-ui);
  font-size: 12px;
  color: var(--neutral-500);
}

/* Invalid state */
.form-field.is-invalid input {
  border-color: var(--error-border);
  background-color: var(--error-bg);
}

.form-field .error {
  display: flex;
  align-items: center;
  gap: 6px;
  font-family: var(--font-ui);
  font-size: 12px;
  color: var(--error-text);
}

/* Disabled state */
.form-field input:disabled {
  background-color: var(--neutral-100);
  color: var(--neutral-400);
  cursor: not-allowed;
}
```

---

### 5.3 Cards

#### Product Card (Standard)

```
┌─────────────────────────┐
│                         │
│      [Cover Image]      │  ← 3:4 aspect ratio
│                         │
├─────────────────────────┤
│ [Tag]                   │  ← Optional: "Essential", "New"
│ Title of the Book       │  ← Outfit 600, Neutral 900, 2 lines max
│ Author Name             │  ← Source Serif 4, Neutral 600
│ £2.99                   │  ← Outfit 600, Teal 600
│ [Add to Cart]           │  ← Button small, secondary
└─────────────────────────┘
```

| Element | Font | Size | Colour |
|---------|------|------|--------|
| Tag | Space Grotesk 600 | 11px uppercase | Teal 700 on Teal 50 |
| Title | Outfit 600 | 16px | Neutral 900 |
| Author | Source Serif 4 400 | 14px | Neutral 600 |
| Price | Outfit 600 | 16px | Teal 600 |

**Specifications:**
- Background: Surface 50
- Border: 1px Surface 400
- Border radius: 8px
- Padding: 16px (below image)
- Image: 100% width, 3:4 aspect ratio, 8px radius (top corners)
- Gap between elements: 8px

**Hover state (desktop):**
- Border: Teal 600
- Cover: scale(1.02) with overflow hidden
- Box shadow: 0 4px 12px rgba(26, 74, 74, 0.1)
- Transition: 0.2s ease

#### Product Card (Compact)

For related products, "you may also like" sections.

```
┌─────────────────────────┐
│      [Cover Image]      │  ← 2:3 aspect ratio, smaller
├─────────────────────────┤
│ Title                   │  ← 14px, 1 line, truncate
│ £2.99                   │  ← 14px
└─────────────────────────┘
```

**Specifications:**
- No CTA button
- No author
- Padding: 12px

#### Product Card (List / Horizontal)

For mobile list views, search results.

```
┌──────────────────────────────────────────┐
│ ┌─────────┐  Title of the Book          │
│ │ [Cover] │  Author Name                │
│ │         │  £2.99     [Add to Cart]    │
│ └─────────┘                              │
└──────────────────────────────────────────┘
```

**Specifications:**
- Cover: 80px × 120px fixed
- Gap: 16px between cover and content
- Padding: 16px

#### Article Card

```
┌─────────────────────────┐
│                         │
│    [Featured Image]     │  ← 16:9 aspect ratio
│                         │
├─────────────────────────┤
│ [Category]              │  ← Tag style
│ Article Title Goes      │  ← Outfit 600, 18px
│ Here on Two Lines       │
│ Brief excerpt text...   │  ← Source Serif 4, 14px, 2 lines
│ 5 min read              │  ← Space Grotesk, 12px, Neutral 500
└─────────────────────────┘
```

#### Author Card

```
┌─────────────────────────┐
│    ┌─────────────┐      │
│    │   [Photo]   │      │  ← 96px circle
│    └─────────────┘      │
│      Author Name        │  ← Outfit 600, centre
│      (1920–1992)        │  ← Source Serif 4 italic
│      12 works           │  ← Space Grotesk, Neutral 500
└─────────────────────────┘
```

#### CSS Implementation

```css
.card {
  background-color: var(--surface-50);
  border: 1px solid var(--surface-400);
  border-radius: 8px;
  overflow: hidden;
  transition: border-color 0.2s, box-shadow 0.2s;
}

.card:hover {
  border-color: var(--teal-600);
  box-shadow: 0 4px 12px rgba(26, 74, 74, 0.1);
}

.card-image {
  width: 100%;
  aspect-ratio: 3 / 4;
  object-fit: cover;
  transition: transform 0.2s;
}

.card:hover .card-image {
  transform: scale(1.02);
}

.card-body {
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.card-title {
  font-family: var(--font-heading);
  font-size: 16px;
  font-weight: 600;
  color: var(--neutral-900);
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.card-author {
  font-family: var(--font-body);
  font-size: 14px;
  color: var(--neutral-600);
}

.card-price {
  font-family: var(--font-heading);
  font-size: 16px;
  font-weight: 600;
  color: var(--teal-600);
}
```

---

### 5.4 Navigation

#### Header (Desktop)

```
┌────────────────────────────────────────────────────────────────────┐
│  [Logo]     Discover  Library  Articles  Membership  About    🔍 👤 🛒 │
└────────────────────────────────────────────────────────────────────┘
```

| Element | Font | Size | Colour |
|---------|------|------|--------|
| Logo | Outfit 700 | 24px | Surface 200 |
| Nav links | Outfit 500 | 15px | Teal 200, hover Surface 200 |
| Active link | Outfit 600 | 15px | Surface 200, underline Amber 500 |

**Specifications:**
- Background: Teal 900
- Height: 64px
- Sticky on scroll
- Container: 1200px max, centred
- Padding: 0 48px

#### Header (Mobile)

```
┌────────────────────────────────┐
│  [☰]    [Logo]           🔍 🛒 │
└────────────────────────────────┘
```

**Specifications:**
- Height: 56px
- Hamburger opens full-screen overlay
- Logo centred

#### Mobile Navigation Overlay

```
┌────────────────────────────────┐
│  [✕]                           │
├────────────────────────────────┤
│  🔍 Search                     │
├────────────────────────────────┤
│  Discover                   ▸  │
│  Library                    ▸  │
│  Articles                   ▸  │
│  Membership                 ▸  │
│  About                      ▸  │
├────────────────────────────────┤
│  [Login]    [Join Now]         │
└────────────────────────────────┘
```

**Specifications:**
- Background: Teal 900
- Full viewport height
- Slide in from left (300ms ease)
- Backdrop: rgba(15, 51, 51, 0.8)
- Touch target: 48px height per item

#### Mega Menu (Desktop)

Triggered on hover for Discover and Library.

```
┌────────────────────────────────────────────────────────────────────┐
│  Browse By          Featured            Quick Links               │
│  ─────────          ────────            ───────────               │
│  Era                [img] Foundation    Popular This Week         │
│  Theme                    Reading Guide New Arrivals              │
│  Author             [img] Golden Age    Staff Picks               │
│  Format                   Collection                              │
└────────────────────────────────────────────────────────────────────┘
```

**Specifications:**
- Background: Surface 50
- Border-top: 2px Amber 500
- Box shadow: 0 8px 24px rgba(26, 74, 74, 0.15)
- 3 columns, 24px gap
- Appears on hover with 200ms delay
- Max height: 400px

#### Breadcrumbs

```
Home  /  Library  /  Ebooks  /  Foundation
```

| Element | Font | Colour |
|---------|------|--------|
| Links | Outfit 400, 14px | Teal 600 |
| Separator | — | Neutral 400 |
| Current | Outfit 500, 14px | Neutral 900 |

#### Pagination

```
[←]  1  2  [3]  4  5  ...  12  [→]
```

| Element | Style |
|---------|-------|
| Current page | Teal 600 bg, Surface 200 text |
| Other pages | Transparent bg, Teal 600 text |
| Arrows | Icon button style |
| Disabled arrow | Neutral 400 |

---

### 5.5 Modals & Dialogs

#### Modal Anatomy

```
┌───────────────────────────────────────────┐
│  Modal Title                        [✕]   │  ← Header
├───────────────────────────────────────────┤
│                                           │
│  Modal content goes here. This can        │  ← Body
│  include text, forms, or other            │
│  components.                              │
│                                           │
├───────────────────────────────────────────┤
│              [Cancel]    [Confirm]        │  ← Footer
└───────────────────────────────────────────┘
```

**Specifications:**
- Max width: 480px (small), 640px (medium), 800px (large)
- Background: Surface 50
- Border radius: 12px
- Padding: 24px
- Header: Outfit 600, 20px
- Backdrop: rgba(15, 51, 51, 0.6)

**Behaviour:**
- Escape key closes modal
- Click outside closes modal (unless `persistent`)
- Focus trapped within modal
- First focusable element receives focus on open
- Return focus to trigger element on close

#### Confirmation Dialog

```
┌───────────────────────────────────────────┐
│  Remove from Cart                   [✕]   │
├───────────────────────────────────────────┤
│                                           │
│  Are you sure you want to remove          │
│  "Foundation" from your cart?             │
│                                           │
├───────────────────────────────────────────┤
│              [Cancel]    [Remove Item]    │
└───────────────────────────────────────────┘
```

**Button placement:** Cancel (ghost) left, Confirm (primary/danger) right.

#### Mobile Modal

On mobile (<768px), modals become bottom sheets:

```
┌────────────────────────────────┐
│████████████████████████████████│  ← Backdrop
│████████████████████████████████│
│████████████████████████████████│
├────────────────────────────────┤
│  ─────  (drag handle)          │  ← Rounded top corners
│  Modal Title             [✕]   │
│                                │
│  Content...                    │
│                                │
│  [Cancel]    [Confirm]         │
└────────────────────────────────┘
```

**Specifications:**
- Slides up from bottom (300ms ease-out)
- Drag handle: 40px × 4px, Neutral 300, centred
- Border radius: 16px 16px 0 0
- Max height: 90vh
- Swipe down to dismiss

#### CSS Implementation

```css
.modal-backdrop {
  position: fixed;
  inset: 0;
  background-color: rgba(15, 51, 51, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  animation: fadeIn 0.2s ease;
}

.modal {
  background-color: var(--surface-50);
  border-radius: 12px;
  width: 100%;
  max-width: 480px;
  max-height: 90vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  animation: scaleIn 0.2s ease;
}

.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px 24px;
  border-bottom: 1px solid var(--surface-300);
}

.modal-title {
  font-family: var(--font-heading);
  font-size: 20px;
  font-weight: 600;
  color: var(--neutral-900);
}

.modal-body {
  padding: 24px;
  overflow-y: auto;
}

.modal-footer {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  padding: 16px 24px;
  border-top: 1px solid var(--surface-300);
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.95); }
  to { opacity: 1; transform: scale(1); }
}

/* Mobile bottom sheet */
@media (max-width: 767px) {
  .modal-backdrop {
    align-items: flex-end;
  }
  
  .modal {
    border-radius: 16px 16px 0 0;
    max-width: 100%;
    animation: slideUp 0.3s ease-out;
  }
  
  @keyframes slideUp {
    from { transform: translateY(100%); }
    to { transform: translateY(0); }
  }
}
```

---

### 5.6 Loading States

#### Skeleton Screens

Use skeleton placeholders that mirror content layout. Preferred over spinners for page/section loads.

**Product Card Skeleton:**
```
┌─────────────────────────┐
│  ░░░░░░░░░░░░░░░░░░░░   │  ← Animated pulse
│  ░░░░░░░░░░░░░░░░░░░░   │
│  ░░░░░░░░░░░░░░░░░░░░   │
├─────────────────────────┤
│  ░░░░░░░░░░░            │
│  ░░░░░░                 │
│  ░░░░                   │
└─────────────────────────┘
```

**Specifications:**
- Background: Neutral 200
- Animation: pulse (opacity 0.6 → 1, 1.5s infinite)
- Border radius: 4px (text), 8px (images)

#### Button Loading

```
[●○○ Adding...]     ← Spinner + text change
```

**Specifications:**
- Disable pointer events
- Replace icon with spinner (Loader2, animated)
- Text changes: "Add to Cart" → "Adding…"
- Maintain button width (prevent layout shift)

#### Page Loading

For route transitions, show thin progress bar at top of viewport.

**Specifications:**
- Height: 3px
- Colour: Amber 500
- Position: fixed, top 0
- Animation: width 0% → 90% (indeterminate), then 100% on complete

#### Image Loading

```
┌─────────────────────────┐
│                         │
│   [Blurred preview]     │  ← Low-res placeholder or dominant colour
│                         │
└─────────────────────────┘
         ↓
┌─────────────────────────┐
│                         │
│   [Sharp full image]    │  ← Fade in on load
│                         │
└─────────────────────────┘
```

**Specifications:**
- Placeholder: 20px blurred thumbnail or extracted dominant colour
- Transition: opacity 0 → 1 over 0.3s

#### CSS Implementation

```css
/* Skeleton base */
.skeleton {
  background: linear-gradient(
    90deg,
    var(--neutral-200) 25%,
    var(--neutral-100) 50%,
    var(--neutral-200) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: 4px;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

.skeleton-text {
  height: 16px;
  margin-bottom: 8px;
}

.skeleton-text.short { width: 60%; }
.skeleton-text.medium { width: 80%; }

.skeleton-image {
  aspect-ratio: 3 / 4;
  border-radius: 8px;
}

/* Progress bar */
.progress-bar {
  position: fixed;
  top: 0;
  left: 0;
  height: 3px;
  background-color: var(--amber-500);
  z-index: 9999;
  transition: width 0.2s;
}

/* Button spinner */
.btn-spinner {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
```

---

### 5.7 Badges & Tags

#### Tag Variants

| Variant | Background | Text | Border | Use Case |
|---------|------------|------|--------|----------|
| **Default** | Teal 50 | Teal 700 | none | Categories, genres, eras |
| **Amber** | Amber 100 | Amber 800 | none | Featured, highlights, "New" |
| **Neutral** | Neutral 100 | Neutral 700 | none | Counts, metadata |
| **Outline** | transparent | Teal 600 | 1px Teal 300 | Filter chips (removable) |
| **Success** | Success bg | Success text | none | "Available", "In Stock" |
| **Warning** | Warning bg | Warning text | none | "Limited", "Ending Soon" |
| **Error** | Error bg | Error text | none | "Sold Out", "Unavailable" |

#### Tag Sizes

| Size | Height | Padding | Font Size |
|------|--------|---------|-----------|
| **Small** | 20px | 6px 8px | 10px |
| **Medium** | 24px | 6px 10px | 11px |
| **Large** | 28px | 8px 12px | 12px |

#### Tag Anatomy

```
┌───────────────┐
│ TAG LABEL     │  ← Space Grotesk 600, uppercase, letter-spacing 0.5px
└───────────────┘
```

#### Badge (Count)

For notification counts, cart items.

```
[🛒]
 ⁽³⁾   ← Badge overlapping icon
```

**Specifications:**
- Min width: 18px
- Height: 18px
- Border radius: 9px (pill)
- Background: Amber 500
- Text: Teal 900, 11px, Outfit 600
- Position: absolute, top -6px, right -6px

#### CSS Implementation

```css
.tag {
  display: inline-flex;
  align-items: center;
  font-family: var(--font-ui);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  border-radius: 4px;
}

/* Sizes */
.tag-sm { height: 20px; padding: 0 8px; font-size: 10px; }
.tag-md { height: 24px; padding: 0 10px; font-size: 11px; }
.tag-lg { height: 28px; padding: 0 12px; font-size: 12px; }

/* Variants */
.tag-default { background: var(--teal-50); color: var(--teal-700); }
.tag-amber { background: var(--amber-100); color: var(--amber-800); }
.tag-neutral { background: var(--neutral-100); color: var(--neutral-700); }
.tag-outline { 
  background: transparent; 
  color: var(--teal-600); 
  border: 1px solid var(--teal-300);
}
.tag-success { background: var(--success-bg); color: var(--success-text); }
.tag-warning { background: var(--warning-bg); color: var(--warning-text); }
.tag-error { background: var(--error-bg); color: var(--error-text); }

/* Removable tag */
.tag-removable {
  padding-right: 6px;
}
.tag-remove {
  margin-left: 4px;
  cursor: pointer;
  opacity: 0.7;
}
.tag-remove:hover {
  opacity: 1;
}

/* Badge */
.badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 18px;
  height: 18px;
  padding: 0 5px;
  font-family: var(--font-heading);
  font-size: 11px;
  font-weight: 600;
  background-color: var(--amber-500);
  color: var(--teal-900);
  border-radius: 9px;
}

/* Badge on icon */
.icon-with-badge {
  position: relative;
}
.icon-with-badge .badge {
  position: absolute;
  top: -6px;
  right: -6px;
}
```

---

### 5.8 Tooltips

#### Tooltip Anatomy

```
                    ┌─────────────────────────────┐
                    │ ePub is a digital book      │
         ▲          │ format compatible with most │
         │          │ e-readers.                  │
        [?]         └─────────────────────────────┘
                              ▼
```

**Specifications:**
- Background: Teal 900
- Text: Surface 200, Source Serif 4, 14px
- Padding: 8px 12px
- Border radius: 6px
- Max width: 240px
- Arrow: 8px

#### Trigger Behaviour

| Trigger | Show | Hide |
|---------|------|------|
| Hover (desktop) | 200ms delay | Immediate on mouse leave |
| Focus (keyboard) | Immediate | On blur |
| Touch (mobile) | On tap | Tap elsewhere |

#### Positions

| Position | Arrow | Use When |
|----------|-------|----------|
| Top | Bottom centre | Default, most common |
| Bottom | Top centre | When near top of viewport |
| Left | Right centre | When near right edge |
| Right | Left centre | When near left edge |

Auto-position to stay within viewport.

#### CSS Implementation

```css
.tooltip-trigger {
  position: relative;
}

.tooltip {
  position: absolute;
  z-index: 1000;
  padding: 8px 12px;
  background-color: var(--teal-900);
  color: var(--surface-200);
  font-family: var(--font-body);
  font-size: 14px;
  line-height: 1.4;
  border-radius: 6px;
  max-width: 240px;
  white-space: normal;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s, visibility 0.2s;
}

.tooltip-trigger:hover .tooltip,
.tooltip-trigger:focus .tooltip {
  opacity: 1;
  visibility: visible;
}

/* Positions */
.tooltip-top {
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  margin-bottom: 8px;
}

.tooltip-bottom {
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  margin-top: 8px;
}

/* Arrow */
.tooltip::after {
  content: '';
  position: absolute;
  border: 6px solid transparent;
}

.tooltip-top::after {
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  border-top-color: var(--teal-900);
}

.tooltip-bottom::after {
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  border-bottom-color: var(--teal-900);
}
```

#### Accessibility

```html
<!-- Tooltip with accessible description -->
<button aria-describedby="tooltip-1">
  <HelpCircle size={16} />
</button>
<div id="tooltip-1" role="tooltip" class="tooltip tooltip-top">
  ePub is a digital book format compatible with most e-readers.
</div>
```

**Requirements:**
- Use `role="tooltip"` on tooltip element
- Use `aria-describedby` to link trigger to tooltip
- Ensure tooltip is focusable via keyboard
- Dismiss on Escape key

Here's the complete Section 6:

---

## 6. Interactive States

All interactive elements must provide clear visual feedback across states. Consistent state styling builds user confidence and supports accessibility requirements.

### 6.1 Hover States

Hover states indicate interactivity and provide feedback on desktop devices. All hover transitions use `200ms ease`.

#### Colour Shifts

| Element | Default | Hover |
|---------|---------|-------|
| **Primary button** | Teal 600 bg | Teal 700 bg |
| **Accent button** | Amber 500 bg | Amber 400 bg |
| **Secondary button** | Transparent bg | Teal 50 bg |
| **Ghost button** | Transparent bg | Surface 100 bg |
| **Text link** | Teal 600 | Teal 700 + underline |
| **Nav link (dark)** | Teal 200 | Surface 200 |
| **Icon button** | Neutral 600 | Teal 600 + Surface 100 bg |
| **Card** | Surface 400 border | Teal 600 border |

#### Transform Effects

| Element | Hover Effect |
|---------|--------------|
| **Product card** | `translateY(-4px)` + shadow |
| **Card image** | `scale(1.02)` within overflow hidden |
| **Icon button** | `scale(1.05)` (subtle) |

#### Shadow Effects

| Element | Default Shadow | Hover Shadow |
|---------|----------------|--------------|
| **Card** | none | `0 4px 12px rgba(26, 74, 74, 0.1)` |
| **Dropdown** | — | `0 8px 24px rgba(26, 74, 74, 0.15)` |
| **Floating button** | `0 2px 8px rgba(26, 74, 74, 0.1)` | `0 4px 16px rgba(26, 74, 74, 0.15)` |

#### CSS Implementation

```css
/* Link hover */
a:hover {
  color: var(--teal-700);
  text-decoration: underline;
  text-underline-offset: 2px;
}

/* Card hover */
.card {
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  border-color: var(--teal-600);
  box-shadow: 0 4px 12px rgba(26, 74, 74, 0.1);
}

/* Card image zoom */
.card-image-wrapper {
  overflow: hidden;
  border-radius: 8px 8px 0 0;
}

.card-image {
  transition: transform 0.2s ease;
}

.card:hover .card-image {
  transform: scale(1.02);
}

/* Icon button hover */
.icon-button:hover {
  color: var(--teal-600);
  background-color: var(--surface-100);
}
```

#### Touch Devices

Hover states should not be relied upon for essential information on touch devices. Use `@media (hover: hover)` to apply hover-only styles:

```css
@media (hover: hover) {
  .card:hover {
    transform: translateY(-4px);
    box-shadow: 0 4px 12px rgba(26, 74, 74, 0.1);
  }
}
```

---

### 6.2 Focus States

Focus states are **critical for accessibility**. They indicate which element has keyboard focus and must be clearly visible. Never remove focus outlines without providing an alternative.

#### Focus Ring Specification

| Property | Value |
|----------|-------|
| Colour | Amber 500 (`#C9943A`) |
| Width | 2px |
| Style | solid |
| Offset | 2px |
| Border radius | Follows element's border-radius + 2px |

#### Focus by Element Type

| Element | Focus Style |
|---------|-------------|
| **Buttons** | 2px Amber 500 outline, 2px offset |
| **Links** | 2px Amber 500 outline, 2px offset |
| **Inputs** | 2px Teal 600 border (replaces default border) |
| **Cards (interactive)** | 2px Amber 500 outline, 2px offset |
| **Checkboxes/Radios** | 2px Amber 500 outline on custom box |
| **Icon buttons** | 2px Amber 500 outline, 2px offset |

#### Focus-Visible vs Focus

Use `:focus-visible` to show focus rings only for keyboard navigation, not mouse clicks:

```css
/* Remove default outline */
button:focus {
  outline: none;
}

/* Show custom focus ring for keyboard users only */
button:focus-visible {
  outline: 2px solid var(--amber-500);
  outline-offset: 2px;
}

/* For browsers without focus-visible support, fall back to :focus */
@supports not selector(:focus-visible) {
  button:focus {
    outline: 2px solid var(--amber-500);
    outline-offset: 2px;
  }
}
```

#### Input Focus

Inputs use a border change rather than outline for a cleaner appearance:

```css
.form-field input:focus,
.form-field textarea:focus,
.form-field select:focus {
  outline: none;
  border: 2px solid var(--teal-600);
  background-color: var(--surface-0);
}
```

#### Focus on Dark Backgrounds

On dark backgrounds (Teal 900), use Surface 200 for focus indicators:

```css
.dark-bg button:focus-visible {
  outline-color: var(--surface-200);
}
```

#### Focus Order

Focus order must follow visual reading order (left-to-right, top-to-bottom for LTR languages). Never use positive `tabindex` values; use DOM order instead.

```html
<!-- Correct: DOM order matches visual order -->
<nav>
  <a href="/discover">Discover</a>
  <a href="/library">Library</a>
  <a href="/articles">Articles</a>
</nav>

<!-- Incorrect: Don't manipulate tab order -->
<nav>
  <a href="/articles" tabindex="3">Articles</a>
  <a href="/discover" tabindex="1">Discover</a>
  <a href="/library" tabindex="2">Library</a>
</nav>
```

#### CSS Implementation

```css
/* Global focus-visible styles */
:focus-visible {
  outline: 2px solid var(--amber-500);
  outline-offset: 2px;
}

/* Remove outline for mouse users */
:focus:not(:focus-visible) {
  outline: none;
}

/* Specific element adjustments */
.btn:focus-visible {
  outline: 2px solid var(--amber-500);
  outline-offset: 2px;
}

.card:focus-visible {
  outline: 2px solid var(--amber-500);
  outline-offset: 2px;
}

a:focus-visible {
  outline: 2px solid var(--amber-500);
  outline-offset: 2px;
  border-radius: 2px;
}

/* Input focus (uses border instead of outline) */
input:focus,
textarea:focus,
select:focus {
  outline: none;
  border: 2px solid var(--teal-600);
}
```

---

### 6.3 Active States

Active states provide immediate feedback when an element is being clicked or tapped. They should feel "pressed" or "depressed".

#### Active Colour Shifts

| Element | Default | Active |
|---------|---------|--------|
| **Primary button** | Teal 600 bg | Teal 800 bg |
| **Accent button** | Amber 500 bg | Amber 600 bg |
| **Secondary button** | Transparent bg | Teal 100 bg |
| **Ghost button** | Transparent bg | Surface 200 bg |
| **Text link** | Teal 600 | Teal 800 |
| **Nav link (dark)** | Teal 200 | Surface 200 |
| **Icon button** | Neutral 600 | Teal 700 |

#### Active Transform

Buttons scale down slightly to create a "pressed" effect:

```css
.btn:active {
  transform: scale(0.98);
}
```

#### Active Duration

Active states should be visible but brief. Transition should be faster than hover (100ms vs 200ms):

```css
.btn {
  transition: background-color 0.2s ease, transform 0.1s ease;
}

.btn:active {
  background-color: var(--teal-800);
  transform: scale(0.98);
}
```

#### CSS Implementation

```css
/* Primary button active */
.btn-primary:active {
  background-color: var(--teal-800);
  transform: scale(0.98);
}

/* Secondary button active */
.btn-secondary:active {
  background-color: var(--teal-100);
  transform: scale(0.98);
}

/* Ghost button active */
.btn-ghost:active {
  background-color: var(--surface-200);
  transform: scale(0.98);
}

/* Link active */
a:active {
  color: var(--teal-800);
}

/* Card active (for clickable cards) */
.card-clickable:active {
  transform: translateY(0);
  box-shadow: none;
}

/* Icon button active */
.icon-button:active {
  color: var(--teal-700);
  transform: scale(0.95);
}
```

---

### 6.4 Disabled States

Disabled states indicate that an element is not interactive. They should look visibly "inactive" while maintaining readability.

#### Disabled Styling

| Property | Value |
|----------|-------|
| Background | Neutral 200 or Neutral 100 |
| Text/Icon | Neutral 400 |
| Border | Neutral 300 (if applicable) |
| Cursor | `not-allowed` |
| Opacity | Do not use opacity alone—use explicit colours |
| Pointer events | `none` (optional, cursor handles this) |

#### Disabled by Element

| Element | Disabled Style |
|---------|----------------|
| **Primary button** | Neutral 200 bg, Neutral 500 text |
| **Secondary button** | Neutral 300 border, Neutral 400 text |
| **Ghost button** | Neutral 300 border, Neutral 400 text |
| **Text link** | Neutral 400, no underline, `cursor: default` |
| **Input** | Neutral 100 bg, Neutral 400 text |
| **Checkbox/Radio** | Neutral 200 fill, Neutral 400 border |
| **Select** | Neutral 100 bg, Neutral 400 text |
| **Card (non-interactive)** | No change (cards are not "disabled") |

#### Accessibility Considerations

- Use `disabled` attribute for form elements—this removes them from tab order
- Use `aria-disabled="true"` for custom components that should remain in tab order but not be activatable
- Provide context for why something is disabled when possible

```html
<!-- Native disabled (removed from tab order) -->
<button disabled>Sold Out</button>

<!-- ARIA disabled (remains in tab order, announced as disabled) -->
<button aria-disabled="true">Sold Out</button>

<!-- With explanation -->
<button disabled aria-describedby="sold-out-msg">Add to Cart</button>
<span id="sold-out-msg" class="sr-only">This item is currently sold out</span>
```

#### CSS Implementation

```css
/* Button disabled */
.btn:disabled,
.btn[aria-disabled="true"] {
  background-color: var(--neutral-200);
  border-color: var(--neutral-200);
  color: var(--neutral-500);
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}

.btn:disabled:hover,
.btn[aria-disabled="true"]:hover {
  background-color: var(--neutral-200);
  transform: none;
}

/* Secondary button disabled */
.btn-secondary:disabled {
  background-color: transparent;
  border-color: var(--neutral-300);
  color: var(--neutral-400);
}

/* Input disabled */
input:disabled,
textarea:disabled,
select:disabled {
  background-color: var(--neutral-100);
  border-color: var(--neutral-200);
  color: var(--neutral-400);
  cursor: not-allowed;
}

/* Link disabled (use class, links don't have disabled attribute) */
a.disabled {
  color: var(--neutral-400);
  text-decoration: none;
  cursor: default;
  pointer-events: none;
}

/* Checkbox/Radio disabled */
input[type="checkbox"]:disabled + .checkbox-box,
input[type="radio"]:disabled + .radio-dot {
  background-color: var(--neutral-200);
  border-color: var(--neutral-300);
}

input[type="checkbox"]:disabled + .checkbox-box + .checkbox-label,
input[type="radio"]:disabled + .radio-dot + .radio-label {
  color: var(--neutral-400);
}
```

---

### 6.5 Error & Success States

Error and success states provide feedback on form validation and system responses. They use semantic colours consistently across all components.

#### Error States

| Property | Value |
|----------|-------|
| Background | Error bg (`#FDF2F2`) |
| Border | Error border (`#F0B8B8`) |
| Text | Error text (`#8B2020`) |
| Icon | AlertCircle or AlertTriangle |

**Error state elements:**
- Form inputs with validation errors
- Alert messages
- Toast notifications
- Inline error messages

#### Error Input Pattern

```
Email Address *                           ← Label turns Error text
┌─────────────────────────────────────┐
│ invalid-email                       │   ← Border: Error border, bg: Error bg
└─────────────────────────────────────┘
⚠ Please enter a valid email address     ← Error text + icon
```

```html
<div class="form-field is-error">
  <label for="email">Email Address <span class="required">*</span></label>
  <input 
    type="email" 
    id="email" 
    value="invalid-email"
    aria-invalid="true"
    aria-describedby="email-error"
  />
  <span id="email-error" class="field-error" role="alert">
    <svg><!-- AlertCircle icon --></svg>
    Please enter a valid email address
  </span>
</div>
```

#### Success States

| Property | Value |
|----------|-------|
| Background | Success bg (`#ECF7F2`) |
| Border | Success border (`#A8DCBE`) |
| Text | Success text (`#1A5C38`) |
| Icon | Check or CheckCircle |

**Success state elements:**
- Validated form inputs (optional—use sparingly)
- Confirmation messages
- Toast notifications
- Completed step indicators

#### Success Input Pattern

```
Email Address *
┌─────────────────────────────────────┐
│ user@example.com                 ✓  │   ← Border: Success border, icon inside
└─────────────────────────────────────┘
```

#### Warning States

| Property | Value |
|----------|-------|
| Background | Warning bg (`#FDF8EB`) |
| Border | Warning border (`#F0D49E`) |
| Text | Warning text (`#7A4D15`) |
| Icon | AlertTriangle |

**Warning state elements:**
- Non-critical alerts
- Notices requiring attention
- Deprecation warnings

#### Info States

| Property | Value |
|----------|-------|
| Background | Info bg (`#E5F2F2`) |
| Border | Info border (`#7DBDBD`) |
| Text | Info text (`#1A4A4A`) |
| Icon | Info |

**Info state elements:**
- Informational messages
- Tips and hints
- Neutral system notifications

#### Alert Component

```
┌─────────────────────────────────────────────────────────┐
│ ⚠  Your session will expire in 5 minutes.        [✕]   │
└─────────────────────────────────────────────────────────┘
```

**Specifications:**
- Padding: 12px 16px
- Border-left: 4px solid (state colour)
- Border-radius: 6px
- Icon: 20px, aligned with first line of text
- Dismiss button (optional): icon-button style

#### Toast Notifications

```
┌────────────────────────────────────┐
│ ✓  Product added to cart           │   ← Success toast
└────────────────────────────────────┘

┌────────────────────────────────────┐
│ ⚠  Payment failed. Please retry.   │   ← Error toast
└────────────────────────────────────┘
```

**Specifications:**
- Position: fixed bottom-right (desktop), bottom-center (mobile)
- Margin from edge: 24px
- Auto-dismiss: 5 seconds (success/info), persistent (error/warning)
- Animation: slide up + fade in
- Stack multiple toasts with 8px gap

#### CSS Implementation

```css
/* Error state */
.form-field.is-error label {
  color: var(--error-text);
}

.form-field.is-error input,
.form-field.is-error textarea,
.form-field.is-error select {
  border-color: var(--error-border);
  background-color: var(--error-bg);
}

.form-field.is-error input:focus {
  border-color: var(--error-text);
}

.field-error {
  display: flex;
  align-items: center;
  gap: 6px;
  font-family: var(--font-ui);
  font-size: 12px;
  color: var(--error-text);
  margin-top: 6px;
}

/* Success state */
.form-field.is-success input {
  border-color: var(--success-border);
  background-color: var(--success-bg);
}

.field-success {
  display: flex;
  align-items: center;
  gap: 6px;
  font-family: var(--font-ui);
  font-size: 12px;
  color: var(--success-text);
  margin-top: 6px;
}

/* Alert component */
.alert {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  padding: 12px 16px;
  border-radius: 6px;
  border-left: 4px solid;
}

.alert-error {
  background-color: var(--error-bg);
  border-left-color: var(--error-text);
  color: var(--error-text);
}

.alert-success {
  background-color: var(--success-bg);
  border-left-color: var(--success-text);
  color: var(--success-text);
}

.alert-warning {
  background-color: var(--warning-bg);
  border-left-color: var(--warning-text);
  color: var(--warning-text);
}

.alert-info {
  background-color: var(--info-bg);
  border-left-color: var(--info-text);
  color: var(--info-text);
}

.alert-icon {
  flex-shrink: 0;
  width: 20px;
  height: 20px;
}

.alert-content {
  flex: 1;
  font-family: var(--font-body);
  font-size: 14px;
  line-height: 1.5;
}

.alert-dismiss {
  flex-shrink: 0;
  margin-left: auto;
}

/* Toast */
.toast-container {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 1100;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

@media (max-width: 767px) {
  .toast-container {
    left: 16px;
    right: 16px;
    bottom: 16px;
  }
}

.toast {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  background-color: var(--teal-900);
  color: var(--surface-200);
  border-radius: 8px;
  box-shadow: 0 4px 16px rgba(15, 51, 51, 0.2);
  animation: slideUp 0.3s ease;
}

.toast-success {
  background-color: var(--success-text);
}

.toast-error {
  background-color: var(--error-text);
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(16px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

### 6.6 State Transition Summary

| Transition | Duration | Easing | Properties |
|------------|----------|--------|------------|
| Hover | 200ms | ease | background-color, border-color, color, box-shadow |
| Focus | 0ms | — | outline (instant for accessibility) |
| Active | 100ms | ease | background-color, transform |
| Disabled | 0ms | — | No transition (instant) |
| Error/Success | 200ms | ease | border-color, background-color |
| Card lift | 200ms | ease | transform, box-shadow |
| Image zoom | 200ms | ease | transform |

```css
/* Standard transition preset */
.interactive {
  transition: 
    background-color 0.2s ease,
    border-color 0.2s ease,
    color 0.2s ease,
    box-shadow 0.2s ease,
    transform 0.1s ease;
}
```
---

## 7. Motion & Animation

Motion and animation enhance user experience by providing feedback, guiding attention, and creating a sense of polish. However, animation must be purposeful, performant, and accessible.

**Core principle:** Motion should feel natural and supportive, never gratuitous or distracting.

### 7.1 Animation Principles

#### Purpose-Driven Motion

Every animation must serve at least one purpose:

| Purpose | Example |
|---------|---------|
| **Feedback** | Button press, form submission confirmation |
| **Orientation** | Page transitions, modal open/close |
| **Guidance** | Drawing attention to new content, error fields |
| **Continuity** | Maintaining context during state changes |
| **Delight** | Subtle polish that reinforces brand personality |

#### Motion Personality

SF Supernova's motion should feel:

- **Confident:** Decisive movements, no hesitation or bounce
- **Warm:** Smooth easing, never mechanical or robotic
- **Sophisticated:** Subtle and refined, never flashy
- **Efficient:** Quick enough to feel responsive, slow enough to be perceived

### 7.2 Timing & Duration

#### Duration Scale

| Token | Duration | Use Case |
|-------|----------|----------|
| `--duration-instant` | 0ms | Focus states, disabled states |
| `--duration-fast` | 100ms | Active states, micro-interactions |
| `--duration-normal` | 200ms | Hover states, colour transitions |
| `--duration-moderate` | 300ms | Modal open/close, panel slide |
| `--duration-slow` | 400ms | Page transitions, complex reveals |
| `--duration-slower` | 500ms | Skeleton shimmer, attention-drawing |

#### Duration Guidelines

| Animation Type | Recommended Duration |
|----------------|---------------------|
| Colour change | 150–200ms |
| Opacity fade | 200–300ms |
| Transform (small) | 150–200ms |
| Transform (large) | 300–400ms |
| Slide/expand | 250–350ms |
| Page transition | 300–400ms |
| Loading shimmer | 1500ms (loop) |
| Spinner rotation | 1000ms (loop) |

**Rule of thumb:** Smaller movements = shorter duration. Larger movements = longer duration.

### 7.3 Easing Functions

#### Standard Easings

| Token | Value | Use Case |
|-------|-------|----------|
| `--ease-default` | `ease` | General purpose, balanced |
| `--ease-in` | `cubic-bezier(0.4, 0, 1, 1)` | Elements exiting view |
| `--ease-out` | `cubic-bezier(0, 0, 0.2, 1)` | Elements entering view |
| `--ease-in-out` | `cubic-bezier(0.4, 0, 0.2, 1)` | Elements moving within view |
| `--ease-bounce` | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Playful emphasis (use sparingly) |

#### Easing Selection Guide

| Scenario | Easing |
|----------|--------|
| **Hover state** | `ease` or `ease-out` |
| **Modal appearing** | `ease-out` |
| **Modal dismissing** | `ease-in` |
| **Expanding accordion** | `ease-in-out` |
| **Card lifting on hover** | `ease-out` |
| **Page entering** | `ease-out` |
| **Page exiting** | `ease-in` |
| **Attention pulse** | `ease-in-out` |

#### CSS Custom Properties

```css
:root {
  /* Durations */
  --duration-instant: 0ms;
  --duration-fast: 100ms;
  --duration-normal: 200ms;
  --duration-moderate: 300ms;
  --duration-slow: 400ms;
  --duration-slower: 500ms;
  
  /* Easings */
  --ease-default: ease;
  --ease-in: cubic-bezier(0.4, 0, 1, 1);
  --ease-out: cubic-bezier(0, 0, 0.2, 1);
  --ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
  --ease-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

### 7.4 Transition Patterns

#### Standard Transitions

```css
/* Colour transitions (buttons, links) */
.transition-colors {
  transition-property: color, background-color, border-color;
  transition-duration: var(--duration-normal);
  transition-timing-function: var(--ease-default);
}

/* Opacity transitions (fade in/out) */
.transition-opacity {
  transition-property: opacity;
  transition-duration: var(--duration-normal);
  transition-timing-function: var(--ease-default);
}

/* Transform transitions (move, scale) */
.transition-transform {
  transition-property: transform;
  transition-duration: var(--duration-normal);
  transition-timing-function: var(--ease-out);
}

/* Shadow transitions (elevation changes) */
.transition-shadow {
  transition-property: box-shadow;
  transition-duration: var(--duration-normal);
  transition-timing-function: var(--ease-default);
}

/* All common properties */
.transition-all {
  transition-property: color, background-color, border-color, opacity, transform, box-shadow;
  transition-duration: var(--duration-normal);
  transition-timing-function: var(--ease-default);
}
```

#### Component-Specific Transitions

```css
/* Button */
.btn {
  transition: 
    background-color var(--duration-normal) var(--ease-default),
    border-color var(--duration-normal) var(--ease-default),
    color var(--duration-normal) var(--ease-default),
    transform var(--duration-fast) var(--ease-default);
}

/* Card */
.card {
  transition:
    transform var(--duration-normal) var(--ease-out),
    box-shadow var(--duration-normal) var(--ease-out),
    border-color var(--duration-normal) var(--ease-default);
}

/* Link */
a {
  transition: color var(--duration-normal) var(--ease-default);
}

/* Input */
input, textarea, select {
  transition:
    border-color var(--duration-normal) var(--ease-default),
    background-color var(--duration-normal) var(--ease-default);
}
```

### 7.5 Keyframe Animations

#### Fade In

```css
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.animate-fade-in {
  animation: fadeIn var(--duration-moderate) var(--ease-out) forwards;
}
```

#### Fade Out

```css
@keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}

.animate-fade-out {
  animation: fadeOut var(--duration-moderate) var(--ease-in) forwards;
}
```

#### Slide Up (Enter)

```css
@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(16px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-slide-up {
  animation: slideUp var(--duration-moderate) var(--ease-out) forwards;
}
```

#### Slide Down (Exit)

```css
@keyframes slideDown {
  from {
    opacity: 1;
    transform: translateY(0);
  }
  to {
    opacity: 0;
    transform: translateY(16px);
  }
}

.animate-slide-down {
  animation: slideDown var(--duration-moderate) var(--ease-in) forwards;
}
```

#### Scale In (Modal)

```css
@keyframes scaleIn {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

.animate-scale-in {
  animation: scaleIn var(--duration-moderate) var(--ease-out) forwards;
}
```

#### Scale Out (Modal)

```css
@keyframes scaleOut {
  from {
    opacity: 1;
    transform: scale(1);
  }
  to {
    opacity: 0;
    transform: scale(0.95);
  }
}

.animate-scale-out {
  animation: scaleOut var(--duration-normal) var(--ease-in) forwards;
}
```

#### Slide In From Left (Mobile Nav)

```css
@keyframes slideInLeft {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}

.animate-slide-in-left {
  animation: slideInLeft var(--duration-moderate) var(--ease-out) forwards;
}
```

#### Slide Out To Left

```css
@keyframes slideOutLeft {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-100%);
  }
}

.animate-slide-out-left {
  animation: slideOutLeft var(--duration-moderate) var(--ease-in) forwards;
}
```

#### Slide Up From Bottom (Mobile Modal)

```css
@keyframes slideUpFromBottom {
  from {
    transform: translateY(100%);
  }
  to {
    transform: translateY(0);
  }
}

.animate-slide-up-bottom {
  animation: slideUpFromBottom var(--duration-moderate) var(--ease-out) forwards;
}
```

### 7.6 Loading Animations

#### Spinner

```css
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.animate-spin {
  animation: spin 1s linear infinite;
}
```

#### Skeleton Shimmer

```css
@keyframes shimmer {
  0% {
    background-position: 200% 0;
  }
  100% {
    background-position: -200% 0;
  }
}

.skeleton {
  background: linear-gradient(
    90deg,
    var(--neutral-200) 25%,
    var(--neutral-100) 50%,
    var(--neutral-200) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}
```

#### Pulse (Attention)

```css
@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.6;
  }
}

.animate-pulse {
  animation: pulse 2s var(--ease-in-out) infinite;
}
```

#### Progress Bar (Indeterminate)

```css
@keyframes progressIndeterminate {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(400%);
  }
}

.progress-indeterminate::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 25%;
  height: 100%;
  background-color: var(--amber-500);
  animation: progressIndeterminate 1.5s var(--ease-in-out) infinite;
}
```

#### Dot Loading

```css
@keyframes dotBounce {
  0%, 80%, 100% {
    transform: scale(0.6);
    opacity: 0.5;
  }
  40% {
    transform: scale(1);
    opacity: 1;
  }
}

.loading-dots span {
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: var(--teal-600);
  animation: dotBounce 1.4s var(--ease-in-out) infinite;
}

.loading-dots span:nth-child(1) { animation-delay: 0s; }
.loading-dots span:nth-child(2) { animation-delay: 0.2s; }
.loading-dots span:nth-child(3) { animation-delay: 0.4s; }
```

### 7.7 Interaction Animations

#### Button Press

```css
.btn:active {
  transform: scale(0.98);
  transition: transform var(--duration-fast) var(--ease-default);
}
```

#### Card Lift

```css
.card {
  transition: 
    transform var(--duration-normal) var(--ease-out),
    box-shadow var(--duration-normal) var(--ease-out);
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 12px rgba(26, 74, 74, 0.1);
}
```

#### Image Zoom

```css
.card-image-wrapper {
  overflow: hidden;
}

.card-image {
  transition: transform var(--duration-normal) var(--ease-out);
}

.card:hover .card-image {
  transform: scale(1.02);
}
```

#### Accordion Expand

```css
.accordion-content {
  display: grid;
  grid-template-rows: 0fr;
  transition: grid-template-rows var(--duration-moderate) var(--ease-in-out);
}

.accordion-content.is-open {
  grid-template-rows: 1fr;
}

.accordion-inner {
  overflow: hidden;
}
```

#### Chevron Rotate

```css
.accordion-trigger svg {
  transition: transform var(--duration-normal) var(--ease-default);
}

.accordion-trigger[aria-expanded="true"] svg {
  transform: rotate(180deg);
}
```

#### Toast Enter/Exit

```css
.toast {
  animation: toastEnter var(--duration-moderate) var(--ease-out) forwards;
}

.toast.is-exiting {
  animation: toastExit var(--duration-normal) var(--ease-in) forwards;
}

@keyframes toastEnter {
  from {
    opacity: 0;
    transform: translateY(16px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes toastExit {
  from {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
  to {
    opacity: 0;
    transform: translateY(-8px) scale(0.95);
  }
}
```

### 7.8 Page Transitions

For single-page applications or smooth navigation experiences.

#### Page Enter

```css
.page-enter {
  animation: pageEnter var(--duration-slow) var(--ease-out) forwards;
}

@keyframes pageEnter {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

#### Page Exit

```css
.page-exit {
  animation: pageExit var(--duration-moderate) var(--ease-in) forwards;
}

@keyframes pageExit {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
```

#### Staggered Content

For lists and grids, stagger child animations:

```css
.stagger-children > * {
  opacity: 0;
  animation: fadeSlideUp var(--duration-moderate) var(--ease-out) forwards;
}

.stagger-children > *:nth-child(1) { animation-delay: 0ms; }
.stagger-children > *:nth-child(2) { animation-delay: 50ms; }
.stagger-children > *:nth-child(3) { animation-delay: 100ms; }
.stagger-children > *:nth-child(4) { animation-delay: 150ms; }
.stagger-children > *:nth-child(5) { animation-delay: 200ms; }
.stagger-children > *:nth-child(6) { animation-delay: 250ms; }

@keyframes fadeSlideUp {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

### 7.9 Accessibility & Reduced Motion

#### Respecting User Preferences

Users can indicate a preference for reduced motion via their operating system settings. Respect this preference using the `prefers-reduced-motion` media query.

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

#### Alternative: Selective Reduction

For more nuanced control, reduce rather than eliminate motion:

```css
@media (prefers-reduced-motion: reduce) {
  /* Disable decorative animations */
  .animate-pulse,
  .animate-bounce,
  .stagger-children > * {
    animation: none;
    opacity: 1;
    transform: none;
  }
  
  /* Keep functional animations but make them instant */
  .modal {
    animation: none;
    opacity: 1;
    transform: scale(1);
  }
  
  /* Reduce skeleton shimmer to static */
  .skeleton {
    animation: none;
    background: var(--neutral-200);
  }
  
  /* Keep spinner for loading indication */
  .animate-spin {
    animation: spin 1s linear infinite;
  }
}
```

#### Motion Safety Guidelines

| Animation Type | Reduced Motion Behaviour |
|----------------|--------------------------|
| **Decorative** (pulse, shimmer) | Remove entirely |
| **Feedback** (button press) | Keep, but reduce duration |
| **Navigation** (page transitions) | Replace with instant cut |
| **Loading** (spinner) | Keep—essential for feedback |
| **Modal open/close** | Replace with instant appear/disappear |
| **Hover effects** | Keep subtle colour changes, remove transforms |

#### Seizure Safety

Never use animations that flash more than 3 times per second. Avoid:

- Rapidly flashing colours
- Strobe effects
- Rapid opacity oscillation

```css
/* NEVER do this */
.dangerous-flash {
  animation: flash 0.1s infinite; /* Dangerous: 10 flashes/second */
}

/* Safe alternative */
.safe-pulse {
  animation: pulse 2s ease-in-out infinite; /* Safe: < 1 flash/second */
}
```

### 7.10 Performance Guidelines

#### Use Transform and Opacity

Animate only `transform` and `opacity` when possible—these properties are GPU-accelerated and don't trigger layout recalculations.

```css
/* ✅ Good: GPU-accelerated */
.card:hover {
  transform: translateY(-4px);
  opacity: 0.9;
}

/* ❌ Avoid: Triggers layout */
.card:hover {
  margin-top: -4px;
  height: 204px;
}
```

#### Use will-change Sparingly

`will-change` hints to the browser that an element will animate, but overuse consumes memory.

```css
/* Use only for elements that will definitely animate */
.modal {
  will-change: transform, opacity;
}

/* Remove after animation completes */
.modal.is-open {
  will-change: auto;
}
```

#### Avoid Animating Layout Properties

Properties that trigger layout recalculation are expensive:

| Avoid Animating | Use Instead |
|-----------------|-------------|
| `width`, `height` | `transform: scale()` |
| `top`, `left`, `right`, `bottom` | `transform: translate()` |
| `margin`, `padding` | `transform: translate()` |
| `border-width` | `box-shadow` or `outline` |

#### Contain Paint

For complex animated components, use `contain` to isolate repaints:

```css
.card {
  contain: layout paint;
}
```

### 7.11 Animation Utility Classes

```css
/* Duration utilities */
.duration-fast { animation-duration: var(--duration-fast); transition-duration: var(--duration-fast); }
.duration-normal { animation-duration: var(--duration-normal); transition-duration: var(--duration-normal); }
.duration-moderate { animation-duration: var(--duration-moderate); transition-duration: var(--duration-moderate); }
.duration-slow { animation-duration: var(--duration-slow); transition-duration: var(--duration-slow); }

/* Easing utilities */
.ease-default { animation-timing-function: var(--ease-default); transition-timing-function: var(--ease-default); }
.ease-in { animation-timing-function: var(--ease-in); transition-timing-function: var(--ease-in); }
.ease-out { animation-timing-function: var(--ease-out); transition-timing-function: var(--ease-out); }
.ease-in-out { animation-timing-function: var(--ease-in-out); transition-timing-function: var(--ease-in-out); }

/* Delay utilities */
.delay-100 { animation-delay: 100ms; transition-delay: 100ms; }
.delay-200 { animation-delay: 200ms; transition-delay: 200ms; }
.delay-300 { animation-delay: 300ms; transition-delay: 300ms; }
.delay-500 { animation-delay: 500ms; transition-delay: 500ms; }

/* Animation utilities */
.animate-fade-in { animation: fadeIn var(--duration-moderate) var(--ease-out) forwards; }
.animate-fade-out { animation: fadeOut var(--duration-moderate) var(--ease-in) forwards; }
.animate-slide-up { animation: slideUp var(--duration-moderate) var(--ease-out) forwards; }
.animate-scale-in { animation: scaleIn var(--duration-moderate) var(--ease-out) forwards; }
.animate-spin { animation: spin 1s linear infinite; }
.animate-pulse { animation: pulse 2s var(--ease-in-out) infinite; }
.animate-shimmer { animation: shimmer 1.5s infinite; }
```
---
# 8. Pages 

## 3. Pages (Detail)

This section provides design specifications for all pages. Pages are organised by template type, with key commercial pages receiving full specifications and supporting pages documented with template references and page-specific notes.

### 3.0 Page Templates

Before detailing individual pages, these reusable templates define common structural patterns.

---

#### Template A: Landing Page

Used for: Homepage, Membership, About, Start Here, How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                         [Header]                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                     [Hero Section]                              │
│              Full-width, gradient or image bg                   │
│                  Headline + Tagline + CTAs                      │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                  [Value Propositions]                           │
│              3-column cards with icons                          │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                  [Featured Content]                             │
│              Grid of cards (products/articles)                  │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    [CTA Section]                                │
│              Contrasting bg, conversion focus                   │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                  [Email Capture]                                │
├─────────────────────────────────────────────────────────────────┤
│                         [Footer]                                │
└─────────────────────────────────────────────────────────────────┘
```

---

#### Template B: Index/Listing Page

Used for: Browse, Authors, Eras, Themes, Collections, Blog Index, Reading Guides Index

```
┌─────────────────────────────────────────────────────────────────┐
│                         [Header]                                │
├─────────────────────────────────────────────────────────────────┤
│  [Breadcrumbs]                                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Page Title                                          [Sort ▼]   │
│  Description text (2-3 sentences)                               │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│           │                                                     │
│ [Filters] │  [Card] [Card] [Card] [Card]                       │
│           │  [Card] [Card] [Card] [Card]                       │
│  Genre    │  [Card] [Card] [Card] [Card]                       │
│  Era      │                                                     │
│  Format   │  [Pagination: ← 1 2 3 ... 10 →]                    │
│  Price    │                                                     │
│           │                                                     │
├─────────────────────────────────────────────────────────────────┤
│                         [Footer]                                │
└─────────────────────────────────────────────────────────────────┘
```

**Desktop:** Sidebar filters (240px) + content grid (3-4 columns)
**Mobile:** Filters collapse to modal triggered by "Filters" button

---

#### Template C: Detail Page

Used for: Product, Article, Author Profile, Reading Guide, Era, Theme

```
┌─────────────────────────────────────────────────────────────────┐
│                         [Header]                                │
├─────────────────────────────────────────────────────────────────┤
│  [Breadcrumbs]                                                  │
├─────────────────────────────────────────────────────────────────┤
│                    │                                            │
│   [Primary        │   Title (H1)                               │
│    Visual]        │   Metadata row                              │
│                   │   Key info / Price                          │
│   Cover image     │   [Primary CTA]                            │
│   or hero         │                                             │
│                    │                                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    [Content Body]                               │
│              Description, tabs, or article text                 │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                   [Related Items]                               │
│              Cards row or grid                                  │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                         [Footer]                                │
└─────────────────────────────────────────────────────────────────┘
```

**Desktop:** 2-column header (visual left, info right), single-column body
**Mobile:** Stacked single column, sticky CTA bar at bottom

---

#### Template D: Form Page

Used for: Login, Register, Forgot Password, Contact, Checkout, Newsletter

```
┌─────────────────────────────────────────────────────────────────┐
│                         [Header]                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    ┌─────────────────┐                         │
│                    │                 │                         │
│                    │  Form Title     │                         │
│                    │                 │                         │
│                    │  [Form Fields]  │                         │
│                    │                 │                         │
│                    │  [Submit CTA]   │                         │
│                    │                 │                         │
│                    │  Helper links   │                         │
│                    │                 │                         │
│                    └─────────────────┘                         │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                         [Footer]                                │
└─────────────────────────────────────────────────────────────────┘
```

**Container:** `.container-narrow` (540px max)
**Background:** Surface 200 with card (Surface 50) for form

---

#### Template E: Dashboard Page

Used for: Account, Library, Orders, Settings, Membership Management

```
┌─────────────────────────────────────────────────────────────────┐
│                         [Header]                                │
├─────────────────────────────────────────────────────────────────┤
│           │                                                     │
│ [Account  │  Page Title                                        │
│  Sidebar] │                                                     │
│           │  [Content Area]                                    │
│  Library  │                                                     │
│  Wishlist │  Tables, lists, cards, or settings forms           │
│  Orders   │                                                     │
│  Settings │                                                     │
│           │                                                     │
├─────────────────────────────────────────────────────────────────┤
│                         [Footer]                                │
└─────────────────────────────────────────────────────────────────┘
```

**Desktop:** Sidebar (240px) + content area
**Mobile:** Sidebar becomes horizontal tabs or dropdown menu

---

#### Template F: Content Page

Used for: Legal pages, FAQ, Help, Press, Status

```
┌─────────────────────────────────────────────────────────────────┐
│                         [Header]                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    Page Title (H1)                              │
│                    Last updated: [date]                         │
│                                                                 │
│              ┌─────────────────────────────┐                   │
│              │                             │                   │
│              │     [Long-form content]     │                   │
│              │     .container-content      │                   │
│              │     700px max width         │                   │
│              │                             │                   │
│              └─────────────────────────────┘                   │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                         [Footer]                                │
└─────────────────────────────────────────────────────────────────┘
```

---

### 3.1 Public Pages

#### 3.1.1 Homepage `/`

**Template:** Landing Page (A)

**Purpose:** Primary entry point demonstrating value, guiding users to content/products, capturing emails.

**Layout Structure:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header - Teal 900 bg]                                        │
│  Logo    Discover  Library  Articles  Membership  About  🔍👤🛒 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Hero Section - Full bleed]                        │
│              Background: Teal 900 → Teal 600 gradient           │
│              or vintage pulp art at 20% opacity                 │
│                                                                 │
│              "Where Golden Age                                  │
│               Science Fiction Lives"                            │
│              text-6xl, Outfit 800, Surface 200                  │
│                                                                 │
│              "Past Futures, Present Discoveries"                │
│              text-lg, Source Serif italic, Teal 200            │
│                                                                 │
│              [Explore Collection]  [View Membership]           │
│              Primary (Amber)       Secondary (outline)          │
│                                                                 │
│              Padding: 80px 0                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Value Propositions - Surface 200 bg]             │
│              3-column grid, 24px gap                            │
│                                                                 │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐              │
│  │ [icon]      │ │ [icon]      │ │ [icon]      │              │
│  │ Expert      │ │ Professional│ │ Guided      │              │
│  │ Curation    │ │ Quality     │ │ Discovery   │              │
│  │ 2-3 lines   │ │ 2-3 lines   │ │ 2-3 lines   │              │
│  └─────────────┘ └─────────────┘ └─────────────┘              │
│                                                                 │
│              Padding: 64px 0                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Featured This Week]                               │
│              Section label + H2                                 │
│                                                                 │
│  [Product]  [Product]  [Article]  [Collection]                 │
│  [Card]     [Card]     [Card]     [Card]                       │
│                                                                 │
│              4-column grid (3 on tablet, 1-2 on mobile)        │
│              Padding: 48px 0                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Recent Articles]                                  │
│              Section label + H2 + "View All →" link            │
│                                                                 │
│  [Article]  [Article]  [Article]                               │
│  [Card]     [Card]     [Card]                                  │
│                                                                 │
│              3-column grid                                      │
│              Padding: 48px 0                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Membership CTA - Teal 800 bg]                    │
│              Full bleed dark section                            │
│                                                                 │
│              "Join the Community"                               │
│              text-4xl, Outfit 700, Surface 200                  │
│                                                                 │
│              Value proposition paragraph                        │
│              Teal 200                                           │
│                                                                 │
│  ┌─────────┐ ┌─────────────┐ ┌─────────┐                      │
│  │Explorer │ │ Enthusiast  │ │Collector│                      │
│  │ £4.99   │ │   £8.99     │ │ £14.99  │                      │
│  │         │ │  ★ Popular  │ │         │                      │
│  │ [Join]  │ │   [Join]    │ │ [Join]  │                      │
│  └─────────┘ └─────────────┘ └─────────┘                      │
│                                                                 │
│              Padding: 80px 0                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Email Capture - Surface 300 bg]                  │
│                                                                 │
│              "Start Your Journey Free"                          │
│              "Curated recommendations, new articles,           │
│               and exclusive offers"                             │
│                                                                 │
│              [email@example.com        ] [Subscribe]           │
│                                                                 │
│              "Join 2,500+ readers. Unsubscribe anytime."       │
│              text-sm, Neutral 500                               │
│                                                                 │
│              Padding: 48px 0                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│  [Footer - Teal 900 bg]                                        │
└─────────────────────────────────────────────────────────────────┘
```

**Component Usage:**

- Header (dark variant)
- Hero with gradient background
- Value proposition cards (icon + heading + text)
- Product cards (standard)
- Article cards
- Membership tier cards
- Email capture form
- Footer (dark)

**Responsive Behaviour:**

- Hero: text-6xl → text-4xl on mobile, stack CTAs vertically
- Value props: 3-col → 1-col stack on mobile
- Featured grid: 4-col → 2-col (tablet) → 1-col (mobile)
- Membership cards: 3-col → vertical stack on mobile

**Key Metrics:**

- Bounce rate: <50%
- Email capture: 3-5%
- Primary CTA click-through: 8-12%

---

#### 3.1.2 About `/about`

**Template:** Landing Page (A) with content focus

**Sections:**

1. Hero: Mission statement headline + founder photo
2. Story: Long-form content block (700px) telling founder story
3. Values: 3-column value cards
4. Team: Founder bio card (if solo) or team grid
5. CTA: "Join the community" or newsletter capture

**Unique Elements:**

- Founder photo: 200px circle, border Amber 500
- Pull quote block with Outfit 500
- Timeline of milestones (optional)

---

#### 3.1.3 Contact `/contact`

**Template:** Form Page (D)

**Form Fields:**

- Name (required)
- Email (required)
- Subject (dropdown: General, Support, Press, Partnership)
- Message (textarea, required)
- Submit button

**Additional Content:**

- Response time expectation: "We typically respond within 24 hours"
- Direct email display: support@sfsupernova.com
- FAQ link: "Check our FAQ for quick answers"

---

#### 3.1.4 Blog Index `/blog`

**Template:** Index/Listing Page (B)

**Filter Options:**

- Category (Reviews, Guides, Author Profiles, History)
- None (simpler than product browse)

**Sort Options:**

- Newest (default)
- Popular
- A-Z

**Card Type:** Article card (16:9 image, title, excerpt, reading time)

**Pagination:** 12 articles per page

---

#### 3.1.5 Blog Post `/blog/[slug]`

**Template:** Detail Page (C) - Article variant

**Layout:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header]                                                       │
├─────────────────────────────────────────────────────────────────┤
│  Home / Blog / [Category] / Article Title                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Featured Image - 16:9]                            │
│              Full width within container                        │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Category Tag]                                     │
│                                                                 │
│              Article Title                                      │
│              text-4xl, Outfit 700                               │
│                                                                 │
│              By [Author] · [Date] · [Reading Time]             │
│              text-sm, Neutral 500                               │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│         ┌─────────────────────────────────────┐                │
│         │                                     │                │
│         │  [Article Body]                     │                │
│         │  .container-content (700px)         │                │
│         │                                     │                │
│         │  Source Serif 4, 18px               │                │
│         │  Line height 1.75                   │                │
│         │                                     │                │
│         │  H2: Outfit 700, text-2xl           │                │
│         │  H3: Outfit 600, text-xl            │                │
│         │                                     │                │
│         │  Blockquotes: Outfit 500            │                │
│         │  4px Amber left border              │                │
│         │                                     │                │
│         │  ─────────────────────────          │                │
│         │  [Mid-article email CTA]            │                │
│         │  ─────────────────────────          │                │
│         │                                     │                │
│         │  [Continue article...]              │                │
│         │                                     │                │
│         └─────────────────────────────────────┘                │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Author Bio Card]                                  │
│              Photo + name + short bio + link                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Related Articles]                                 │
│              3 article cards                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [End-of-article email CTA]                        │
│              Lead magnet if relevant                            │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│  [Footer]                                                       │
└─────────────────────────────────────────────────────────────────┘
```

**Mid-Article CTA (after ~50% of content):**

- Light card (Surface 100 bg)
- "Want more recommendations?"
- Email input + Subscribe button
- Inline within content flow

**Schema Markup:** Article schema with headline, author, datePublished, image

---

#### 3.1.6 Help Centre `/help`

**Template:** Content Page (F) with FAQ accordion

**Structure:**

1. Search bar (prominent)
2. Category cards (4): Account, Orders, Membership, Content
3. Popular articles list
4. Contact CTA at bottom

---

#### 3.1.7 FAQ `/faq`

**Template:** Content Page (F)

**Component:** Accordion groups by category

**Categories:**

- General (What is SF Supernova?, etc.)
- Products (Formats, Downloads, Compatibility)
- Membership (Tiers, Credits, Cancellation)
- Account (Password, Settings)
- Payment (Methods, Refunds)

**Accordion Behaviour:**

- Single expand (one open at a time)
- Chevron rotation on expand
- Smooth height animation

---

#### 3.1.8 Newsletter `/newsletter`

**Template:** Form Page (D)

**Content:**

- Headline: "Join Our Weekly Newsletter"
- Value proposition (3 bullet points)
- Email field + Subscribe button
- Privacy reassurance
- Sample newsletter preview (optional)

---

#### 3.1.9 Start Here `/start-here`

**Template:** Landing Page (A) - Onboarding focus

**Purpose:** Guide newcomers to vintage sci-fi

**Sections:**

1. Hero: "New to Vintage Sci-Fi?"
2. Curated starter paths (3 cards): "The Essentials", "By Theme", "By Era"
3. Interactive quiz CTA: "Find Your Perfect Starting Point"
4. Featured beginner-friendly products
5. Newsletter signup

---

#### 3.1.10 Press `/press`

**Template:** Content Page (F)

**Content:**

- About SF Supernova (press-friendly summary)
- Founder bio + high-res photo download
- Logo assets download (PNG, SVG)
- Press contact email
- Recent coverage/mentions (if any)

---

#### 3.1.11 Status `/status`

**Template:** Content Page (F) - Minimal

**Content:**

- Current system status (operational/degraded/down)
- Recent incidents list
- Uptime percentage
- Link to subscribe to status updates

**Styling:**

- Green/Amber/Red status indicators
- Minimal design, functional focus

---

#### 3.1.12 How It Works `/how-it-works`

**Template:** Landing Page (A)

**Sections:**

1. Hero: "How SF Supernova Works"
2. Step cards (3-4): Browse → Purchase → Download → Enjoy
3. Format explanation (ePub, PDF, Audiobook)
4. Device compatibility grid
5. Membership benefits overview
6. CTA: "Start Browsing"

---

### 3.2 Content Discovery

#### 3.2.1 Author Directory `/authors`

**Template:** Index/Listing Page (B) - Card variant

**Layout:** Alphabetical grid with letter jump links

```
A  B  C  D  E  F  G  H  I  J  K  L  M  N  O  P  Q  R  S  T  U  V  W  X  Y  Z

[Author] [Author] [Author] [Author]
[Card]   [Card]   [Card]   [Card]
```

**Card Type:** Author card (circular photo, name, dates, work count)

**Filter:** Era checkboxes (optional)

**Sort:** Alphabetical (default), Work count, Popularity

---

#### 3.2.2 Author Profile `/author/[slug]`

**Template:** Detail Page (C) - Author variant

**Layout:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Breadcrumbs: Home / Authors / Isaac Asimov]                  │
├─────────────────────────────────────────────────────────────────┤
│                    │                                            │
│   [Author Photo]   │   Isaac Asimov                            │
│   200px circle     │   (1920–1992)                             │
│                    │                                            │
│                    │   [Era tags] [Theme tags]                 │
│                    │                                            │
│                    │   "The father of robotics fiction..."     │
│                    │   Brief intro (2-3 sentences)              │
│                    │                                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  [Biography - Tabs or Accordion]                               │
│                                                                 │
│  Life | Works | Influence | Further Reading                    │
│  ─────────────────────────────────────────                     │
│                                                                 │
│  [Tab content - long form, .container-content]                 │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  [Available Works]                                              │
│  Product grid (their books/audiobooks available on site)       │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  [Related Authors]                                              │
│  "If you like Asimov, explore..."                              │
│  Author cards row                                               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

#### 3.2.3 Eras Index `/eras`

**Template:** Index/Listing Page (B) - Visual variant

**Layout:** Large era cards with period imagery

```
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   [1920s]       │ │   [1930s]       │ │   [1940s]       │
│   Pulp Era      │ │   Golden Age    │ │   WWII Era      │
│   Begins        │ │   Dawns         │ │                 │
│   43 works      │ │   127 works     │ │   89 works      │
│   [Explore →]   │ │   [Explore →]   │ │   [Explore →]   │
└─────────────────┘ └─────────────────┘ └─────────────────┘
```

**Card:** Large (spans 4 columns), period-appropriate cover art background

---

#### 3.2.4 Era Page `/eras/[slug]`

**Template:** Index/Listing Page (B)

**Header:** Era name, date range, description paragraph, representative image

**Content:** Product grid filtered to era, with additional filters (theme, format)

---

#### 3.2.5 Themes Index `/themes`

**Template:** Index/Listing Page (B) - Visual variant

**Layout:** Theme cards with icons or representative imagery

**Card Display:** Icon + Theme name + work count

---

#### 3.2.6 Theme Page `/themes/[slug]`

**Template:** Index/Listing Page (B)

**Header:** Theme name, description, "Why this theme matters" paragraph

**Content:** Product grid filtered to theme

---

#### 3.2.7–3.2.8 Category/Tag Archive

**Template:** Index/Listing Page (B)

Standard archive pages with header and filtered product/article grid.

---

#### 3.2.9 Collections `/collections`

**Template:** Index/Listing Page (B) - Featured variant

**Content:** Curated collection cards (larger format with descriptions)

**Card Type:** Collection card with cover montage, title, description, item count, price

---

#### 3.2.10 New Arrivals `/new-arrivals`

**Template:** Index/Listing Page (B)

**Sort:** Newest first (fixed)

**Filter:** Format, Era, Theme

---

#### 3.2.11 Popular `/popular`

**Template:** Index/Listing Page (B)

**Sort:** Popularity (fixed)

**Content:** Best-selling/most-viewed products

---

### 3.3 Free Content

#### 3.3.1 Free Content Hub `/free`

**Template:** Landing Page (A) - Feature showcase

**Sections:**

1. Hero: "Explore Free Content"
2. Category cards: Free Ebooks, Free Audiobooks, Radio Dramas
3. Featured free items grid
4. "Want more?" Membership CTA

---

#### 3.3.2–3.3.3 Free Ebooks/Audiobooks

**Template:** Index/Listing Page (B)

Standard browse filtered to free items with format pre-selected.

---

#### 3.3.4 Radio Dramas Index `/radio-dramas`

**Template:** Index/Listing Page (B)

**Card Type:** Show card (show artwork, title, episode count, era)

---

#### 3.3.5 Radio Show `/radio-dramas/[show-slug]`

**Template:** Detail Page (C)

**Content:**

- Show artwork and description
- Episode list (sortable by date, episode number)
- "Play All" functionality

---

#### 3.3.6 Radio Episode `/radio-dramas/[show-slug]/[episode-slug]`

**Template:** Detail Page (C) - Audio variant

**Content:**

- Audio player (prominent)
- Episode title, show name, date, duration
- Description/synopsis
- Transcript (expandable)
- Previous/Next episode navigation

---

### 3.4 Reading Guides & Lists

#### 3.4.1 Reading Guides Index `/reading-guides`

**Template:** Index/Listing Page (B)

**Card Type:** Article card with "Guide" tag

---

#### 3.4.2 Reading Guide `/reading-guides/[slug]`

**Template:** Detail Page (C) - Article variant

**Unique Elements:**

- Checklist component (interactive checkboxes for tracking)
- "Download PDF" CTA (lead magnet)
- Embedded product cards for referenced works

---

#### 3.4.3–3.4.4 Reading Lists

Similar to Reading Guides but lighter content, more list-focused.

---

### 3.5 Commerce

#### 3.5.1 Browse `/browse`

**Template:** Index/Listing Page (B)

**Full Specification:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header]                                                       │
├─────────────────────────────────────────────────────────────────┤
│  Home / Browse                                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Browse All Products                          Showing 127 items │
│                                               [Sort: Popular ▼] │
│                                                                 │
├───────────────┬─────────────────────────────────────────────────┤
│               │                                                 │
│  [Filters]    │  [Product] [Product] [Product] [Product]       │
│  240px        │  [Card]    [Card]    [Card]    [Card]          │
│               │                                                 │
│  Format       │  [Product] [Product] [Product] [Product]       │
│  ☑ Ebook (98) │  [Card]    [Card]    [Card]    [Card]          │
│  ☐ Audio (56) │                                                 │
│  ☐ Bundle(12) │  [Product] [Product] [Product] [Product]       │
│               │  [Card]    [Card]    [Card]    [Card]          │
│  Era          │                                                 │
│  ☐ 1920s (12) │                                                 │
│  ☐ 1930s (34) │  [← Previous]  1  2  3  4  5 ... 10  [Next →]  │
│  ☑ 1940s (45) │                                                 │
│  ☐ 1950s (67) │                                                 │
│  [Show more]  │                                                 │
│               │                                                 │
│  Theme        │                                                 │
│  ☐ Time Travel│                                                 │
│  ☐ Space Opera│                                                 │
│  ☐ Dystopia   │                                                 │
│  [Show more]  │                                                 │
│               │                                                 │
│  Price        │                                                 │
│  ☐ Under £3   │                                                 │
│  ☐ £3–£5      │                                                 │
│  ☐ Over £5    │                                                 │
│               │                                                 │
│  [Clear All]  │                                                 │
│               │                                                 │
├───────────────┴─────────────────────────────────────────────────┤
│  [Footer]                                                       │
└─────────────────────────────────────────────────────────────────┘
```

**Filter Behaviour:**

- Multi-select within groups
- Show result count per option
- Update results instantly (no "Apply" button)
- Active filters shown as removable chips above grid
- "Clear All" resets all filters

**Sort Options:**

- Relevance (default)
- Popularity
- Price: Low to High
- Price: High to Low
- Newest
- Title: A-Z

**Grid:** 4 columns (desktop), 3 (tablet), 2 (mobile)

**Pagination:** 20 items per page

**Mobile Filter Pattern:**

```
┌────────────────────────────────┐
│  Browse Products     [Filters] │ ← Button triggers modal
│  127 items           [Sort ▼]  │
├────────────────────────────────┤
│  [Active filter chips]         │
├────────────────────────────────┤
│  [Product] [Product]           │
│  [Card]    [Card]              │
```

Filter modal: Full-screen overlay with all filter groups, "Show Results" CTA at bottom

---

#### 3.5.2 Browse by Genre `/browse/[genre]`

**Template:** Index/Listing Page (B)

Same as Browse but with genre pre-filtered and header specific to genre.

---

#### 3.5.3 Product Page `/product/[slug]`

**Template:** Detail Page (C) - Product variant

**Full Specification:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header]                                                       │
├─────────────────────────────────────────────────────────────────┤
│  Home / Library / Ebooks / Foundation                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────┐    Foundation                              │
│  │                 │    by Isaac Asimov                         │
│  │                 │                                            │
│  │  [Cover Image]  │    [1950s] [Space Opera] [Essential]      │
│  │                 │                                            │
│  │  400px max      │    ★★★★★ (47 reviews)                      │
│  │  3:4 aspect     │                                            │
│  │                 │    £3.99                                   │
│  │                 │    Members: £3.19 (save 20%)               │
│  │                 │                                            │
│  │                 │    Format: [ePub ▼]                        │
│  │                 │                                            │
│  │                 │    [Add to Cart]  btn-primary, btn-lg      │
│  │                 │    [♡ Add to Wishlist]                     │
│  │                 │                                            │
│  │  [Read Sample]  │    ──────────────────────                  │
│  │  btn-secondary  │    📄 ePub, 2.4 MB                         │
│  │                 │    🕐 8 hour read                          │
│  └─────────────────┘    📅 Originally published 1951            │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  [Synopsis] [Author] [Historical Context] [Reviews]            │
│  ─────────────────────────────────────────────────              │
│                                                                 │
│  [Tab content]                                                  │
│                                                                 │
│  The Galactic Empire is crumbling. Hari Seldon has foreseen    │
│  the coming dark age and established the Foundation to         │
│  preserve human knowledge...                                    │
│                                                                 │
│  [Read more]                                                    │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Frequently Bought Together                                     │
│                                                                 │
│  [Foundation] + [Foundation and Empire] + [Second Foundation]  │
│  [This item]    £3.99                      £3.99               │
│                                                                 │
│  Total: £11.97  →  Bundle price: £9.99 (save 17%)              │
│  [Add All to Cart]                                              │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Similar Works                                                  │
│                                                                 │
│  [Product] [Product] [Product] [Product]                       │
│  [Card]    [Card]    [Card]    [Card]                          │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  [Membership CTA Banner]                                        │
│  "Members save 20-40% on every purchase"                       │
│  [Learn More]                                                   │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│  [Footer]                                                       │
└─────────────────────────────────────────────────────────────────┘
```

**Mobile Layout:**

```
┌────────────────────────────────┐
│  [Header]                      │
├────────────────────────────────┤
│  [Breadcrumbs - collapsed]     │
├────────────────────────────────┤
│                                │
│      [Cover Image]             │
│      Full width                │
│                                │
├────────────────────────────────┤
│  Foundation                    │
│  by Isaac Asimov               │
│                                │
│  [Tags row]                    │
│                                │
│  £3.99                         │
│  Members: £3.19                │
│                                │
│  [Read Sample]                 │
│                                │
├────────────────────────────────┤
│  [Tabs: Synopsis | Author...]  │
├────────────────────────────────┤
│  [Tab content]                 │
├────────────────────────────────┤
│  [Similar Works carousel]      │
├────────────────────────────────┤
│  [Footer]                      │
├────────────────────────────────┤
│  ┌────────────────────────┐    │ ← Sticky bottom bar
│  │ £3.99   [Add to Cart]  │    │
│  └────────────────────────┘    │
└────────────────────────────────┘
```

**Sample Modal:**

- Text sample: First chapter in reader modal
- Audio sample: Inline player, 5-minute excerpt

**Add to Cart Behaviour:**

1. Button shows loading spinner
2. Text changes to "Adding..."
3. Success: "Added ✓" for 2 seconds
4. Cart icon badge updates
5. Optional: Mini-cart drawer slides in

---

#### 3.5.4 Search Results `/search`

**Template:** Index/Listing Page (B) - Search variant

**Layout:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header with search expanded]                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Search: "asimov foundation"                    [Clear] [🔍]   │
│                                                                 │
│  47 results for "asimov foundation"                            │
│                                                                 │
│  [All] [Products (23)] [Articles (18)] [Authors (6)]          │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  [Mixed results grid - cards vary by type]                     │
│                                                                 │
│  No sidebar filters on search (rely on content type tabs)      │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│  [Footer]                                                       │
└─────────────────────────────────────────────────────────────────┘
```

**No Results State:**

- "No results for [query]"
- Suggestions: "Try different keywords" or browse categories
- Popular searches list

---

#### 3.5.5 Cart `/cart`

**Template:** Custom (Form Page variant)

**Layout:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header]                                                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Your Cart (3 items)                                           │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ [Cover]  Foundation                           £3.99     │   │
│  │  80px    Isaac Asimov · ePub                           │   │
│  │          [Remove]                                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ [Cover]  The Stars My Destination             £4.99     │   │
│  │  80px    Alfred Bester · ePub                          │   │
│  │          [Remove]                                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ [Cover]  Foundation Series (Audiobook)       £14.99     │   │
│  │  80px    Isaac Asimov · MP3 Bundle                     │   │
│  │          [Remove]                                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  [Frequently Bought Together suggestion]                       │
│                                                                 │
├───────────────────────────────────────┬─────────────────────────┤
│                                       │                         │
│  [Continue Shopping]                  │   Subtotal:    £23.97  │
│                                       │   Member      -£4.79   │
│                                       │   Discount:            │
│                                       │   ─────────────────    │
│                                       │   Total:       £19.18  │
│                                       │                         │
│                                       │   [Proceed to Checkout]│
│                                       │   btn-primary, btn-lg  │
│                                       │                         │
│                                       │   🔒 Secure checkout    │
│                                       │                         │
└───────────────────────────────────────┴─────────────────────────┘
```

**Empty Cart:**

- "Your cart is empty"
- "Discover something new" CTA → Browse
- Featured products below

**Remove Animation:** Item fades out and collapses (300ms)

---

#### 3.5.6 Checkout `/checkout`

**Template:** Custom (Single-page checkout)

**Layout:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Minimal Header - Logo only, no nav]                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Checkout                                                       │
│                                                                 │
├─────────────────────────────────────┬───────────────────────────┤
│                                     │                           │
│  Contact Information                │   Order Summary           │
│  ────────────────────               │                           │
│  Email *                            │   [Cover] Foundation      │
│  [________________________]         │           £3.99           │
│                                     │                           │
│  ☐ Email me with news and offers   │   [Cover] Stars My...     │
│                                     │           £4.99           │
│  Billing Address                    │                           │
│  ────────────────────               │   ─────────────────       │
│  Country *                          │   Subtotal    £23.97     │
│  [United Kingdom           ▼]       │   Discount    -£4.79     │
│                                     │   ─────────────────       │
│  First Name *    Last Name *        │   Total       £19.18     │
│  [___________]   [___________]      │                           │
│                                     │   [Edit cart]             │
│  Payment                            │                           │
│  ────────────────────               │                           │
│                                     │                           │
│  [Stripe Payment Element]           │                           │
│  Card number                        │                           │
│  [____ ____ ____ ____]             │                           │
│  Expiry    CVC                      │                           │
│  [__/__]   [___]                   │                           │
│                                     │                           │
│  [Complete Purchase]                │                           │
│  btn-primary, btn-lg, full width   │                           │
│                                     │                           │
│  🔒 Secured by Stripe              │                           │
│  Visa  MC  Amex  icons             │                           │
│                                     │                           │
└─────────────────────────────────────┴───────────────────────────┘
```

**Mobile Layout:** Single column, order summary collapsed to expandable accordion at top

**Processing State:**

- Button disabled, shows spinner
- "Processing payment..."
- Overlay prevents interaction

**Error States:**

- Inline field errors (red border + message)
- Payment error alert at top of form

---

#### 3.5.7 Order Confirmation `/checkout/confirmation`

**Template:** Custom (Success page)

**Layout:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Minimal Header]                                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              ✓                                                  │
│              Success icon (Teal, 64px)                         │
│                                                                 │
│              Thank you for your order!                          │
│              text-3xl, Outfit 700                               │
│                                                                 │
│              Order #SF-12345                                    │
│              Confirmation sent to you@email.com                │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              Your Downloads                                     │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ [Cover]  Foundation              [Download ePub]        │   │
│  │          Isaac Asimov                                   │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ [Cover]  The Stars My Dest...    [Download ePub]        │   │
│  │          Alfred Bester                                  │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│              [Download All]                                     │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              What's Next?                                       │
│                                                                 │
│              • Downloads also sent to your email               │
│              • Access anytime from your account                │
│              • Need help? Visit our FAQ                        │
│                                                                 │
│              [Continue Browsing]    [Go to Library]            │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Membership CTA - if not member]                  │
│              "Enjoyed this? Members save 20-40%"               │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│  [Footer]                                                       │
└─────────────────────────────────────────────────────────────────┘
```

---

#### 3.5.8 Gift Cards `/gift-cards`

**Template:** Landing Page (A) - Product focus

**Sections:**

1. Hero: "Give the Gift of Golden Age Sci-Fi"
2. Gift card amount options (£10, £25, £50, £100, Custom)
3. How it works (3 steps)
4. Delivery options (email, print at home)
5. FAQ section

---

#### 3.5.9 File Formats Guide `/formats`

**Template:** Content Page (F)

**Content:**

- Format comparison table (ePub vs PDF vs Audiobook)
- Device compatibility chart
- Download instructions per device type
- Troubleshooting FAQ

---

### 3.6 Membership

#### 3.6.1 Membership `/membership`

**Template:** Landing Page (A) - Conversion focus

**Layout:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header]                                                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Hero - Teal gradient]                            │
│              "Unlock Your Sci-Fi Library"                       │
│              Value proposition paragraph                        │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Monthly] / [Annual - Save 17%]  ← Toggle         │
│                                                                 │
│  ┌─────────────┐ ┌─────────────────┐ ┌─────────────┐          │
│  │             │ │  ★ Most Popular │ │             │          │
│  │  Explorer   │ │   Enthusiast    │ │  Collector  │          │
│  │             │ │                 │ │             │          │
│  │   £4.99     │ │     £8.99       │ │   £14.99    │          │
│  │   /month    │ │     /month      │ │   /month    │          │
│  │             │ │                 │ │             │          │
│  │ ✓ 20% off   │ │ ✓ 30% off       │ │ ✓ 40% off   │          │
│  │ ✓ Ad-free   │ │ ✓ 2 credits/mo  │ │ ✓ 4 credits │          │
│  │ ✓ Early     │ │ ✓ Exclusive     │ │ ✓ VIP       │          │
│  │   access    │ │   content       │ │   access    │          │
│  │             │ │                 │ │             │          │
│  │ [Choose]    │ │ [Choose]        │ │ [Choose]    │          │
│  │             │ │ Amber button    │ │             │          │
│  └─────────────┘ └─────────────────┘ └─────────────┘          │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Feature Comparison Table]                        │
│              Detailed feature-by-tier breakdown                │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [Testimonials]                                     │
│              Member quotes (when available)                     │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│              [FAQ Accordion]                                    │
│              Common membership questions                        │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│  [Footer]                                                       │
└─────────────────────────────────────────────────────────────────┘
```

**Pricing Toggle:**

- Monthly/Annual switch
- Annual shows savings badge
- Prices update without page reload

**Popular Tier Highlight:**

- Amber border
- "Most Popular" badge
- Slightly elevated (shadow or scale)

---

#### 3.6.2 Compare Memberships `/membership/compare`

**Template:** Content Page (F) with table

**Content:** Full feature comparison table with all tiers and all features

---

#### 3.6.3 Gift Membership `/membership/gift`

**Template:** Form Page (D)

**Form:**

- Recipient name, email
- Tier selection
- Duration (1, 3, 6, 12 months)
- Personal message
- Delivery date
- Payment

---

### 3.7 Account

#### 3.7.1 Account Dashboard `/account`

**Template:** Dashboard Page (E)

**Layout:**

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header]                                                       │
├─────────────────────────────────────────────────────────────────┤
│               │                                                 │
│  [Sidebar]    │   Welcome back, [Name]                         │
│               │                                                 │
│  Dashboard ●  │   ┌──────────────────┐ ┌──────────────────┐    │
│  Library      │   │ Membership       │ │ Credits          │    │
│  Wishlist     │   │ Enthusiast       │ │ 2 remaining      │    │
│  Reading      │   │ Renews Dec 15    │ │ [Use Credit]     │    │
│  History      │   │ [Manage]         │ │                  │    │
│  My Lists     │   └──────────────────┘ └──────────────────┘    │
│  Orders       │                                                 │
│  Downloads    │   Recent Activity                               │
│  Credits      │   ─────────────────                             │
│  Membership   │                                                 │
│  Settings     │   [Order card] [Order card]                    │
│               │                                                 │
│  ─────────    │   Quick Actions                                │
│  [Logout]     │   [Browse Library] [View Downloads]            │
│               │                                                 │
├───────────────┴─────────────────────────────────────────────────┤
│  [Footer]                                                       │
└─────────────────────────────────────────────────────────────────┘
```

**Mobile:** Sidebar becomes horizontal nav or dropdown

---

#### 3.7.2 My Library `/account/library`

**Template:** Dashboard Page (E)

**Content:** Grid of purchased products with download buttons, format filters

---

#### 3.7.3 Wishlist `/account/wishlist`

**Template:** Dashboard Page (E)

**Content:** Product cards with "Move to Cart" and "Remove" actions

---

#### 3.7.4 Reading History `/account/reading-history`

**Template:** Dashboard Page (E)

**Content:** Chronological list of viewed/started products

---

#### 3.7.5–3.7.6 My Lists

**Template:** Dashboard Page (E)

**Content:** User-created lists with add/remove/reorder functionality

---

#### 3.7.7 Order History `/account/orders`

**Template:** Dashboard Page (E)

**Content:** Table of orders (date, items, total, status, actions)

---

#### 3.7.8 Order Detail `/account/orders/[id]`

**Template:** Dashboard Page (E)

**Content:** Full order details, download links, invoice download

---

#### 3.7.9 Downloads `/account/downloads`

**Template:** Dashboard Page (E)

**Content:** All available downloads with format, size, download button

---

#### 3.7.10 Audiobook Credits `/account/credits`

**Template:** Dashboard Page (E)

**Content:** Credit balance, usage history, available audiobooks to claim

---

#### 3.7.11 Membership Management `/account/membership`

**Template:** Dashboard Page (E)

**Content:**

- Current plan details
- Upgrade/downgrade options
- Billing history
- Update payment method
- Cancel membership (clear, ethical flow)

---

#### 3.7.12 Settings `/account/settings`

**Template:** Dashboard Page (E)

**Sections:**

- Profile (name, email)
- Password change
- Email preferences
- Connected accounts (if social login)
- Delete account

---

### 3.8 Auth

#### 3.8.1 Login `/login`

**Template:** Form Page (D)

**Form:**

- Email
- Password
- Remember me checkbox
- [Login] button
- "Forgot password?" link
- "Don't have an account? Register" link
- Social login options (if enabled)

---

#### 3.8.2 Register `/register`

**Template:** Form Page (D)

**Form:**

- Email
- Password
- Confirm password
- Newsletter opt-in checkbox
- Terms acceptance checkbox
- [Create Account] button
- "Already have an account? Login" link

---

#### 3.8.3 Forgot Password `/forgot-password`

**Template:** Form Page (D)

**Flow:**

1. Email input → Submit
2. Success message: "Check your email for reset link"
3. Reset page: New password + confirm → Submit
4. Success: "Password updated" → Login link

---

### 3.9 Legal

All legal pages use **Template F: Content Page**

**Common Elements:**

- Last updated date
- Table of contents (for long pages)
- Print-friendly styling
- 700px content width

#### 3.9.1 Privacy Policy `/privacy`

Standard privacy policy with GDPR compliance sections.

#### 3.9.2 Terms of Service `/terms`

Terms and conditions of use.

#### 3.9.3 Refund Policy `/refunds`

14-day money-back guarantee details.

#### 3.9.4 Accessibility `/accessibility`

WCAG compliance statement, known issues, contact for assistance.

#### 3.9.5 Cookie Policy `/cookies`

Cookie usage explanation, categories, management options.

#### 3.9.6 Copyright & DMCA `/copyright`

Copyright policy, DMCA takedown procedures.

#### 3.9.7 Licensing `/licensing`

Content licensing information.

---

### 3.10 Error Pages

#### 3.10.1 Not Found `/404`

**Template:** Custom (minimal)

```
┌─────────────────────────────────────────────────────────────────┐
│  [Header]                                                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                         404                                     │
│              text-6xl, Outfit 800, Teal 600                    │
│                                                                 │
│              "Lost in Space"                                    │
│              text-2xl, Outfit 600                               │
│                                                                 │
│              The page you're looking for                        │
│              doesn't exist or has moved.                        │
│                                                                 │
│              [Back to Homepage]  [Browse Products]             │
│                                                                 │
│              ─────────────────────────                         │
│                                                                 │
│              Popular destinations:                              │
│              • Browse All Products                              │
│              • Latest Articles                                  │
│              • Contact Support                                  │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│  [Footer]                                                       │
└─────────────────────────────────────────────────────────────────┘
```

---

#### 3.10.2 Server Error `/500`

**Template:** Custom (minimal)

```
┌─────────────────────────────────────────────────────────────────┐
│  [Minimal Header - Logo only]                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                         500                                     │
│              text-6xl, Outfit 800, Error text                  │
│                                                                 │
│              "Something Went Wrong"                             │
│                                                                 │
│              We're experiencing technical difficulties.         │
│              Please try again in a few minutes.                │
│                                                                 │
│              [Try Again]  [Go to Homepage]                     │
│                                                                 │
│              If this persists, contact                         │
│              support@sfsupernova.com                           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Note:** 500 page must be static HTML (no database/server dependencies)

---

### 9. Pages (Detail) *(currently numbered as Section 3)*

#### 9.1 Public
- 9.1.1 Homepage `/` **⚠️ MISSING: Page specification**
- 9.1.2 About `/about` **⚠️ MISSING: Page specification**
- 9.1.3 Contact `/contact` **⚠️ MISSING: Page specification**
- *(etc. — all subsections exist as headings but lack content)*

#### 9.2 Content Discovery
*(All subsections exist as headings but lack content)*

#### 9.3 Free Content
*(All subsections exist as headings but lack content)*

#### 9.4 Reading Guides & Lists
*(All subsections exist as headings but lack content)*

#### 9.5 Commerce
*(All subsections exist as headings but lack content)*

#### 9.6 Membership
*(All subsections exist as headings but lack content)*

#### 9.7 Account
*(All subsections exist as headings but lack content)*

#### 9.8 Auth
*(All subsections exist as headings but lack content)*

#### 9.9 Legal
*(All subsections exist as headings but lack content)*

#### 9.10 Error
*(All subsections exist as headings but lack content)*

---

### ⚠️ MISSING: 10. Responsive Patterns
**⚠️ MISSING: 10.1 Breakpoint Behaviours**
**⚠️ MISSING: 10.2 Mobile Navigation**
**⚠️ MISSING: 10.3 Touch Targets**
**⚠️ MISSING: 10.4 Content Reflow Patterns**


/* Complete responsive utility classes */

/* Display utilities */
.d-none { display: none; }
.d-block { display: block; }
.d-flex { display: flex; }
.d-grid { display: grid; }

@media (min-width: 768px) {
  .md\:d-none { display: none; }
  .md\:d-block { display: block; }
  .md\:d-flex { display: flex; }
  .md\:d-grid { display: grid; }
}

@media (min-width: 1024px) {
  .lg\:d-none { display: none; }
  .lg\:d-block { display: block; }
  .lg\:d-flex { display: flex; }
  .lg\:d-grid { display: grid; }
}

/* Flex direction */
.flex-col { flex-direction: column; }
.flex-row { flex-direction: row; }

@media (min-width: 768px) {
  .md\:flex-col { flex-direction: column; }
  .md\:flex-row { flex-direction: row; }
}

@media (min-width: 1024px) {
  .lg\:flex-col { flex-direction: column; }
  .lg\:flex-row { flex-direction: row; }
}

/* Grid columns */
.grid-cols-1 { grid-template-columns: repeat(1, 1fr); }
.grid-cols-2 { grid-template-columns: repeat(2, 1fr); }
.grid-cols-3 { grid-template-columns: repeat(3, 1fr); }
.grid-cols-4 { grid-template-columns: repeat(4, 1fr); }

@media (min-width: 768px) {
  .md\:grid-cols-2 { grid-template-columns: repeat(2, 1fr); }
  .md\:grid-cols-3 { grid-template-columns: repeat(3, 1fr); }
  .md\:grid-cols-4 { grid-template-columns: repeat(4, 1fr); }
}

@media (min-width: 1024px) {
  .lg\:grid-cols-3 { grid-template-columns: repeat(3, 1fr); }
  .lg\:grid-cols-4 { grid-template-columns: repeat(4, 1fr); }
  .lg\:grid-cols-6 { grid-template-columns: repeat(6, 1fr); }
}

/* Gap */
.gap-sm { gap: 8px; }
.gap-md { gap: 16px; }
.gap-lg { gap: 24px; }

@media (min-width: 1024px) {
  .lg\:gap-lg { gap: 24px; }
  .lg\:gap-xl { gap: 32px; }
}

/* Text alignment */
.text-left { text-align: left; }
.text-center { text-align: center; }
.text-right { text-align: right; }

@media (min-width: 768px) {
  .md\:text-left { text-align: left; }
  .md\:text-center { text-align: center; }
}

/* Padding */
.p-sm { padding: 8px; }
.p-md { padding: 16px; }
.p-lg { padding: 24px; }

@media (min-width: 768px) {
  .md\:p-lg { padding: 24px; }
  .md\:p-xl { padding: 32px; }
}

@media (min-width: 1024px) {
  .lg\:p-xl { padding: 32px; }
  .lg\:p-xxl { padding: 48px; }
}











---


## 11. Accessibility

SF Supernova is committed to WCAG 2.1 AA compliance, ensuring the platform is usable by everyone regardless of ability. This section consolidates accessibility requirements and provides implementation guidance.

**Core Principle:** Accessibility is not an afterthought—it's built into every component, pattern, and page from the start.

### 11.1 Focus Indicators

Focus indicators show which element currently has keyboard focus. They are essential for keyboard and assistive technology users.

#### Focus Ring Specification

| Property | Value |
|----------|-------|
| Colour (light bg) | Amber 500 (`#C9943A`) |
| Colour (dark bg) | Surface 200 (`#E8E3D6`) |
| Width | 2px |
| Style | solid |
| Offset | 2px |
| Border radius | Element's border-radius + 2px |

#### Focus-Visible Strategy

Use `:focus-visible` to show focus rings only for keyboard navigation, not mouse clicks:

```css
/* Remove default browser outline */
:focus {
  outline: none;
}

/* Show focus ring for keyboard users */
:focus-visible {
  outline: 2px solid var(--amber-500);
  outline-offset: 2px;
}

/* Fallback for browsers without :focus-visible */
@supports not selector(:focus-visible) {
  :focus {
    outline: 2px solid var(--amber-500);
    outline-offset: 2px;
  }
}
```

#### Focus by Element Type

| Element | Focus Style |
|---------|-------------|
| **Buttons** | 2px Amber 500 outline, 2px offset |
| **Links** | 2px Amber 500 outline, 2px offset, 2px border-radius |
| **Form inputs** | 2px Teal 600 border (replaces default border) |
| **Cards (clickable)** | 2px Amber 500 outline, 2px offset |
| **Checkboxes/Radios** | 2px Amber 500 outline on custom element |
| **Dropdowns/Selects** | 2px Teal 600 border |
| **Modal close button** | 2px Amber 500 outline |
| **Nav items (dark bg)** | 2px Surface 200 outline |

#### Input Focus (Border Style)

Form inputs use border change rather than outline for cleaner appearance:

```css
input:focus,
textarea:focus,
select:focus {
  outline: none;
  border: 2px solid var(--teal-600);
  background-color: var(--surface-0);
}

/* Adjust padding to prevent layout shift */
input {
  border: 1px solid var(--surface-400);
  padding: 12px 16px;
}

input:focus {
  border: 2px solid var(--teal-600);
  padding: 11px 15px; /* Reduce by 1px to compensate */
}
```

#### Focus on Dark Backgrounds

```css
/* Header, footer, mobile nav */
.dark-bg :focus-visible {
  outline-color: var(--surface-200);
}

.dark-bg a:focus-visible,
.dark-bg button:focus-visible {
  outline: 2px solid var(--surface-200);
  outline-offset: 2px;
}
```

#### Focus Within (Parent Highlighting)

For complex components, highlight parent when child has focus:

```css
.card:focus-within {
  box-shadow: 0 0 0 2px var(--amber-500);
}

.form-field:focus-within label {
  color: var(--teal-600);
}
```

#### Never Remove Focus Indicators

```css
/* ❌ NEVER do this */
*:focus {
  outline: none;
}

/* ✅ Always provide alternative */
button:focus {
  outline: none;
  box-shadow: 0 0 0 2px var(--amber-500);
}
```

---

### 11.2 Colour Contrast Requirements

#### WCAG Contrast Ratios

| Level | Normal Text (<18px) | Large Text (≥18px bold, ≥24px) | UI Components |
|-------|---------------------|-------------------------------|---------------|
| **AA (minimum)** | 4.5:1 | 3:1 | 3:1 |
| **AAA (enhanced)** | 7:1 | 4.5:1 | n/a |

**SF Supernova targets AA compliance minimum, AAA where practical.**

#### Verified Colour Pairings

| Foreground | Background | Ratio | Level |
|------------|------------|-------|-------|
| Neutral 900 (`#1A1A1A`) | Surface 200 (`#E8E3D6`) | 12.4:1 | AAA ✓ |
| Neutral 800 (`#333333`) | Surface 200 (`#E8E3D6`) | 9.1:1 | AAA ✓ |
| Teal 600 (`#1A4A4A`) | Surface 200 (`#E8E3D6`) | 7.2:1 | AAA ✓ |
| Teal 700 (`#153D3D`) | Surface 200 (`#E8E3D6`) | 8.5:1 | AAA ✓ |
| Surface 200 (`#E8E3D6`) | Teal 900 (`#0F3333`) | 10.1:1 | AAA ✓ |
| Teal 200 (`#7DBDBD`) | Teal 900 (`#0F3333`) | 5.8:1 | AA ✓ |
| Amber 500 (`#C9943A`) | Teal 900 (`#0F3333`) | 5.2:1 | AA ✓ |
| Neutral 500 (`#737373`) | Surface 200 (`#E8E3D6`) | 4.6:1 | AA ✓ |

#### Problematic Pairings to Avoid

| Foreground | Background | Ratio | Issue |
|------------|------------|-------|-------|
| Neutral 400 | Surface 200 | 2.8:1 | ❌ Fails AA |
| Teal 300 | Surface 100 | 2.1:1 | ❌ Fails AA |
| Amber 300 | Surface 200 | 1.9:1 | ❌ Fails AA |

#### Text Colour Usage

```css
/* Primary text - use for headings, body copy */
.text-primary {
  color: var(--neutral-900); /* 12.4:1 on Surface 200 */
}

/* Secondary text - use for supporting content */
.text-secondary {
  color: var(--neutral-700); /* 7.2:1 on Surface 200 */
}

/* Muted text - use sparingly, larger sizes only */
.text-muted {
  color: var(--neutral-500); /* 4.6:1 on Surface 200 - AA for normal text */
}

/* ❌ Don't use for small text */
.text-placeholder {
  color: var(--neutral-400); /* 2.8:1 - fails, use only for decorative */
}
```

#### Link Contrast

Links must be distinguishable from surrounding text:

```css
/* Links in body text */
.content a {
  color: var(--teal-600);
  text-decoration: underline;
  text-underline-offset: 2px;
}

/* If removing underline, ensure 3:1 contrast with surrounding text */
.nav-link {
  color: var(--teal-600); /* Must be 3:1 against body text colour */
}
```

#### Non-Text Contrast (UI Components)

UI components and graphical objects need 3:1 contrast:

```css
/* Form field borders */
input {
  border: 1px solid var(--surface-400); /* 3:1 against Surface 200 bg */
}

/* Icons */
.icon {
  color: var(--neutral-600); /* 3.5:1 against Surface 200 */
}

/* Disabled states - exempt from contrast requirements but should be visible */
button:disabled {
  background-color: var(--neutral-200);
  color: var(--neutral-500);
}
```

#### Colour Not Sole Indicator

Never use colour alone to convey information:

```css
/* ❌ Bad: Colour only */
.error {
  border-color: red;
}

/* ✅ Good: Colour + icon + text */
.error {
  border-color: var(--error-border);
}

.error-message {
  color: var(--error-text);
  display: flex;
  align-items: center;
  gap: 6px;
}

.error-message::before {
  content: '';
  /* Error icon */
}
```

#### Testing Tools

- **Browser DevTools:** Chrome/Firefox accessibility panel
- **Contrast checkers:** WebAIM Contrast Checker, Colour Contrast Analyser
- **Automated testing:** axe DevTools, WAVE

---

### 11.3 Screen Reader Patterns

#### Semantic HTML First

Use semantic HTML elements—they provide built-in accessibility:

```html
<!-- ✅ Good: Semantic elements -->
<header>...</header>
<nav>...</nav>
<main>...</main>
<article>...</article>
<aside>...</aside>
<footer>...</footer>

<!-- ❌ Bad: Divs with roles -->
<div role="banner">...</div>
<div role="navigation">...</div>
```

#### Landmark Regions

Every page should have these landmarks:

```html
<body>
  <header role="banner">
    <nav role="navigation" aria-label="Main">...</nav>
  </header>
  
  <main role="main" id="main-content">
    <!-- Page content -->
  </main>
  
  <aside role="complementary" aria-label="Sidebar">
    <!-- Secondary content -->
  </aside>
  
  <footer role="contentinfo">...</footer>
</body>
```

#### Skip Link

Allow keyboard users to bypass navigation:

```html
<body>
  <a href="#main-content" class="skip-link">Skip to main content</a>
  <header>...</header>
  <main id="main-content" tabindex="-1">...</main>
</body>
```

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 16px;
  padding: 8px 16px;
  background-color: var(--amber-500);
  color: var(--teal-900);
  font-weight: 600;
  z-index: 1001;
  border-radius: 4px;
}

.skip-link:focus {
  top: 16px;
}
```

#### Heading Hierarchy

Use proper heading levels—don't skip:

```html
<!-- ✅ Correct hierarchy -->
<h1>Page Title</h1>
  <h2>Section</h2>
    <h3>Subsection</h3>
    <h3>Subsection</h3>
  <h2>Section</h2>

<!-- ❌ Skipping levels -->
<h1>Page Title</h1>
  <h3>Section</h3>  <!-- Skipped h2! -->
```

#### ARIA Labels

Use ARIA when HTML semantics aren't sufficient:

```html
<!-- Labelling navigation regions -->
<nav aria-label="Main navigation">...</nav>
<nav aria-label="Footer links">...</nav>

<!-- Icon-only buttons -->
<button aria-label="Close modal">
  <svg><!-- X icon --></svg>
</button>

<!-- Search input -->
<input type="search" aria-label="Search products">

<!-- Describing current state -->
<button aria-expanded="false" aria-controls="menu">
  Menu
</button>
```

#### Live Regions

Announce dynamic content changes:

```html
<!-- Polite: Announced after current speech -->
<div aria-live="polite" aria-atomic="true">
  Item added to cart
</div>

<!-- Assertive: Interrupts current speech (use sparingly) -->
<div aria-live="assertive" role="alert">
  Payment failed. Please try again.
</div>

<!-- Status messages -->
<div role="status" aria-live="polite">
  Showing 24 of 127 products
</div>
```

```javascript
// Dynamically announce messages
function announce(message, priority = 'polite') {
  const region = document.getElementById('announcer');
  region.setAttribute('aria-live', priority);
  region.textContent = message;
  
  // Clear after announcement
  setTimeout(() => {
    region.textContent = '';
  }, 1000);
}

// Usage
announce('Product added to cart');
announce('Form submitted successfully');
announce('Error: Please check your email', 'assertive');
```

#### Form Accessibility

```html
<!-- Labels -->
<label for="email">Email address</label>
<input type="email" id="email" name="email">

<!-- Required fields -->
<label for="name">
  Name <span aria-hidden="true">*</span>
  <span class="sr-only">(required)</span>
</label>
<input type="text" id="name" required aria-required="true">

<!-- Error messages -->
<label for="password">Password</label>
<input 
  type="password" 
  id="password"
  aria-invalid="true"
  aria-describedby="password-error"
>
<span id="password-error" role="alert">
  Password must be at least 8 characters
</span>

<!-- Help text -->
<label for="username">Username</label>
<input 
  type="text" 
  id="username"
  aria-describedby="username-help"
>
<span id="username-help">
  Letters and numbers only, 3-20 characters
</span>

<!-- Fieldset for groups -->
<fieldset>
  <legend>Shipping method</legend>
  <input type="radio" id="standard" name="shipping" value="standard">
  <label for="standard">Standard (5-7 days)</label>
  <input type="radio" id="express" name="shipping" value="express">
  <label for="express">Express (2-3 days)</label>
</fieldset>
```

#### Hidden Content

```css
/* Visually hidden but available to screen readers */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* Focusable when tabbed to (skip links) */
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
  white-space: normal;
}
```

```html
<!-- Hidden from screen readers (decorative) -->
<span aria-hidden="true">★★★★☆</span>
<span class="sr-only">4 out of 5 stars</span>

<!-- Hidden from everyone -->
<div hidden>This content is not rendered</div>

<!-- Visible but not announced -->
<img src="decoration.svg" alt="" role="presentation">
```

#### Image Alt Text

```html
<!-- Informative images -->
<img src="foundation-cover.jpg" alt="Foundation by Isaac Asimov - Book cover showing a galaxy spiral">

<!-- Decorative images -->
<img src="flourish.svg" alt="" role="presentation">

<!-- Complex images -->
<figure>
  <img src="sales-chart.png" alt="Sales chart showing growth from £800 in January to £2,400 in December">
  <figcaption>2024 Monthly Sales Growth</figcaption>
</figure>

<!-- Linked images -->
<a href="/product/foundation">
  <img src="foundation-cover.jpg" alt="Foundation by Isaac Asimov">
</a>
```

#### Modal Accessibility

```html
<div 
  role="dialog" 
  aria-modal="true"
  aria-labelledby="modal-title"
  aria-describedby="modal-description"
>
  <h2 id="modal-title">Confirm Purchase</h2>
  <p id="modal-description">
    You are about to purchase 3 items for £19.99
  </p>
  <button>Cancel</button>
  <button>Confirm</button>
</div>
```

---

### 11.4 Keyboard Navigation

#### Focus Order

Focus order must follow visual reading order (left-to-right, top-to-bottom for LTR):

```html
<!-- ✅ Correct: DOM order matches visual order -->
<nav>
  <a href="/">Home</a>
  <a href="/browse">Browse</a>
  <a href="/about">About</a>
</nav>

<!-- ❌ Wrong: CSS reordering breaks focus order -->
<nav style="display: flex; flex-direction: row-reverse;">
  <a href="/">Home</a>      <!-- Visually last, focused first -->
  <a href="/browse">Browse</a>
  <a href="/about">About</a> <!-- Visually first, focused last -->
</nav>
```

#### Tabindex Usage

```html
<!-- tabindex="0": Add to tab order (for custom interactive elements) -->
<div role="button" tabindex="0">Custom button</div>

<!-- tabindex="-1": Programmatically focusable, not in tab order -->
<div id="modal" tabindex="-1">Modal receives focus via JS</div>
<main id="main-content" tabindex="-1">Skip link target</main>

<!-- ❌ Never use positive tabindex -->
<button tabindex="3">Don't do this</button>
```

#### Keyboard Interactions by Component

| Component | Keys | Action |
|-----------|------|--------|
| **Button** | Enter, Space | Activate |
| **Link** | Enter | Navigate |
| **Checkbox** | Space | Toggle |
| **Radio group** | ↑↓ or ←→ | Move selection |
| **Select/Dropdown** | ↑↓, Enter, Esc | Navigate, select, close |
| **Modal** | Esc | Close |
| **Tabs** | ←→, Home, End | Switch tabs |
| **Accordion** | Enter, Space | Expand/collapse |
| **Menu** | ↑↓, Enter, Esc | Navigate, select, close |
| **Carousel** | ←→ | Previous/next slide |

#### Implementing Keyboard Handlers

```javascript
// Button with Enter and Space
button.addEventListener('keydown', (e) => {
  if (e.key === 'Enter' || e.key === ' ') {
    e.preventDefault();
    button.click();
  }
});

// Dropdown menu
menu.addEventListener('keydown', (e) => {
  const items = menu.querySelectorAll('[role="menuitem"]');
  const currentIndex = Array.from(items).indexOf(document.activeElement);
  
  switch (e.key) {
    case 'ArrowDown':
      e.preventDefault();
      items[(currentIndex + 1) % items.length].focus();
      break;
    case 'ArrowUp':
      e.preventDefault();
      items[(currentIndex - 1 + items.length) % items.length].focus();
      break;
    case 'Home':
      e.preventDefault();
      items[0].focus();
      break;
    case 'End':
      e.preventDefault();
      items[items.length - 1].focus();
      break;
    case 'Escape':
      closeMenu();
      triggerButton.focus();
      break;
  }
});
```

#### Focus Trapping (Modals)

When modal is open, focus must stay within modal:

```javascript
function trapFocus(modal) {
  const focusableElements = modal.querySelectorAll(
    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
  const firstElement = focusableElements[0];
  const lastElement = focusableElements[focusableElements.length - 1];
  
  modal.addEventListener('keydown', (e) => {
    if (e.key !== 'Tab') return;
    
    if (e.shiftKey) {
      // Shift + Tab
      if (document.activeElement === firstElement) {
        e.preventDefault();
        lastElement.focus();
      }
    } else {
      // Tab
      if (document.activeElement === lastElement) {
        e.preventDefault();
        firstElement.focus();
      }
    }
  });
  
  // Focus first element on open
  firstElement.focus();
}

function openModal(modal) {
  modal.setAttribute('aria-hidden', 'false');
  modal.classList.add('is-open');
  document.body.classList.add('modal-open');
  trapFocus(modal);
}

function closeModal(modal, returnFocus) {
  modal.setAttribute('aria-hidden', 'true');
  modal.classList.remove('is-open');
  document.body.classList.remove('modal-open');
  returnFocus.focus(); // Return focus to trigger element
}
```

#### Roving Tabindex (Tab Panels, Toolbars)

For composite widgets, only one item is in tab order at a time:

```html
<div role="tablist">
  <button role="tab" tabindex="0" aria-selected="true">Tab 1</button>
  <button role="tab" tabindex="-1" aria-selected="false">Tab 2</button>
  <button role="tab" tabindex="-1" aria-selected="false">Tab 3</button>
</div>
```

```javascript
tabs.addEventListener('keydown', (e) => {
  const tabButtons = tabs.querySelectorAll('[role="tab"]');
  const currentIndex = Array.from(tabButtons).indexOf(document.activeElement);
  let newIndex;
  
  switch (e.key) {
    case 'ArrowRight':
      newIndex = (currentIndex + 1) % tabButtons.length;
      break;
    case 'ArrowLeft':
      newIndex = (currentIndex - 1 + tabButtons.length) % tabButtons.length;
      break;
    case 'Home':
      newIndex = 0;
      break;
    case 'End':
      newIndex = tabButtons.length - 1;
      break;
    default:
      return;
  }
  
  e.preventDefault();
  
  // Update tabindex
  tabButtons[currentIndex].setAttribute('tabindex', '-1');
  tabButtons[newIndex].setAttribute('tabindex', '0');
  tabButtons[newIndex].focus();
  
  // Activate tab
  activateTab(tabButtons[newIndex]);
});
```

#### Visible Focus During Navigation

Ensure focus is visible when scrolling into view:

```css
/* Ensure focused element isn't hidden behind sticky header */
:target {
  scroll-margin-top: 80px;
}

*:focus {
  scroll-margin-top: 80px;
  scroll-margin-bottom: 20px;
}
```

```javascript
// Scroll focused element into view if needed
element.focus({ preventScroll: false });

// Or manually scroll
element.focus();
element.scrollIntoView({ behavior: 'smooth', block: 'center' });
```

---

### 11.5 Accessibility Testing Checklist

#### Automated Testing

Run these tools on every page:

| Tool | What it catches |
|------|-----------------|
| **axe DevTools** | WCAG violations, missing labels, contrast issues |
| **WAVE** | Structure issues, missing alt text, form labels |
| **Lighthouse** | Performance + accessibility score |
| **Pa11y** | CLI tool for CI/CD integration |

#### Manual Testing

Automated tools catch ~30% of issues. Manual testing is essential:

**Keyboard Testing:**

- [ ] Can reach all interactive elements with Tab?
- [ ] Can activate buttons with Enter/Space?
- [ ] Can escape modals with Escape key?
- [ ] Is focus order logical?
- [ ] Is focus always visible?
- [ ] Can navigate forms without mouse?

**Screen Reader Testing:**

- [ ] Are all images described (or hidden if decorative)?
- [ ] Do form fields have labels?
- [ ] Are error messages announced?
- [ ] Are dynamic changes announced?
- [ ] Do headings create logical outline?
- [ ] Are landmarks present and labelled?

**Visual Testing:**

- [ ] Does content reflow at 400% zoom?
- [ ] Is text readable at 200% zoom?
- [ ] Do focus indicators have sufficient contrast?
- [ ] Is colour not the only indicator?

**Recommended Screen Readers:**

- **macOS:** VoiceOver (built-in, Cmd+F5)
- **Windows:** NVDA (free), JAWS
- **iOS:** VoiceOver (built-in)
- **Android:** TalkBack (built-in)

---

### 11.6 ARIA Reference

#### Commonly Used Roles

| Role | Use Case |
|------|----------|
| `role="button"` | Clickable non-button element |
| `role="link"` | Clickable non-anchor element |
| `role="dialog"` | Modal dialog |
| `role="alert"` | Important, time-sensitive message |
| `role="status"` | Status update (polite) |
| `role="tab"` / `role="tabpanel"` | Tab interface |
| `role="menu"` / `role="menuitem"` | Dropdown menu |
| `role="navigation"` | Navigation region |
| `role="search"` | Search region |
| `role="img"` | Image (with aria-label) |
| `role="presentation"` / `role="none"` | Decorative, remove semantics |

#### Commonly Used States & Properties

| Attribute | Use Case |
|-----------|----------|
| `aria-label` | Label when no visible text |
| `aria-labelledby` | Reference visible label element |
| `aria-describedby` | Reference description/help text |
| `aria-expanded` | Toggle expanded state |
| `aria-hidden` | Hide from assistive technology |
| `aria-live` | Announce dynamic changes |
| `aria-pressed` | Toggle button state |
| `aria-selected` | Selection state (tabs, listbox) |
| `aria-invalid` | Form validation error |
| `aria-required` | Required form field |
| `aria-disabled` | Disabled but focusable |
| `aria-controls` | References controlled element |
| `aria-current` | Current item (page, step, date) |

#### ARIA Patterns Reference

For complex widgets, follow WAI-ARIA Authoring Practices:
https://www.w3.org/WAI/ARIA/apg/patterns/



---

### ⚠️ MISSING: 12. Version History

---
