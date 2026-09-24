# coderkrow for COSMIC

Custom COSMIC desktop theme built from `.ai/rules/brand/RULES.md` —
the same `coderkrow` palette already used by Ghostty, Starship, Zed,
opencode, and herdr.

- ground `#111110` (never `#000`), text `#e8e6df` (never `#fff`)
- brand teal `#1a595a` on active hints / window decoration
- interactive accent `#3bb8ba`, signal cyan `#00d1d4` for accent and
  active states only
- no purple, no gradients, flat surfaces

## How COSMIC themes work

COSMIC does **not** read a plain config file for themes. A theme is a
RON document (`coderkrow-dark.ron`) imported through the desktop:

```
Settings → Appearance → custom theme import
```

The file carries the full dark palette, spacing, corner radii,
background, text tint, accent, and container colors in one document.

## Activate

`cosmic/coderkrow-dark.ron` in this repo is a complete COSMIC dark
theme. Pick one of the two install styles below.

### Option A — import via Settings (recommended)

1. Open COSMIC Settings → Appearance.
2. Import `cosmic/coderkrow-dark.ron` as a custom theme.
3. Select `Coderkrow Dark`.

### Option B — copy to the themes directory

Copy `cosmic/coderkrow-dark.ron` into your COSMIC custom-themes
location, then select `Coderkrow Dark` under Settings → Appearance.

### Reload

No command needed — the desktop applies the theme as soon as you select
it in Settings.

## Verify

Confirm after selecting the theme:

- background is near-black `#111110`, text is warm off-white `#e8e6df`
- accent highlights render cyan `#00d1d4`
- containers and panels stay flat, no gradients or frosted blur

If the import is rejected, the RON failed to parse — re-copy the file
unmodified from this repo and try again.

## Tweak

- Edit the color tuples in `cosmic/coderkrow-dark.ron`, re-import, then
  re-select the theme.
- `bg_color`, `text_tint`, and `accent` control different parts of the
  desktop — change them together when shifting accents.
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
