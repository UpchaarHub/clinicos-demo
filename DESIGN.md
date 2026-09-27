# ClinicOS Demo — Design System

Single-file demo app (`index.html`, vanilla JS, zero dependencies). Every color,
font size, spacing, and corner radius in the file follows this document.
Light theme only; all body text meets WCAG AA (≥ 4.5:1) on its background.

## 1. Palette (restrained)

| Token | Value | Used for |
|---|---|---|
| `--teal` | `#0D9488` | Primary actions, active nav, brand mark, links-as-buttons |
| `--teal-dark` | `#0B7C72` | Hover states, emphasis text, stat values |
| `--teal-light` | `#E6F7F5` | Selected backgrounds (active nav, role option), avatars, token numbers |
| `--bg` | `#F2F6F6` | Page background |
| `--card` | `#FFFFFF` | Cards, modals, sheets, inputs |
| `--ink` | `#14332F` | Primary text, toast background |
| `--muted` | `#5F716E` | Secondary text, labels, table headers |
| `--line` | `#E2EAE9` | Borders, dividers, input borders |
| `--danger` | `#DC2626` | Destructive actions, errors, allergy tags |
| `--red-bg` | `#FDECEC` | Error banners |
| `--amber` | `#B45309` | Warning text |
| `--amber-bg` | `#FEF3E2` | Warning banners |
| `--green` | `#15803D` | Success text, status dots |
| `--green-bg` | `#E9F7EE` | Success pills |
| `--info` | `#1E40AF` | Informational text |
| `--info-bg` | `#EEF6FF` | Informational banners |
| `--info-line` | `#CFE4FB` | Informational borders |
| `--banner-bg` / `--banner-line` / `--banner-ink` | `#FFF8E6` / `#F0DFAE` / `#8A6D1A` | Demo banner on login |
| `--pill-wait-bg` / `--pill-wait-ink` | `#FFF7E6` / `#A16207` | "waiting / unpaid" pills |
| `--pill-prog-bg` / `--pill-prog-ink` | `#E0F2FF` / `#0369A1` | "in-progress" pills |

Status colors are semantic only: green = done/paid/active, amber = waiting/unpaid/paused,
blue = in-progress, red = destructive/stop. Never use color alone — every status also has a text label.

**Intentional exception:** the WhatsApp Center phone mock keeps real WhatsApp brand
colors (phone `#0B141A`, wallpaper `#E5DDD2`, outgoing bubble `#D9FDD3`, ticks `#53BDEB`,
meta `#667781`). It is a device mock, not app chrome.

## 2. Type scale

System stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Noto Sans", Arial, sans-serif`
(Hindi renders via system Devanagari fonts; verified clean in screenshots).

| Element | Size / weight |
|---|---|
| `h1` (login brand) | 24px / 800 |
| `h2` (page titles) | 20px / 700 |
| `h3` (card titles) | 16px / 700 |
| Body | 15px / 400, line-height 1.45 |
| Small (subs, hints) | 12–13px, `--muted` |
| Micro labels (section headers, table heads) | 10.5–11.5px / 700, uppercase, letter-spaced, `--muted` |
| Stat values | 24px / 800, `--teal-dark` |

## 3. Spacing scale

`4 · 8 · 10 · 12 · 14 · 16 · 20 · 24 · 28` — no other values.
Card padding 16 · card bottom margin 14 · page-head bottom margin 14 ·
main padding 16 desktop / 12 mobile · field bottom margin 12.

## 4. Corner radii

| Radius | Used for |
|---|---|
| 6px | small tags |
| 8–10px | inputs, small buttons (`.btn.sm` 9px), banners |
| 12px | buttons, token rows, role options |
| 14px | cards, stats, sidebar nav |
| 16–20px | brand mark (16), login card (20) |
| 20–24px | pills (20), toasts (24) |
| 26px | phone mock |
| 50% | avatars, status dots |

Shadows: `--shadow: 0 2px 10px rgba(20,51,47,.07)` — cards, tokens, nav. Nothing else.

## 5. Components

- **Buttons** — `.btn`: full-width, 13px/18px padding, 15px/700, radius 12, teal bg + white text.
  `.btn.sm`: auto width, 10px/14px padding, 13px, radius 9 (≥ 40px touch target).
  Variants: `.secondary` (white bg, teal border+text), `.ghost` (pale `#EEF4F3` bg),
  `.danger` (red bg). One primary action per card/modal — it comes first.
- **Button states** — hover: darken 6% (`filter:brightness(.94)`); pressed: `scale(.98)`;
  disabled: 45% opacity, `not-allowed`; keyboard focus: 2px teal `outline` offset 2px
  (`:focus-visible`, global).
- **Fields** — label 12.5px/600 `--muted`; input/select/textarea 15px, 11–12px padding,
  1.5px `--line` border, radius 10, white bg; focus: teal border; invalid: `--danger`
  border + `.err` message (12.5px/600 red) directly under the field.
- **Cards** — white, radius 14, `--shadow`, padding 16. Card titles are `h3`.
- **Rows** — `.prow`: 11px vertical padding, `--line` divider, pointer cursor when clickable;
  clickable rows are keyboard-focusable (`tabindex`, Enter/Space activates) with the same
  focus ring as buttons.
- **Pills / tags** — pill: 11px/700, radius 20, semantic bg+ink. Tag: 11px/700, radius 6.
- **Nav** — desktop sidebar (220px, sticky); mobile bottom nav (4 primary + "More" sheet).
  Active item: `--teal-light` bg + `--teal-dark` text. Buttons ≥ 44px tall.
- **Modal** — bottom sheet on mobile (top radius 18), centered dialog on desktop (radius 18);
  opens with a 0.2s fade+rise; veil click and `Esc` dismiss.
- **Sheet** — mobile "More" menu, slides up 0.25s, `Esc`/veil dismisses.
- **Toast** — ink bg, white 13.5px/600 text, radius 24, slides up 0.25s, auto-dismiss 2.4s.
  Success/failure/info only — never the sole carrier of a form error.
- **Tables** — `.log`: 13px, muted uppercase micro headers, `--line` row dividers;
  wrapped in `.tablewrap` (horizontal scroll container) so wide tables never cause page-level sideways scroll.
- **Toggle** — `.tgl`: 48×27px, teal when on, knob slides 0.15s; always has `aria-pressed` + text label.
- **View transitions** — `#view` fades in 0.15s on every navigation.

## 6. States

- **Loading** — n/a: all storage is synchronous localStorage; no spinners needed.
- **Empty** — every list has one: "Queue is clear.", "No patients found.", "No bills yet.",
  "No visits in range.", "No messages yet.", "No follow-ups due." — muted 13px, never a blank card.
- **Error** — inline `.err` under the offending field (login PIN, patient registration);
  toasts for transient failures (mic unavailable, bad import file).
- **Submitting/success/failure** — every mutating action ends in a toast naming what happened
  ("Token #6 issued", "Bill R-104 marked paid", "Clinic profile saved").

## 7. Responsive

Breakpoint 820px. Below it: sidebar → bottom nav + More sheet; `.stats` 4→2 columns;
`.grid2` → 1 column; main padding 12 with 96px bottom clearance for the nav.
No page-level horizontal scrolling at 390px (tables scroll inside `.tablewrap`).
Layout holds at 200% text size (no fixed-height text containers).

## 8. Launch checklist (per page)

One-line value prop on the login screen ("AI-powered clinic & hospital management").
One primary CTA per view. `document.title` updates per view ("Token Queue · ClinicOS").
Meta description + SVG favicon (teal rounded square, white plus). Zero placeholder text —
`placeholderPage()` was removed; the only "…"-style copy is intentional empty-state guidance.
