# Dutch Textbook — Component Catalog

Live showcase: `components.html`

---

## Left-Border Family

3 tiers by severity. All: `border-radius: 0 8px 8px 0`, no surrounding border.

| Component | Class | Left | Tint | See in |
|-----------|-------|------|------|--------|
| Tip | `.tip` | 2px accent | 4% | basics → Гласные (det) |
| Rule box | `.rule-box` | 3px accent | 5% | word_order → Главное |
| Trap | `.trap` | 3px #c53030 | 5% | word_order → Ловушки |

---

## Container 1: Table (`.dtable`)

HTML `<table>` with headers. Subtypes via cell classes.

| Subtype | Extra class | Cell classes | See in |
|---------|-------------|-------------|--------|
| Default | — | `.mc` (mono) | word_order → Союзы |
| Pronunciation | — | `.pron-letter`, `.pron-sound`, `.pron-examples`, `.pron-note` | basics → Произношение |
| Conjugation grid | `.conj-grid` | `.mc` on form cells | conjugation → Zijn |
| Verb pattern | `.vp-table` in `.vp-group` | `.vp-inf`, `.vp-form`, `.vp-ru` | verbs → Паттерны |

---

## Container 2: List Card (`.list-card`)

Div-based card with optional `.lc-head` header. 6 interchangeable row types inside.

| Row type | Class | Layout | See in |
|----------|-------|--------|--------|
| Default | `.lc-item` | `.lc-w` + `.lc-e` | word_order → Что в конец |
| Phrase | `.phrase` | `.phrase-nl` + `.phrase-note` (right) | phrasebook → all |
| Number | `.num-row` | `.num-val` (right-aligned) + `.num-nl` + `.num-note` (italic) | numerals → 0–12 |
| Prefix/suffix | `.prefix-row` | `.prefix-name` + `.prefix-meaning` + `.prefix-ex` | prefixes → Отделяемые |
| Conjunction | `.cr` in `.conj-group` | `.cr-nl` + `.cr-ru` + `.cr-ex` | word_order → Все союзы |
| Compound | `.compound-row` | `.compound-top`(word→meaning) + `.compound-parts` below | vocabulary → Сложные |

All rows: `padding: 5-7px 14px`, `border-bottom: 1px solid var(--border)`.

Special: `.gender` tag for suffix gender markers (`de`/`het`) — small gray badge.

---

## Container 3: Comparison (`.comparison`)

2-column CSS grid. Each cell: `.cmp` with optional `.cmp-label`.

| Subtype | Extra class | See in |
|---------|-------------|--------|
| Default (labeled) | — | word_order → Придаточное (Сравните) |
| Spelling pairs | `.pairs` | basics → Гласные (det) |

Pairs subtype: `.pair-word` (centered mono) + `.pair-label`.

---

## Standalone

| Component | Class | See in |
|-----------|-------|--------|
| Formula | `.formula` | word_order → Главное (V2) |
| Example | `.ex` + `.ex-nl` + `.ex-ru` + `.ex-note` | everywhere |
| Decision tree | `.tree` → `.tree-node` → `.tree-branches` → `.tree-b` | adjectives → Правило, hebben_zijn → Правило |

### Decision Tree structure
```
.tree
  .tree-node
    .tree-q          (question text)
    .tree-branches
      .tree-b.tree-b-no   (exit branch)
        .tree-b-label      (нет →)
        .tree-b-exit        (result)
      .tree-b.tree-b-yes  (continue branch)
        .tree-b-label      (да ↓)
    .tree-child            (nested, indented, left border)
      .tree-node           (recurse)
```
Labels: `text-align:right`, `min-width:42px`, `margin-right:6px` — arrows align.

---

## Structural

| Component | Class | Purpose |
|-----------|-------|---------|
| Summary card | `.summary` | Cheat sheet + TOC at top of guide |
| Section | `.section` + `.section-head` | Scroll target, TOC entry |
| Subsection | `.subsection` + `.ss-title` | Nested group within section |
| Group label | `.group-label` | Semantic tag (ПРАВИЛО, СПРАВОЧНИК...) |
| Expandable | `det()` helper → `.det-btn` + `.det-body` | Hides detail layer |

---

## Syntax Highlighting (inline spans)

| Class | Color | Effect |
|-------|-------|--------|
| `.v1` | #2d6a4f | green bg, main verb |
| `.v2` | #7b6b8a | purple bg + dotted underline, end verb |
| `.conj` | #b45309 | amber bg, conjunction |
| `.subj` | #4a6fa5 | blue, no bg, subject |
| `.hi` | accent | bold accent, general highlight |
| `.mc` | mono font | monospaced cell value |
| `.smono` | mono + accent + .7 opacity | keyword in summary |

---

## Unified Design Tokens

All notes: `font-size:11px; color:var(--dim); font-style:italic`
All row padding: `5-7px 14px` horizontal
Left-border radii: `0 8px 8px 0`
Card radii: `10px` (content), `16px` (summary, index cards)
