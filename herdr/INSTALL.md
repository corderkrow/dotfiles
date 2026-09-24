# coderkrow for herdr

Custom herdr theme built from `.ai/rules/brand/RULES.md` — the same
`coderkrow` palette already used by Ghostty, Starship, Zed, opencode, and
COSMIC.

- ground `#111110` (never `#000`), text `#e8e6df` (never `#fff`)
- brand teal `#1a595a` on active rows / selection
- interactive accent `#3bb8ba`, signal cyan `#00d1d4` for info and
  active states only
- no purple, no gradients, flat surfaces

## How herdr themes work

Herdr does **not** load theme files from a directory. The only built-in
themes live inside the binary (`catppuccin`, `tokyo-night`, `gruvbox`,
`dracula`, `nord`, `one-dark`, `solarized`, `kanagawa`, `rose-pine`,
`vesper`, `terminal`, plus light siblings). A custom theme is therefore a
base theme selected with `theme.name` plus per-token overrides under
`[theme.custom]` — all inside herdr's config file:

```
~/.config/herdr/config.toml      # Linux / macOS
%APPDATA%\herdr\config.toml      # Windows
```

Reference: <https://herdr.dev/docs/config-reference/#ref-theme>

## Activate

`herdr/config.toml` in this repo is a complete herdr config carrying the
theme. Pick one of the two install styles below.

### Option A — symlink (recommended for dotfiles)

If you do not already have a herdr config:

```sh
mkdir -p ~/.config/herdr
ln -sf ~/dotfiles/herdr/config.toml ~/.config/herdr/config.toml
```

### Option B — merge into an existing config

Copy the `[theme]`, `[theme.custom]`, `[theme.custom.light]`, and `[ui]`
tables from `herdr/config.toml` into your existing
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
accent         = "#3bb8ba"
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
no errors; a bad color value is rejected at startup and herdr falls back to
a safe default with a warning. A duplicate table header (usually a second
`[ui]` from an Option B merge) produces
`config parse error: … duplicate key 'ui' in document root`; fix the merge
and re-run `herdr config check` until it reports `config: ok`.

## Light / dark auto-switch

By default the theme is dark-only, matching the rest of the dotfiles stack.
To follow the host terminal's light/dark appearance, uncomment these three
lines under `[theme]`:

```toml
auto_switch = true
dark_name  = "catppuccin"
light_name = "catppuccin-latte"
```

`[theme.custom.light]` then repaints the light appearance with the coderkrow
light tokens (warm off-white `#f5f4f0`, ink `#1d1d1b`, deep-teal accent).
The shared `[theme.custom]` values remain the dark appearance. Manual theme
selection in herdr Settings disables `auto_switch`.

## Tweak

- Edit the tokens in `herdr/config.toml`, keep hex lowercase, then
  `herdr server reload-config`.
- `theme.custom.accent` and `ui.accent` control different parts of the UI —
  change them together.
- Allowed color formats: `#rrggbb`, named colors (`cyan`, `blue`, …),
  `rgb(r,g,b)`, or reset aliases (`reset`, `default`, `none`, `transparent`).
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
