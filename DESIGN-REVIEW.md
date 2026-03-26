# Dutch Textbook — Design Review

## Part 1: Universal Review (product-level)

### INDEX PAGE

**Header "Naslagwerk"** — confusing now. Naslagwerk is a block name (Справочник). The page header should be something else or removed. The title "Nederlands" is enough.

**Block icons: emoji** — violates hub rule "No Emoji. Emoji are device-dependent and visually inconsistent with line-icon aesthetic." Need 5 SVG stroke icons matching hub style (stroke-width 1.6, round caps, no fill).

**Index cards** — clean, but `--surface-read` (rgba 45% opacity) might be too subtle on warm paper. Cards almost invisible. Compare with hub's solid `--surface` cards. Consider: either solid `--surface` or slightly higher opacity.

**Block labels** — small colored dot + emoji + name. After SVG fix: dot + icon + name. The dot may be redundant if icon is colored. Consider: icon replaces dot.

**Arrow `›`** on cards — text character, not SVG. Inconsistent with icon approach. Replace with chevron SVG or remove (the whole card is tappable).

**Animation** — `fadeIn .3s` on cards, sections, summary. Hub uses `fadeUp .4s` with staggered delays. Current: no stagger, slightly faster. Consider stagger for index cards.

---

### GUIDE VIEW — TOPBAR

**"Назад"** — Russian word in a Dutch textbook. Hub uses "← Hub" (English). Options:
- `← Hub` (match hub pattern)
- `← [block name]` like "← Глагол" (shows where you're going)
- Just chevron `‹` with no text (cleaner)

**Topbar density** — currently: back-btn + block label + guide title + lang toggle. That's 4 elements on a narrow phone. The block label (uppercase, accent) + guide title (bold) might be too much. Consider dropping the topbar block label — it's already in the guide header below.

**Lang toggle** — appears on both index and guide topbars. On index it's rarely needed (you choose once). Consider: only on guide view, or in a settings area.

---

### GUIDE VIEW — HEADER

**Guide header** has: block label + emoji, title, subtitle (NL), level badge.

After opening a guide from index: you see the topbar (with block+title), then the header (with block+title again). **Redundancy**: block label appears twice, title appears twice. The topbar version appears on scroll (sticky), the header version is the "hero". This is intentional (recipes does this too — header title then cook-bar title), but worth noting.

**Level badge** — small accent pill. Currently only shows on guide header, not on topbar. This is correct — it's metadata, not navigation.

---

### GUIDE VIEW — CONTENT

**Summary card** — white `--surface` background, shadow, accent border. This is the only component with a shadow. Everything else is flat with border. The shadow creates visual hierarchy (summary = most important), but it's the only elevated element. Consistent or lonely?

**Section titles** — 16px/600 with bottom border. Clean. But the border runs full width of the content area. Consider: should it match hub's approach (no borders on titles)?

**Group labels** — 9px uppercase, opacity .35. Very subtle. This is intentional — they shouldn't compete with section titles. But on first visit, a user might not notice them at all. Worth testing if they're readable.

**det-btn** — the only interactive element besides navigation. Currently: accent-tinted pill with `›` arrow. On tap, arrow rotates 90°. The arrow rotation is the only visual feedback for expand state. Consider: also changing button text/color when open.

**Scroll-to-top button** — white circle with arrow, bottom-right. Appears at scrollY > 400. Simple and functional. Matches hub's minimal approach.

---

### TYPOGRAPHY

**Body text**: 15px/1.65. Hub uses 15px for cook steps. ✓ Match.
**Section title**: 16px/600. Hub h1 is 24px. Our guide-title is 24px. ✓ But section titles are smaller — this is correct hierarchy.
**Card name**: 14px/500. Hub card name: 14px/500. ✓ Exact match.
**Card desc**: 11px/300. Hub card desc: 11px/300. ✓ Exact match.
**Uppercase labels**: Our section label 11px, hub section label 11px. ✓ But letter-spacing varies (1.5px vs 2.5px). Need to pick one.
**Mono numbers**: 12px in tables. Hub uses 12-16px. ✓ Within range.

Weight 700 is never used — matches hub rule "Never use 700."

---

### COMPONENTS — QUICK VISUAL SCAN

**Tables** — consistent styling. Headers in `--surface-alt`, good contrast. But `.vp-table` has tighter padding (5px 10px) than `.dtable` (7px 12px). Should unify.

**Left-border family** — tip/rule-box/trap. Clear visual hierarchy through thickness and color. The 8px right radius looks good. But `.trap` has `margin-bottom:8px` while `.rule-box` has `margin-bottom:10px`. Unify to 10px.

**Examples** — `.ex` cards with border. They look good but there are a LOT of them. In a section with 5+ examples, the visual rhythm becomes monotonous. Consider: should examples inside `det-body` have a simpler look (no border, just lines)?

**Decision tree** — tested in adjectives and hebben_zijn. The left border line connecting levels works. Arrow alignment (text-align:right) was fixed. Visually clean.

**Phrase notes** — `.phrase-note` was missing `font-style:italic` until recently. Now has it. But `.phrase-note` max-width 45% might clip on narrow phones. Test at 320px.

---

## Part 2: Hub Alignment Checklist

| Token/Pattern | Hub (DESIGN.md) | Dutch Textbook | Match? | Action |
|---|---|---|---|---|
| Fonts | Manrope 300-600 + JetBrains Mono | Same | ✓ | — |
| Weight 700 | Never | Never used | ✓ | — |
| `--radius` | 16px | 16px | ✓ | — |
| `--radius-sm` | 10px | 10px | ✓ | — |
| Button radius | 6-8px | 6px | ✓ | — |
| Page padding | 16-20px | 16px | ✓ | — |
| Card padding | 14-16px | 14-16px | ✓ | — |
| Card gap | 8px | 8px margin-bottom | ✓ | — |
| Border pattern | `color-mix(var(--c) 14%)` | Same | ✓ | — |
| BG tint pattern | `color-mix(var(--c) 5-8%)` | Same | ✓ | — |
| Icons | SVG stroke, width 1.6, round | **Emoji** | ✗ | Replace with SVG |
| No emoji rule | Strict | Violated | ✗ | Fix |
| Header gradient | `accent 6%, transparent` | `accent 5%, transparent` | ~✓ | Align to 6% |
| Noise overlay | 2.5% fractalNoise | None | — | Intentional (clean reading) |
| Ambient glow | On hub only | None | ✓ | Correct |
| Card shadow | None (border only) | Summary has shadow | ? | Decide: keep or remove |
| Navigation back | `← Hub` text link | `← Назад` text + svg | ✗ | Review |
| Animation | fadeUp .4s staggered | fadeIn .3s no stagger | ~✗ | Align timing + add stagger |
| `letter-spacing` labels | 2.5px | Mixed (1.5-3px) | ~✗ | Pick one value |
| v2 underline | Designed with dotted underline | Missing in CSS | ✗ | Add back |

---

## Part 3: Priority Fixes

### P0 — Rule violations
1. **Emoji → SVG**: 5 block icons needed (basis, woorden, werkwoord, zinsbouw, naslagwerk)
2. **v2 dotted underline**: was designed, disappeared from CSS. Add back.

### P1 — Visual consistency
3. **Topbar "Назад"**: decide pattern (← Hub / ← block name / chevron only)
4. **Index header "Naslagwerk"**: remove or rename (conflicts with block name)
5. **letter-spacing**: unify to 2px everywhere
6. **Card arrow `›`**: replace with SVG or remove
7. **Header gradient**: 5% → 6% (match hub)

### P2 — Polish
8. **Index card opacity**: test `--surface-read` vs solid `--surface`
9. **Animation**: match hub timing (.4s) + stagger index cards
10. **vp-table padding**: 5px 10px → 7px 12px (match dtable)
11. **trap margin**: 8px → 10px (match rule-box)
12. **Summary shadow**: decide keep/remove (only elevated element)
13. **Topbar simplify**: consider dropping block label from guide topbar
14. **Block dot**: may be redundant after SVG icons
