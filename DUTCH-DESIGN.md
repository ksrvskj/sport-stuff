# Dutch Textbook — Design System v3

---

## Architecture

### Files
| File | Lines | Content |
|------|-------|---------|
| `dutch.html` | ~350 | Shell: CSS + HTML templates + rendering logic |
| `dutch-data.js` | ~1260 | Data: GROUPS, BLOCKS, GUIDES, helpers |
| `dutch-preview.html` | ~1610 | Combined (for preview / offline) |
| `components.html` | ~420 | Component showcase |

### Views
Two views in one page via `body.reading` class toggle:
- **Index** — springboard with block cards
- **Guide** — topbar + header + summary + sections

Deep links: `dutch.html?g=word_order&lang=en`

### Scalability
| Action | What to change | Breaks? |
|--------|---------------|---------|
| Add section to guide | Push to `sections[]` in data.js | No |
| Add new guide | Add to `GUIDES` + `BLOCKS` in data.js | No |
| Add new block | Add to `BLOCKS` + CSS color variable | No |
| Split oversized guide | Two GUIDES entries, move sections | No |
| Phrasebook grows | Add sections | No |
| Need B2+ content | New block "Gevorderd" | No |

---

## 5-Block Navigation

| Block | ID | Color | Guides | Rationale |
|-------|-----|-------|--------|-----------|
| Основы | `basis` | `--blue` | basics | First day: sounds, articles, negation |
| Слова | `woorden` | `--purple` | adjectives, pronouns, prepositions | How words work |
| Глагол | `werkwoord` | `--green` | conjugation, verbs, tenses, modal, hebben_zijn | Complete verb system |
| Предложение | `zinsbouw` | `--orange` | word_order, prefixes, passive | Sentence construction |
| Справочник | `naslagwerk` | `--teal` | numerals, vocabulary, phrasebook | Look-up, not linear |

Distribution: 1 — 3 — 5 — 3 — 3

---

## Section Groups (semantic tags, not order)

| Group | RU | EN | Learner asks |
|-------|----|----|-------------|
| `overview` | Сводка | Overview | What is this? |
| `rule` | Правило | Rule | What's the principle? |
| `formation` | Как устроено | Formation | How is it formed? |
| `types` | Разновидности | Types | What kinds? |
| `watchout` | Осторожно | Watch Out | Where will I err? |
| `reference` | Справочник | Reference | Give me everything |

Order per guide is **pedagogical**. Groups can repeat with gaps.

---

## 14 Guides — Compact Map

**basics**: pronunciation(ref) → vowels(rule) → articles(rule) → plural(form) → diminutives(form) → negation(rule)
**adjectives**: rule+tree(rule) → table(form) → comparison(form) → adverbs(types) → irregular(watch)
**pronouns**: overview(over) → reflexive(types) → demonstrative(types) → relative(types) → er(ref)
**prepositions**: place(types) → time(types) → direction(types) → with_verbs(ref)
**conjugation**: zijn(ref) → hebben(ref) → worden(ref) → zullen(ref)
**verbs**: kofschip(rule) → participle(rule) → patterns(types) → groups(types) → important(ref)
**tenses**: overview(over) → presens(form) → perfectum(form) → imperfectum(form) → perf_vs_imperf(watch) → other(form) → conditionals(watch) → infinitive(ref)
**modal**: overview(over) → kunnen(types) → moeten(types) → mogen(types) → willen(types) → hoeven(watch) → ipp(watch)
**hebben_zijn**: rule+tree(rule) → zijn_verbs(types) → both(watch)
**word_order**: main(rule) → questions(rule) → tmp(rule) → subordinate(rule) → conjunctions(types) → traps(watch) → all_conj(ref)
**prefixes**: overview(over) → separable(types) → inseparable(types) → ge_participle(form) → both(watch)
**passive**: worden_vs_zijn(rule) → by_tense(form) → impersonal(watch)
**numerals**: cardinals(form) → ordinals(form) → time_dates(types) → half_drie(watch) → full_list(ref)
**vocabulary**: compounds(rule) → suffixes(form) → borrowings(types) → idioms(ref)
**phrasebook**: greetings(types) → language(types) → smalltalk(types) → shopping(types) → directions(types)

---

## Color System

### Light Theme Base
| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#faf7f2` | Page background (warm paper) |
| `--surface` | `#ffffff` | Summary card |
| `--surface-read` | `rgba(255,255,255,.45)` | In-guide cards |
| `--surface-alt` | `#f5f1eb` | Table/list headers |
| `--text` | `#1c1917` | Primary text |
| `--dim` | `#9c9590` | Translations, notes |

### Block Colors
| Block | Token | Hex |
|-------|-------|-----|
| Basis | `--blue` | `#4a6fa5` |
| Woorden | `--purple` | `#7b6b8a` |
| Werkwoord | `--green` | `#5a8a6e` |
| Zinsbouw | `--orange` | `#c4856c` |
| Naslagwerk | `--teal` | `#5a8a8a` |

### Syntax
`.v1` green #2d6a4f · `.v2` purple #7b6b8a (dotted underline) · `.conj` amber #b45309 · `.subj` blue #4a6fa5 · `.hi` accent

---

## Hub Alignment

### Shared
Manrope + JetBrains Mono · 16px radii · 10px content radii · 6px buttons · 16px side padding · stroke-only icon style

### Intentionally different
Light theme (textbook = paper) · No noise overlay · No ambient glow · 5 block colors instead of 3 accents

### TODO: Design Review
- [ ] Emoji → SVG stroke icons (5 block icons)
- [ ] "Назад" → review topbar pattern
- [ ] Topbar weight/density vs hub
- [ ] Font sizes vs DESIGN.md scale
- [ ] Shadow values vs hub
- [ ] Header gradient like hub pages
