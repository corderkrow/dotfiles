# coderkrow for herdr

Custom herdr theme built from `.ai/rules/brand/RULES.md` — the same
`coderkrow` palette already used by Ghostty, Starship, Zed, opencode, and
COSMIC. Two variants, one palette:

| File | Registers | Ground | Text | `theme.name` |
| --- | --- | --- | --- | --- |
| `config.toml` | dark | `#111110` | `#e8e6df` | `catppuccin` |
| `config-light.toml` | light | `#f5f4f0` | `#1d1d1b` | `catppuccin-latte` |

Dark:

- ground `#111110` (never `#000`), text `#e8e6df` (never `#fff`)
- brand teal `#1a595a` on active rows / selection
- interactive accent `#3bb8ba`, signal cyan `#00d1d4` for info and
  active states only

Light:

- ground `#f5f4f0` (never `#fff`), text `#1d1d1b` (never `#000`)
- active row `#dcebeb`, selection `#c3dede` — teal tints on the warm
  off-white ground
- accent `#1a595a` (deep teal). Signal cyan `#00d1d4` is 1.7:1 on the
  light ground, so it is kept for fills only; `teal` becomes `#007b7d`
  (4.6:1) and `blue` `#1f6b8f` (5.4:1) when the token carries text
- teal and cyan hues are identical in both variants — only the ground
  and the neutral steps invert

Both: no purple, no gradients, flat surfaces.

## How herdr themes work

Herdr does **not** load theme files from a directory. The only built-in
themes live inside the binary (`catppuccin`, `catppuccin-latte`,
`tokyo-night`, `tokyo-night-day`, `gruvbox`, `gruvbox-light`, `dracula`,
`nord`, `one-dark`, `one-light`, `solarized`, `solarized-light`,
`kanagawa`, `kanagawa-lotus`, `rose-pine`, `rose-pine-dawn`, `vesper`,
`terminal`). A custom theme is therefore a base theme selected with
`theme.name` plus per-token overrides under `[theme.custom]` — all inside
herdr's config file:

```
~/.config/herdr/config.toml      # Linux / macOS
%APPDATA%\herdr\config.toml      # Windows
```

Herdr reads exactly one config file, so a variant is a whole file, not a
directory entry: symlink `config.toml` for dark, `config-light.toml` for
light. Both files also carry the other appearance under
`[theme.custom.dark]` / `[theme.custom.light]`, so either one can drive
`auto_switch` on its own.

Reference: <https://herdr.dev/docs/config-reference/#ref-theme>

## Activate

Both files in this repo are complete herdr configs carrying the theme.
Pick the variant you want and one of the two install styles below.

### Option A — symlink (recommended for dotfiles)

```sh
mkdir -p ~/.config/herdr

# dark
ln -sf ~/dotfiles/herdr/config.toml       ~/.config/herdr/config.toml

# or light
ln -sf ~/dotfiles/herdr/config-light.toml ~/.config/herdr/config.toml
```

Switching variants is a one-line symlink swap plus
`herdr server reload-config` — no restart.

### Option B — merge into an existing config

Copy the `[theme]`, `[theme.custom]`, `[theme.custom.light]` /
`[theme.custom.dark]`, and `[ui]` tables from `herdr/config.toml` (dark)
or `herdr/config-light.toml` (light) into your existing
`~/.config/herdr/config.toml`.

**Do not duplicate table headers.** TOML rejects a repeated table and herdr
falls back to defaults with `config.toml invalid; using defaults`. Every
config here already has a `[ui]` table (`status_indicators`, `[ui.toast]`,
…), so merge its keys into that block instead of pasting a second `[ui]`:

```toml
# existing config
onboarding = false

[ui.toast]
delivery = "system"

# keys from herdr/config.toml go here, not under a new [ui] header
[ui]
status_indicators = "symbols"
accent         = "#3bb8ba"   # "#1a595a" for the light variant
```

Same rule for `[theme]` and `[theme.custom]`: add the missing keys to the
existing table. A repeated header is the most common cause of the
`invalid; using defaults` warning.

### Reload

```sh
herdr server reload-config
```

Or open the global menu inside herdr and choose **reload config**. Theme
changes apply without restarting panes.

## Verify

```sh
herdr config check
```

Prints diagnostics for `~/.config/herdr/config.toml`. A valid file reports
`config: ok`; a bad color value or an unknown token is reported and herdr
falls back to a safe default with a warning. A duplicate table header
(usually a second `[ui]` from an Option B merge) produces
`config parse error: … duplicate key 'ui' in document root`; fix the merge
and re-run `herdr config check` until it reports `config: ok`.

To check a variant before installing it, point herdr at the file directly:

```sh
HERDR_CONFIG_PATH=~/dotfiles/herdr/config-light.toml herdr config check
```

Then confirm on screen:

- dark: panels `#111110`, text `#e8e6df`, active row `#1a595a`, cyan
  `#00d1d4` accents
- light: panels `#f5f4f0`, text `#1d1d1b`, active row `#dcebeb`, deep-teal
  `#1a595a` accents — no pure white background, no cyan body text
- borders, separators and surfaces stay flat in both

## Light / dark auto-switch

Each file ships the opposite appearance in a sub-table, so either can
follow the host terminal instead of pinning one variant. Uncomment these
three lines under `[theme]`:

```toml
# in config.toml (dark base)          # in config-light.toml (light base)
auto_switch = true                    auto_switch = true
dark_name   = "catppuccin"            dark_name   = "catppuccin"
light_name  = "catppuccin-latte"      light_name  = "catppuccin-latte"
```

`[theme.custom]` paints the file's own appearance; `[theme.custom.light]`
(in `config.toml`) or `[theme.custom.dark]` (in `config-light.toml`) paints
the other one. Manual theme selection in herdr Settings disables
`auto_switch`.

## Tweak

- Edit the tokens in `herdr/config.toml` or `herdr/config-light.toml`,
  keep hex lowercase, then `herdr server reload-config`.
- `theme.custom.accent` and `ui.accent` control different parts of the UI —
  change them together.
- Keep the two files in sync: the light variant only changes the ground,
  the neutral steps, the container fills, and the colors that need
  contrast on a light background. Teal, cyan and the dark tokens are
  shared verbatim — `config.toml`'s `[theme.custom.light]` block must
  match `config-light.toml`'s shared tokens, and `config-light.toml`'s
  `[theme.custom.dark]` block must match `config.toml`'s shared tokens.
- Allowed color formats: `#rrggbb`, named colors (`cyan`, `blue`, …),
  `rgb(r,g,b)`, or reset aliases (`reset`, `default`, `none`, `transparent`).
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
