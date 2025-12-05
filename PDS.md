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

---

Ready for the next section.
---

### ⚠️ MISSING: 6. Interactive States
**⚠️ MISSING: 6.1 Hover States**
**⚠️ MISSING: 6.2 Focus States**
**⚠️ MISSING: 6.3 Active States**
**⚠️ MISSING: 6.4 Disabled States**
**⚠️ MISSING: 6.5 Error & Success States**

---

### ⚠️ MISSING: 7. Motion & Animation
**⚠️ MISSING: 7.1 Timing & Easing**
**⚠️ MISSING: 7.2 Transition Patterns**
**⚠️ MISSING: 7.3 Loading Animations**

# 8. Pages

### Public
`/` `/about` `/contact` `/blog` `/blog/[slug]` `/help` `/faq` `/newsletter` `/start-here` `/press` `/status` `/how-it-works`

### Content Discovery
`/authors` `/author/[slug]` `/eras` `/eras/[slug]` `/themes` `/themes/[slug]` `/category/[slug]` `/tag/[slug]` `/collections` `/new-arrivals` `/popular`

### Free Content
`/free` `/free/ebooks` `/free/audiobooks` `/radio-dramas` `/radio-dramas/[show-slug]` `/radio-dramas/[show-slug]/[episode-slug]`

### Reading Guides & Lists
`/reading-guides` `/reading-guides/[slug]` `/reading-lists` `/reading-lists/[slug]`

### Commerce
`/browse` `/browse/[genre]` `/product/[slug]` `/search` `/cart` `/checkout` `/checkout/confirmation` `/gift-cards` `/formats`

### Membership
`/membership` `/membership/compare` `/membership/gift`

### Account
`/account` `/account/library` `/account/wishlist` `/account/reading-history` `/account/lists` `/account/lists/[id]` `/account/orders` `/account/orders/[id]` `/account/downloads` `/account/credits` `/account/membership` `/account/settings`

### Auth
`/login` `/register` `/forgot-password`

### Legal
`/privacy` `/terms` `/refunds` `/accessibility` `/cookies` `/copyright` `/licensing`

### Error
`/404` `/500`

---

# 9. Pages (Detail)

### 3.1 Public

#### 3.1.1 Homepage `/`

#### 3.1.2 About `/about`

#### 3.1.3 Contact `/contact`

#### 3.1.4 Blog Index `/blog`

#### 3.1.5 Blog Post `/blog/[slug]`

#### 3.1.6 Help Centre `/help`

#### 3.1.7 FAQ `/faq`

#### 3.1.8 Newsletter `/newsletter`

#### 3.1.9 Start Here `/start-here`

#### 3.1.10 Press `/press`

#### 3.1.11 Status `/status`

#### 3.1.12 How It Works `/how-it-works`

### 3.2 Content Discovery

#### 3.2.1 Author Directory `/authors`

#### 3.2.2 Author Profile `/author/[slug]`

#### 3.2.3 Eras Index `/eras`

#### 3.2.4 Era Page `/eras/[slug]`

#### 3.2.5 Themes Index `/themes`

#### 3.2.6 Theme Page `/themes/[slug]`

#### 3.2.7 Category Archive `/category/[slug]`

#### 3.2.8 Tag Archive `/tag/[slug]`

#### 3.2.9 Collections `/collections`

#### 3.2.10 New Arrivals `/new-arrivals`

#### 3.2.11 Popular `/popular`

### 3.3 Free Content

#### 3.3.1 Free Content Hub `/free`

#### 3.3.2 Free Ebooks `/free/ebooks`

#### 3.3.3 Free Audiobooks `/free/audiobooks`

#### 3.3.4 Radio Dramas Index `/radio-dramas`

#### 3.3.5 Radio Show `/radio-dramas/[show-slug]`

#### 3.3.6 Radio Episode `/radio-dramas/[show-slug]/[episode-slug]`

### 3.4 Reading Guides & Lists

#### 3.4.1 Reading Guides Index `/reading-guides`

#### 3.4.2 Reading Guide `/reading-guides/[slug]`

#### 3.4.3 Reading Lists Index `/reading-lists`

#### 3.4.4 Reading List `/reading-lists/[slug]`

### 3.5 Commerce

#### 3.5.1 Browse `/browse`

#### 3.5.2 Browse by Genre `/browse/[genre]`

#### 3.5.3 Product Page `/product/[slug]`

#### 3.5.4 Search Results `/search`

#### 3.5.5 Cart `/cart`

#### 3.5.6 Checkout `/checkout`

#### 3.5.7 Order Confirmation `/checkout/confirmation`

#### 3.5.8 Gift Cards `/gift-cards`

#### 3.5.9 File Formats Guide `/formats`

### 3.6 Membership

#### 3.6.1 Membership `/membership`

#### 3.6.2 Compare Memberships `/membership/compare`

#### 3.6.3 Gift Membership `/membership/gift`

### 3.7 Account

#### 3.7.1 Account Dashboard `/account`

#### 3.7.2 My Library `/account/library`

#### 3.7.3 Wishlist `/account/wishlist`

#### 3.7.4 Reading History `/account/reading-history`

#### 3.7.5 My Lists `/account/lists`

#### 3.7.6 User List `/account/lists/[id]`

#### 3.7.7 Order History `/account/orders`

#### 3.7.8 Order Detail `/account/orders/[id]`

#### 3.7.9 Downloads `/account/downloads`

#### 3.7.10 Audiobook Credits `/account/credits`

#### 3.7.11 Membership Management `/account/membership`

#### 3.7.12 Settings `/account/settings`

### 3.8 Auth

#### 3.8.1 Login `/login`

#### 3.8.2 Register `/register`

#### 3.8.3 Forgot Password `/forgot-password`

### 3.9 Legal

#### 3.9.1 Privacy Policy `/privacy`

#### 3.9.2 Terms of Service `/terms`

#### 3.9.3 Refund Policy `/refunds`

#### 3.9.4 Accessibility `/accessibility`

#### 3.9.5 Cookie Policy `/cookies`

#### 3.9.6 Copyright & DMCA `/copyright`

#### 3.9.7 Licensing `/licensing`

### 3.10 Error

#### 3.10.1 Not Found `/404`

#### 3.10.2 Server Error `/500`

---

---

### 8. Pages *(currently numbered as Section 2)*
*(Page list — exists)*

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

---

### ⚠️ MISSING: 11. Accessibility
**⚠️ MISSING: 11.1 Focus Indicators**
**⚠️ MISSING: 11.2 Colour Contrast Requirements**
**⚠️ MISSING: 11.3 Screen Reader Patterns**
**⚠️ MISSING: 11.4 Keyboard Navigation**

---

### ⚠️ MISSING: 12. Version History

---
