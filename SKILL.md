---
name: warm-dashboard-ui
description: Apply the "Warm Neutral" web UI design system — cream background, single orange primary, slate accent, white hairline cards, pill components, segmented tab track, dot status chips, mono stats. Use whenever the user asks to style or restyle a web UI, create/update a design system, wants a warm/soft/cream look, mentions this system by name ("warm neutral", "Oyen style"), or shares a screenshot of this style to copy — even if they just say "make it match the design system".
---

# Warm Neutral design system

A soft, warm, low-chrome dashboard aesthetic: one orange accent doing all the
emotional work on a cream canvas, hairline-bordered white cards, everything
interactive is a pill. Calm by default; color appears only where it means
something (accent, status, data).

## When to apply

- Building or restyling any web UI (plain CSS, Tailwind, CSS-in-JS — tokens are framework-agnostic)
- User says "use the design system", "make it match the sample", "warm/soft/cream look"
- Do NOT apply to: dark-mode UIs, marketing pages needing high drama, or brand palettes that clash with orange

## Tokens

Start from `references/tokens.css` — copy the `:root` block and adapt values,
don't rename variables. The palette:

| Token | Value | Role |
|---|---|---|
| `--bg` | `#F7F5F1` | Warm off-white canvas. Flat — no gradients, no noise. |
| `--card` | `#FFFFFF` | Card/surface |
| `--border` | `#E9E6E0` | Hairline card borders (1px, always visible — cards are defined by border + slight shadow, never by heavy shadow) |
| `--fg` | `#26231E` | Near-black warm text |
| `--body-fg` | `#6E6A61` | Secondary text |
| `--muted-fg` | `#8A857B` | Tertiary/meta text |
| `--muted-bg` | `#F1EFEA` | Tracks, ghost buttons, nested panels |
| `--primary` | `#E07E2A` | Orange — CTAs, active data, brand. Hover `#C96D1F`. |
| `--accent` | `#64748B` | Slate — the *second* data color (bars, informational chips). Never used decoratively. |
| `--ok-*` | fg `#217A46` / bg `#E7F3EB` | Positive status |
| `--warn-*` | fg `#B25E09` / bg `#FCEEE0` | Busy/pending status |
| `--radius` | `20px` | Cards |
| `--radius-sm` | `12px` | Inputs, inner panels |
| `--radius-pill` | `999px` | Every button, chip, tab |
| `--shadow-sm` | `0 1px 2px rgba(30,26,20,.05)` | Resting cards |
| `--shadow-hover` | `0 10px 24px rgba(30,26,20,.08)` | Hover lift |
| `--speed` | `220ms` | All transitions |

## Component recipes

**Cards** — white, 1px `--border`, `--radius`, `--shadow-sm`. Hover (if
clickable): `translateY(-2px)` + `--shadow-hover`. Nested panels inside a card
use `--muted-bg` + `--radius-sm`, no border.

**Segmented tabs** — a track, not loose buttons: container gets `--muted-bg`,
4px padding, pill radius; inactive tabs transparent on the track; active tab =
white pill + 1px border + `--shadow-sm`, dark text. Inactive text `--body-fg`.
Orange is *not* used for the active tab.

**Buttons** — pills. Primary: orange bg, white text. Ghost: `--muted-bg`, no
border, dark text, hover darkens to `--muted-bg-strong`. Weight 600, not bold.

**Status chips** — borderless tinted pill: colored dot (7px, `currentColor`)
+ text in the same hue. ok=green, busy/pending=orange (`--warn-*`),
error=red (`#B91C1C` on `#FDECEA`), neutral=`--muted-bg`.

**Progress bars** — 4–5px tall, pill radius, track `--muted-bg-strong`-ish
gray. Fill color carries meaning: orange = active/compute, slate = storage/
memory. Two bars per card max.

**Metrics/stats** — mono font (`JetBrains Mono` or similar) for technical
stat lines like `GPU busy 31 s · 51 s wall`. Numbers get
`font-variant-numeric: tabular-nums`. Labels muted, values dark semibold,
right-aligned details muted.

**Section headers** — bold dark title left, muted meta right
("1 active · 50 in all"), separated by `·`.

## Rules

- Flat background. The cream canvas is flat; radial gradients and patterns break the system.
- 1px borders everywhere; drop the 2px-border habit. Depth comes from shadow tokens, not border thickness.
- One accent doing the work. If everything is orange, nothing is. Slate is the only sanctioned companion hue.
- Single sans family (Inter works) + one mono for stats. No serif display faces.
- Keep the existing a11y contract: visible `:focus-visible` rings (2px `--ring`, offset 2), `prefers-reduced-motion` kill-switch, SVG icons only (Lucide), no emoji icons.
- Mobile ≤640px: stacked inputs, full-width buttons, tab grids stay even (e.g. 2×2) rather than ragged wraps.

## Workflow

1. Read `references/tokens.css` and copy the `:root` block into the project's global stylesheet (or Tailwind config), adapting variable names to the project's existing convention so component classes don't churn.
2. Restyle components in place — keep existing class names and DOM structure; this is a token + recipe swap, not a rewrite.
3. Update brand marks (logo gradients, `theme-color`, favicon) to the orange→slate diagonal: `linear-gradient(135deg, #F2A65A, #E07E2A 45%, #64748B)`.
4. Run the app and let the user look before polishing details.

Full copy-paste starter (tokens + generic component classes): `references/tokens.css`.
Reference implementation: the IG Grabber frontend (`frontend/app/globals.css` in that repo) — every recipe above in production use.
