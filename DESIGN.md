# Design

Direction: **Bayt, the bilingual editorial** (chosen from four directions on 2026-07-18). Static, dependency-free site (plain HTML/CSS/JS, GitHub Pages), fully self-contained: system fonts, inline SVG, no CDNs, no external requests.

## Concept

Typography is the design. Poster-scale New York serif English in duet with monumental gold Arabic ghost words, set on warm paper with ruled lines. One emerald accent, spent with intent: the italic emphasis word in each headline, links, and the single drenched "for masjids" band. Screenshots are artifacts placed in the composition, not the composition itself.

## Tokens (style.css `:root`)

- Light ("paper"): `--paper #f6f3ea`, `--ink #17120c`, `--ink-2 #574e3d`, `--ink-3 #8a7f66`, rules `rgba(23,18,12,0.22)`.
- Dark ("night paper", ink and paper swap): `--paper #16110a`, `--ink #f0e9d8`, `--ink-2 #beb298`, emerald lightens to `#7fc4a2`, gold to `#d3b465`.
- Accent: `--emerald #1d5a41` (the only color spent on meaning); `--gold #97781f` for Arabic, check marks, diamonds; `--gold-ghost` ~15% for monumental Arabic.
- Ease: `--ease-out cubic-bezier(0.16,1,0.3,1)`.

Contrast: ink 13+:1, ink-2 ≥6:1, emerald ≥7:1 on paper; verified in both modes.

## Editorial grammar

- **Masthead** nav: wordmark + Arabic, ruled bottom edge on scroll, no icons.
- **Ghost Arabic** (`.ghost`): one monumental gold word per section (ٱلصَّلَاة، ٱلْمَسَاجِد، ٱلْإِقَامَة، ٱلسُّنَّة، ٱلتَّذْكِير، لِلْمَسَاجِد), aria-hidden, clipped by the section.
- **Rules** (`.rule-x`): 1px hairlines that draw themselves on reveal (`scaleX`), 2px heavy rule before the footer.
- **Display headlines**: serif 600, clamp up to ~124px in the hero, tracking −0.025em, one *italic emerald* word each (same family, never a second face).
- **Ruled lists**: feature points and FAQ rows separated by hairlines, no cards anywhere; details list uses a small gold ◆ lead.
- **Versus columns** (#mission): two text columns split by a vertical rule under a heavy top rule; ✕ vs ✓.
- **The one drenched moment**: #masjids band, solid emerald, paper text, gold CTA.
- **iPhone frames** (`.phone`): true iPhone 16 Pro Max geometry (1320×2868); hero phone rotated 5°, cropped at the right edge.

## Type

- Display: `"New York", "Iowan Old Style", Georgia` serif.
- Body: system SF stack 17px/1.65; standfirst 18–21px.
- Meta: 11.5px, tracking 0.2em, small caps; used once in the hero masthead line only (no per-section eyebrows).
- Arabic: `"Geeza Pro", "Baghdad", "Al Bayan"`, always `lang="ar" dir="rtl"`.
- Long left-aligned prose is justified with hyphenation (mission lede/coda, FAQ answers, doc pages).

## Motion (dial 5)

- Hero: headline lines rise from clipped containers (staggered), rules draw, standfirst and phone fade up.
- Sections: IO reveals (22px rise), rule draws, 70ms staggers.
- Phones drift ±22px on scroll via idle-stopping rAF lerp.
- Press: buttons scale 0.97; FAQ opens animate via `::details-content`.
- Full `prefers-reduced-motion` fallback.

## Voice rules (enforced in markup)

No em dashes. No personal names; community "we". Preserved lines: "So no one misses the jama'ah.", free forever / no ads / no accounts / no tracking, sadaqah jariyah framing, closing dua. Page slugs and anchor ids (`#nearby`, `#day`, `#learn`, `#reminders`, `#themes`, `#features`, `#mission`, `#faq`, `#masjids`) stable.
