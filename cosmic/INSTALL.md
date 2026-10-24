# coderkrow for COSMIC

Custom COSMIC desktop themes built from `.ai/rules/brand/RULES.md` —
the same `coderkrow` palette already used by Ghostty, Starship, Zed,
opencode, and herdr.

Two variants, one palette:

| File | Palette | Ground | Text |
| --- | --- | --- | --- |
| `coderkrow-dark.ron` | `Dark` | `#111110` | `#e8e6df` |
| `coderkrow-light.ron` | `Light` | `#f5f4f0` | `#1d1d1b` |

- ground is never `#000` / `#fff` — always the warm off-white or
  near-black brand tokens
- brand teal `#1a595a` on active hints / window decoration
- interactive accent: signal cyan `#00d1d4` in dark, teal-mid `#2e7f80`
  in light (cyan has only 1.7:1 contrast on the light ground)
- teal and cyan hues are identical in both variants — only the neutral
  ramp and the ground invert
- no purple, no gradients, flat surfaces, `is_frosted: false`

## How COSMIC themes work

COSMIC does **not** read a plain config file for themes. A theme is a
RON document (`coderkrow-dark.ron`, `coderkrow-light.ron`) imported
through the desktop:

```
Settings → Appearance → custom theme import
```

Each file carries the full palette, spacing, corner radii, background,
text tint, accent, and container colors in one document. The `palette:
Dark(...)` / `palette: Light(...)` variant also tells COSMIC which side
of the auto light/dark switch the theme belongs to.

## Activate

Both files in this repo are complete COSMIC themes. Pick one of the two
install styles below, once per variant you want.

### Option A — import via Settings (recommended)

1. Open COSMIC Settings → Appearance.
2. Import `cosmic/coderkrow-dark.ron` and/or `cosmic/coderkrow-light.ron`
   as custom themes.
3. Select `Coderkrow Dark` or `Coderkrow Light`.

### Option B — copy to the themes directory

Copy the `.ron` files into your COSMIC custom-themes location, then
select `Coderkrow Dark` / `Coderkrow Light` under Settings → Appearance.

### Reload

No command needed — the desktop applies the theme as soon as you select
it in Settings. To have COSMIC pick the variants automatically, choose
`Coderkrow Dark` for dark mode and `Coderkrow Light` for light mode in
the same Appearance panel.

## Verify

Confirm after selecting the theme:

- dark: background near-black `#111110`, text warm off-white `#e8e6df`
- light: background warm off-white `#f5f4f0`, text near-black `#1d1d1b`
- accent highlights render cyan `#00d1d4` (dark) or teal `#2e7f80`
  (light)
- containers and panels stay flat, no gradients or frosted blur

If the import is rejected, the RON failed to parse — re-copy the file
unmodified from this repo and try again.

## Tweak

- Edit the color tuples in the `.ron` file, re-import, then re-select the
  theme.
- `bg_color`, `text_tint`, and `accent` control different parts of the
  desktop — change them together when shifting accents.
- Keep the two variants in sync: the light file only changes the neutral
  ramp (`neutral_0` lightest → `neutral_10` darkest, the reverse of the
  dark file), the ground, the container fills, and the accent colors that
  need contrast on a light background. Teal, cyan, and `window_hint` are
  shared verbatim.
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
