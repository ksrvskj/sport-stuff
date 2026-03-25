# Personal Tools — Design System

Reference document for all visual and UX decisions.
Keep in repo root. Update when decisions change.

---

## Typography

**Primary:** Manrope (Google Fonts)
- Weights used: 300 (light, descriptions), 400 (body), 500 (labels, names), 600 (titles, emphasis)
- Never use 700 — too heavy for this aesthetic
- Discrete weights: `wght@300;400;500;600`

**Monospace:** JetBrains Mono
- Weights: 400, 500, 600
- Used for: ingredient amounts, KBJU numbers, timers, coffee doses, portion stepper value
- Never for body text

**Sizing scale:**
- Page title (h1): 24px / weight 600
- Section label (uppercase): 11px / weight 400 / letter-spacing 2.5px
- Card name: 14px / weight 500
- Card description: 11px / weight 300
- Body text (cook steps): 15px / weight 400
- Small meta: 10-11px / weight 400
- Mono numbers: 12-16px depending on context

---

## Color Palette

### Base
| Token        | Hex       | Usage                        |
|-------------|-----------|------------------------------|
| `--bg`      | `#0f0f12` | Page background              |
| `--surface` | `#17171c` | Card/panel backgrounds       |
| `--text`    | `#e2dbd0` | Primary text (warm white)    |
| `--dim`     | `#6b6560` | Secondary text, descriptions |

### 3 Accent Families
| Token       | Hex       | Domain                       |
|------------|-----------|------------------------------|
| `--warm`   | `#c9a87e` | Food, recipes, default accent|
| `--cool`   | `#7fa693` | Body, health, workout        |
| `--neutral`| `#9b928a` | Coffee, utilities            |

Each page sets `--accent` in inline `<style>`:
- Recipes: `--accent: var(--warm)` (`#c9a87e`)
- Workout: `--accent: var(--cool)` (`#7fa693`)
- Coffee: `--accent: var(--neutral)` (`#9b928a`)

### Recipe Category Colors (derived from accents)
| Category | Token       | Hex       | Character                |
|----------|------------|-----------|--------------------------|
| Soup     | `--soup`   | `#c9a87e` | Warm gold                |
| Curry    | `--curry`  | `#7fa693` | Sage green               |
| Pasta    | `--pasta`  | `#b49ac4` | Soft lavender            |
| Skillet  | `--skillet`| `#7faab4` | Muted teal               |
| Comfort  | `--comfort`| `#c4917e` | Dusty coral              |

### Dietary Tags
| Tag      | Color       | Matches            |
|----------|------------|---------------------|
| Vegan    | `--vegan`  | `#7fa693` (= cool)  |
| GF       | `--gf`     | `#c9a87e` (= warm)  |
| Fast     | `--fast`   | `#7faab4` (= teal)  |
| Protein  | `--hprot`  | `#c4917e` (= coral) |

### Color Usage Rules
- Category colors appear in: card border (14% opacity), card icon bg (8%), filter buttons, inline highlights in cook steps
- Text is always `--text` or `--dim`, never category-colored (except tiny tags and mono numbers)
- Borders: `color-mix(in srgb, var(--c) 14%, transparent)` — subtle, visible on OLED
- Backgrounds: `color-mix(in srgb, var(--c) 5-8%, transparent)` — tint, not color

---

## Spacing & Layout

### Border Radius
| Element          | Radius         |
|-----------------|----------------|
| Cards, panels   | `16px` (--radius) |
| Small elements  | `10px` (--radius-sm) |
| Buttons, pills  | `6-8px`        |
| Icons (hub)     | `9-13px` proportional to size |
| Step numbers    | `50%` (circle) |

### Spacing Principles
- **Tight between related elements.** Cards in a group, icon next to its label, filters in a row — keep close. They belong together.
- **Generous around groups.** Page margins, header-to-content gap, section separators — air here.
- **Don't add air between things that belong together.** If items are part of the same unit (card group, filter bar), reducing gap makes them feel more cohesive, not cramped.
- **Every spacing decision needs a reason.** "It looks better with more space" is not a reason. "These are a group and should read as one block" is.

### Specific Values
| Context                    | Value   |
|---------------------------|---------|
| Page padding (sides)      | 16-20px |
| Card padding              | 14-16px |
| Card margin-bottom        | 8px     |
| Hub grid gap              | 8px     |
| Icon-to-text gap (cards)  | 10px    |
| Filter button gap         | 6px     |
| Section spacing (header->content) | 12px |

---

## Icons

### Hub — SVG Line Icons
3 custom SVGs, one per tool. Consistent stroke width 1.6, round caps/joins, no fill.

| Tool    | Icon description     | Accent   |
|---------|---------------------|----------|
| Workout | Stick figure        | `--cool` |
| Recipes | Pot with steam      | `--warm` |
| Coffee  | Cup with handle     | `--neutral` |

### Recipe Categories — 5 SVG Icons
One icon per category (not per recipe). New recipe inherits category icon.

| Category | Icon              |
|----------|-------------------|
| Soup     | Pot + steam lines |
| Curry    | Dome bowl         |
| Pasta    | Barrel/vessel     |
| Skillet  | Pan + steam       |
| Comfort  | Star              |

All: `viewBox="0 0 24 24"`, stroke only, same weight as hub icons.

All icons are centralized in `icons.js` — accessed via `ICONS.cat.soup`, `ICONS.coffee.chemex`, `ICONS.tier.moon`, etc.
Use `iconInner(svg)` helper to extract inner SVG content when wrapper `<svg>` already exists.

### Icon Sizing
| Context         | Container | SVG size |
|----------------|-----------|----------|
| Hub hero card  | 44x44px   | 22x22px  |
| Hub small card | 34x34px   | 17x17px  |
| Recipe card    | 34x34px   | 18x18px  |
| Cook mode hero | 42x42px   | 22x22px  |

### No Emoji
Emoji are device-dependent and visually inconsistent with line-icon aesthetic. Exception: dietary tags in filter pills — these are functional labels, not decorative.

---

## Texture & Atmosphere

### Noise Overlay
SVG fractalNoise filter, 2.5% opacity, 128px tile. Applied via `body::before`, `position:fixed`, `pointer-events:none`. Adds tactile quality, removes digital flatness.

### Ambient Glow (hub only)
Two blurred circles (280px, blur 100px, opacity 5%):
- Warm (#c9a87e) top-right
- Cool (#7fa693) bottom-left

Decorative, not functional. Only on hub page where there's enough empty space.

### Header Gradient
Each page: `linear-gradient(180deg, color-mix(in srgb, var(--accent) 6%, transparent), transparent)`. Barely visible warm wash at top.

---

## Animation

### Entrance (hub only)
`fadeUp`: opacity 0->1, translateY 6px->0, duration 0.4s ease.
Stagger: 50ms between elements (header -> card 1 -> card 2 -> card 3 -> footer).

Never apply `animation: fadeUp ... both` to dynamically rendered content — the `both` fill-mode keeps elements at `opacity:0` if the animation can't replay (e.g. after innerHTML rebuild). Entrance animation is for static hub elements only.

### Interactions
- Card tap: `transform: scale(0.97)` on `:active` — instant, no transition delay
- Buttons: `transform: scale(0.97)` on `:active`
- Filter buttons: color/border transition 0.15s
- No hover effects (mobile-first, hover doesn't exist on touch)

### Accessibility
`@media (prefers-reduced-motion: reduce)` -> disable all animations.

---

## Nutrition Display (ED-Sensitivity)

### Principle
Nutrition info is available but not prominent. It's reference data for the cook, not a selling point.

### Browse Mode
- Only **protein** shown, as a small pill: `P 12g`
- No calories, fat, carbs on cards
- Protein is athletic context (training recovery), not restriction framing

### Cook Mode
- Full KBJU at the **bottom**, after steps and tips
- Small, grey, mono font, opacity 0.25: `280 kcal . P 10g . F 6g . C 45g / per serving`
- Not before the recipe, not colorful, not prominent

### Nutrition Toggle
- Button fixed bottom-right, 32px circle
- Hides ALL nutrition (protein pills in browse + KBJU in cook)
- State saved in `localStorage('hideNutrition')`
- `?clean=1` URL param -> hides nutrition (for sharing to ED-sensitive friends)

### Language Rules
Never use:
- "low calorie" / "guilt-free" / "clean eating" / "cheat meal"
- Calorie count as a selling point or subtitle

OK to use:
- "Light & filling" (describes texture, not restriction)
- "Protein" (athletic framing)
- "Quick classic" (neutral)

---

## Shared Components

### Header
`.header` with `.header-top` (flex: content left, lang toggle right).
Contains: `.header-sub` (uppercase label), `h1` (gradient text), `.header-desc`, `.header-links`.

### Language Toggle
`.lang-toggle` with `.lang-btn` buttons. Active state via `.lang-btn.active`.
Appears in header and (for recipes) in cook mode bar.

### Cards
`.card` with `--c` CSS variable for per-item color theming.
Contains: `.card-top` (flex: icon + body), `.card-body` (name + sub + meta row).
Expandable via toggling content after `.card-top`.

### Stepper
`.stepper` — `[-][value][+]` control for portions.
Value input: JetBrains Mono, colored with `--c`.

### Timer Ring
`.timer-wrap` > `.timer-ring` > `.timer-inner` + `.timer-hint`.
Conic-gradient fill shows progress. Shared between recipes (countdown) and coffee (count-up).
Default size: 44x44 ring / 36x36 inner. Coffee brew variant: 64x64 / 52x52.

### Check Button
`.check-btn` / `.check-btn.checked` — 28px circle, turns `--vegan` green when checked.

### View Switching
`#browseView` / `#cookView` toggled via `body.cooking` class.
CSS: `body.cooking #browseView{display:none} body.cooking #cookView{display:block}`.

---

## Deep Links & URL Params

### Pattern
Read on load -> set state -> render. Write on state change via `history.replaceState` (not pushState — don't pollute back button).

### Recipes
| Param   | Values          | Effect                    |
|---------|-----------------|---------------------------|
| `r`     | recipe id       | Opens cook mode           |
| `lang`  | `ru` / `en`     | Sets language             |
| `clean` | `1`             | Hides nutrition           |

Example: `recipes.html?r=rosti-egg&lang=en`

### Coffee
| Param | Values      | Effect              |
|-------|-------------|----------------------|
| `m`   | method id   | Opens that method    |
| `lang`| `ru` / `en` | Sets language        |

Example: `coffee.html?m=chemex&lang=en`

### Workout
| Param | Values               | Effect         |
|-------|----------------------|----------------|
| `t`   | `min`/`regular`/`full`| Sets tier      |

### Language
URL param `?lang=` overrides `localStorage`. Priority: URL > localStorage > default `'ru'`. Shared across all pages via same localStorage key `'lang'`.

---

## i18n

All user-visible strings are `{ru:"...", en:"..."}` objects, resolved via `t(obj)` helper. This includes: recipe names, subtitles, ingredient names, units, step text, tips, UI labels, filter labels.

Fixed strings (never translated): method names (Chemex, V60), technical terms.

---

## Ingredient Rounding

When scaling portions, amounts are rounded context-aware:

| Type                | Rule                    | Example                  |
|--------------------|-------------------------|--------------------------|
| Countable (onion, egg) | Nearest 0.5          | 1.33 -> 1.5, 1.8 -> 2   |
| Small measures (tsp, tbsp) | Nearest 0.5      | 0.75 tsp -> 1 tsp       |
| Grams/ml >= 50     | Nearest 5              | 137g -> 135g             |
| Grams/ml 10-49     | Nearest integer        | 13.5g -> 14g             |
| Grams/ml < 10      | 1 decimal              | 1.33g -> 1.3g            |

---

## File Structure

```
personal-tools/
  DESIGN.md        <- this file
  style.css        <- design system + all page CSS (shared)
  icons.js         <- all SVG icons (ICONS.hub/cat/coffee/tier/tag/ui + iconInner helper)
  index.html       <- hub dashboard (links style.css + hub-specific inline)
  workout.html     <- morning routine
  recipes.html     <- batch cooking (browse + cook mode)
  coffee.html      <- brew guides (calculators)
```

Each page: `<link rel="stylesheet" href="style.css">` + inline `<style>` only for `:root` variable overrides.
Each page (except hub): `<script src="icons.js"></script>` before the main `<script>` block.

Hub is the exception: it links style.css for shared base (body, noise, fonts) but keeps bento grid / hero card styles inline (hub-specific layout).

---

## Architecture Decisions

| Decision | Choice | Why | Reconsider when |
|----------|--------|-----|-----------------|
| Framework | Vanilla JS | 15 recipes, 1 developer, static hosting, <100ms load | Persistent features (favorites, shopping list, meal plans) |
| Hosting | GitHub Pages | Free, zero config, custom domain possible | Need server-side logic |
| CSS | Shared file + inline `:root` overrides | One source of truth for design system | File count grows past 6-7 |
| Rendering | `innerHTML` rebuild, data-driven | Simple, no virtual DOM overhead | Lists exceed ~100 items or need partial updates |
| i18n | JS objects in each file | Simple, no build step | 3+ languages or external translators |
| Icons | Inline SVG | No HTTP requests, style with CSS | Need 20+ icons -> consider sprite |
| State | JS variables + localStorage | No serialization overhead | Cross-page state or offline sync |

---

## Coding Conventions

### Page Structure
```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="theme-color" content="#0f0f12">
  <title>...</title>
  <link rel="stylesheet" href="style.css">
  <style>:root{--accent:#...}</style>
</head>
<body>
  <!-- HTML structure -->
  <script>
    // All JS inline, single script block
    // Data → State → Functions → Init
  </script>
</body>
</html>
```

### JS Patterns
- **Data arrays** (`R`, `M`, exercises) at the top — plain objects, no classes
- **State variables** after data — `let curCat`, `let openMethod`, `let cookId`
- **`t(obj)`** resolves `{ru, en}` to current language string
- **`render()`** / **`fullRender()`** rebuilds DOM from state via innerHTML
- **Targeted DOM updates** for timers (`updateTmRing`, `updateBrewRing`) — don't re-render entire page every second
- **`readURL()`** at init — parse URL params, set state
- **`updateURL()`** on state change — `history.replaceState`, not pushState
- **`event.stopPropagation()`** on nested clickable elements inside cards

### CSS Patterns
- **`--c` variable** on each card/item for per-item color theming
- **`color-mix(in srgb, var(--c) N%, transparent)`** for dynamic opacity tinting
- **`var(--br, var(--accent))`** fallback pattern for page-specific overrides
- **No `!important`** — specificity is managed via selector order
- **No `animation: ... both` on dynamic content** — `both` fill-mode keeps opacity:0 after innerHTML rebuild

### Gotchas
- `pointer-events: none` on noise overlay and decorative elements
- `event.stopPropagation()` required for buttons inside clickable cards
- Timer intervals survive `render()` calls — they reference state variables, re-query DOM by ID
- `localStorage` keys: `'lang'`, `'hideNutrition'` — shared across pages
