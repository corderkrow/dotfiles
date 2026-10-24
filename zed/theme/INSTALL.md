# coderkrow for Zed

Custom Zed themes built from `.ai/rules/brand/RULES.md` — the same
`coderkrow` palette already used by Ghostty, Starship, opencode, herdr,
and COSMIC. Ships both variants:

| File | Registers | Appearance |
| --- | --- | --- |
| `coderkrow-dark.json` | `coderkrow dark` | `dark` |
| `coderkrow-light.json` | `coderkrow light` | `light` |

## Palette

Dark:

- ground `#111110` (never `#000`), text `#e8e6df` (never `#fff`)
- code surface (editor, gutter, terminal) is card surface `#1a1a18` —
  chrome stays `#111110`, active tab merges into editor
- active line `#22221e`, keywords/accent `#00d1d4`, strings `#3bb8ba`,
  comments `#888780` italic

Light:

- ground `#f5f4f0` (never `#fff`), text `#1d1d1b` (never `#000`)
- code surface `#faf9f6` and toolbar sit one step above the ground —
  chrome stays `#f5f4f0`, active tab merges into editor
- active line `#f0eee8`, keywords `#1a595a`, strings/types `#2b7677`,
  comments `#736e66` italic
- teal hues are unchanged between variants; only the ground under them
  moves. `#00d1d4` / `#3bb8ba` are too low-contrast for text on the
  light ground (1.7:1 / 2.3:1), so the light theme keeps them for fills,
  selection and search washes and uses the deep teal steps for code.

Both:

- no purple, no gradients, no shadows, flat borders only
- weights 400/500/italic only, no bold

## How Zed themes work

Zed loads local theme files from its themes directory. Each JSON file
registers one or more themes by `name` — the two files here register
`coderkrow dark` and `coderkrow light`, so the light/dark toggle in Zed
switches between them without a restart.

```
~/.config/zed/themes/coderkrow-dark.json    # dark variant
~/.config/zed/themes/coderkrow-light.json   # light variant
~/.config/zed/settings.json                 # optional pin (see below)
```

Reference: <https://zed.dev/docs/themes#build-your-theme>

## Activate

`zed/theme/coderkrow-{dark,light}.json` in this repo are complete Zed
themes. Pick one of the two install styles below.

### Option A — symlink (recommended for dotfiles)

```sh
mkdir -p ~/.config/zed/themes
ln -sf ~/dotfiles/zed/theme/coderkrow-dark.json  ~/.config/zed/themes/coderkrow-dark.json
ln -sf ~/dotfiles/zed/theme/coderkrow-light.json ~/.config/zed/themes/coderkrow-light.json
```

### Option B — copy

```sh
mkdir -p ~/.config/zed/themes
cp ~/dotfiles/zed/theme/coderkrow-*.json ~/.config/zed/themes/
```

Then in Zed: `theme selector: toggle` → `coderkrow dark` or
`coderkrow light`. Pin both so the OS appearance switch picks the right
one in `~/.config/zed/settings.json`:

```json
{
  "theme": {
    "mode": "system",
    "light": "coderkrow light",
    "dark": "coderkrow dark"
  }
}
```

Use `"mode": "light"` or `"mode": "dark"` instead of `"system"` to lock
one variant.

### Reload

No restart needed — the theme selector applies immediately. Edited theme
files are picked up on the next selector open.

## Verify

Open the theme selector and confirm both `coderkrow dark` and
`coderkrow light` are listed.

Dark renders: near-black chrome `#111110`, `#1a1a18` editor surface,
cyan keywords, teal strings, muted italic comments.

Light renders: warm off-white chrome `#f5f4f0`, `#faf9f6` editor
surface, deep teal keywords, mid-teal strings, gray italic comments —
no pure white background, no cyan body text.

If a theme is missing, check the file sits directly under
`~/.config/zed/themes/` with a `.json` extension and validates as JSON.

## Tweak

- Edit the tokens in `zed/theme/coderkrow-dark.json` or
  `coderkrow-light.json`, keep hex lowercase, then re-open the theme
  selector.
- `background` (chrome) and `editor.background` (code surface) control
  different parts of the UI — change them together when shifting tones.
- Keep the two variants' key sets identical so the OS appearance switch
  never falls back to missing values.
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
