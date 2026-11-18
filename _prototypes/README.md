# Home page prototypes

`home-variants.html` is a standalone prototype for a redesigned home page.
Open it directly in a browser (`open _prototypes/home-variants.html`). Quarto
ignores this folder because its name starts with `_`, so nothing here is
published.

A switcher at the bottom of the page picks the layout; in variant C a second
row picks the motion motif. A URL hash opens a state directly:
`#A`, `#B`, `#C`, or `#C-<motif>` (for example `#C-walk2rio`). The last choice
is remembered per browser.

**Decision (Nov 2026):** variant C with the *Mixture → Rio* motif went live on
`index.qmd` (Walk → Rio was picked first, then swapped for Mixture → Rio as the
more natural link between a curve and the landscape). Everything else here is
kept for reference.

The live drawing is a static export of the prototype's SVG, pasted into a raw
HTML block in `index.qmd`, so the live page builds nothing in JavaScript. A
two-line script jumps it to the finished frame when the visitor has *reduce
motion* on. Its styles are the `.rio-sketch` rules in `custom.scss`. To change
the drawing, edit the motif here, then re-export it: load
`home-variants.html#C-mixture`, copy the `<svg class="series tall rio">`
element, and rename its class to `rio-sketch`.

## Where the ideas came from

Three design-resource posts on X were reviewed for ideas:

- Viktor Oddy's list of 15 resources (motionsites.ai prompts, land-book,
  godly.website, Fontshare, realtimecolors, coolors, Lucide, svgl, and others).
- Tobi's MCP component library (glass pricing cards, 3D card carousels).
- Lucas's list (scrolltide 3D scroll components, scrollshaders, footer.design,
  cta.gallery, refero styles).

Verdict: almost all of it is aimed at product landing pages and reads as
marketing on an academic site. Worth borrowing: **Fontshare** (the Gambetta
serif comes from there), **realtimecolors** (testing the palette, including a
future dark mode), and the galleries for layout and spacing ideas only. Lucide
was ruled out because it has no Google Scholar, ORCID or RePEc icons, so
Academicons stays.

The Rio motifs were inspired by the hand-drawn sketch (croquis) of Sugarloaf
and Urca in the FGV EPGE site header. The drawing here is generated from
curves and does not copy EPGE's artwork, so the page doesn't borrow FGV
branding.

## Layouts

| Variant | What it is |
|---|---|
| **A · Current** | The live home page as it was: Geist sans-serif name, four paragraphs, portrait on the right. Baseline for comparison. |
| **B · Editorial** | Mono kicker ("Economics & Finance · FGV EPGE"), the name in Gambetta serif on one line, a smaller portrait, a one-sentence serif lede, a short bio, profile links, and the three current working papers with the coloured status dots. |
| **C · + motion** | B plus one small drawing under the name that animates once and then stays still. |

B went through one revision. The first version set the name huge and on two
lines ("Felipe S." / grey italic "Iachan"); it was cut to one upright line at
about half the size (about 56px desktop, 38px phone), and the portrait shrank
from 220px to 180px, centred beside the name.

## Motion motifs (variant C)

Each motif draws once, then holds. With *reduce motion* switched on in the
operating system, each one shows its finished state with no animation.

### Data motifs (64px strip, warm grey ink)

| Hash | Motif | What draws |
|---|---|---|
| `walk` | Random walk | A seeded random walk with a faint shaded band. |
| `fan` | Fan chart | History line, a dotted "today" marker, then a widening three-band forecast fan with a dashed central path. |
| `irf` | Impulse response | Dashed zero line, a response that dips and recovers, and a confidence band. |
| `scatter` | Scatter + fit | About 90 dots appear in sequence, then an OLS line draws through them. |
| `curves` | Yield curves | Five Nelson–Siegel term structures, drawn one after another, each darker. |
| `hist` | Histogram | Bars grow from the baseline, then a normal density draws over them. |

### Rio motifs (120px strip, navy accent ink)

All four end with the same scene: Sugarloaf and Urca, three wavy water lines,
small boxy buildings, and the cable line with a tiny cable car that crosses
once to the summit.

| Hash | Motif | What draws |
|---|---|---|
| `croquis` | Rio sketch | Pure pen sketch: water, then Urca and Sugarloaf as overlapping arcs, a faint second stroke for a hand-drawn feel, shading, buildings, cable car. |
| `mixture` | **Mixture → Rio** (live) | A flat axis and two Gaussian components draw first (a two-component mixture); the bells sharpen into the mountains and the axis ripples into the bay. |
| `walk2rio` | Walk → Rio | The random walk draws, then settles into the skyline outline; water, shading, buildings and cable car follow. |
| `irf2rio` | IRF → Rio | Act 1 is an impulse response (shock arrow, dashed zero line, peak, undershoot, smaller rebound, confidence band). Act 2 morphs it: peak → Sugarloaf, rebound → Urca, undershoot → saddle, zero line → bay, band → shading. |

## Technical notes

- **No libraries.** Everything is inline SVG. Line drawing uses CSS
  `stroke-dashoffset` with `pathLength="1000"`; shape changes use SVG `<animate
  attributeName="d">` between two paths with the same number of points; the
  cable car uses `<animateMotion>`.
- **Don't combine a CSS animation and an SVG `<animate>` on the same element.**
  In IRF → Rio the band's CSS fade-in restarted whenever the morph ran, so the
  band vanished. The fix was to put the CSS fade on a wrapping `<g>` and the
  morph on the inner `<path>`.
- A `<set>` on a presentation attribute (`stroke-dasharray`) did not take
  effect, so the dashed zero line in IRF → Rio crossfades into a separate
  solid line instead.
- `pop()` must merge an element's existing `class` with `pop`; an early
  version wrote two `class` attributes and the second was silently dropped,
  so bands drew as outlines.
- The mountains use an asymmetric generalised bell,
  `base − h·exp(−|d/w|^p)` with different left and right widths.
  Sugarloaf: centre 640, height 112, widths 50/40, p = 3.4 (steep dome).
  Urca: centre 785, height 50, widths 52/80, p = 2.2.
- Screenshots for review were taken with headless Chrome
  (`--virtual-time-budget` to pick the moment in the animation), using a copy
  with the portrait embedded so it loads from `file://`.
