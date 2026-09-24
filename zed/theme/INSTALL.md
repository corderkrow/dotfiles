# coderkrow for Zed

Custom Zed theme built from `.ai/rules/brand/RULES.md` — the same
`coderkrow` palette already used by Ghostty, Starship, opencode, herdr,
and COSMIC.

- ground `#111110` (never `#000`), text `#e8e6df` (never `#fff`)
- code surface (editor, gutter, terminal) is card surface `#1a1a18` —
  chrome stays `#111110`, active tab merges into editor
- active line `#22221e`, keywords/accent `#00d1d4`, strings `#3bb8ba`,
  comments `#888780` italic
- no purple, no gradients, no shadows, flat borders only
- weights 400/500/italic only, no bold

## How Zed themes work

Zed loads local theme files from its themes directory. Each JSON file
registers one or more themes by `name` — `coderkrow-dark.json`
registers `coderkrow dark` (dark-only, matching the rest of the
dotfiles stack).

```
~/.config/zed/themes/coderkrow-dark.json   # theme file
~/.config/zed/settings.json               # optional pin (see below)
```

Reference: <https://zed.dev/docs/themes#build-your-theme>

## Activate

`zed/theme/coderkrow-dark.json` in this repo is a complete Zed theme.
Pick one of the two install styles below.

### Option A — symlink (recommended for dotfiles)

```sh
mkdir -p ~/.config/zed/themes
ln -sf ~/dotfiles/zed/theme/coderkrow-dark.json ~/.config/zed/themes/coderkrow-dark.json
```

### Option B — copy

```sh
mkdir -p ~/.config/zed/themes
cp ~/dotfiles/zed/theme/coderkrow-dark.json ~/.config/zed/themes/
```

Then in Zed: `theme selector: toggle` → `coderkrow dark`. Pin it in
`~/.config/zed/settings.json`:

```json
{
  "theme": {
    "mode": "dark",
    "light": "coderkrow dark",
    "dark": "coderkrow dark"
  }
}
```

### Reload

No restart needed — the theme selector applies immediately. Edited theme
files are picked up on the next selector open.

## Verify

Open the theme selector and confirm `coderkrow dark` is listed and
renders: near-black chrome `#111110`, `#1a1a18` editor surface, cyan
keywords, teal strings, muted italic comments. If the theme is missing,
check the file sits directly under `~/.config/zed/themes/` with a
`.json` extension and validates as JSON.

## Tweak

- Edit the tokens in `zed/theme/coderkrow-dark.json`, keep hex
  lowercase, then re-open the theme selector.
- `background` (chrome) and `editor.background` (code surface) control
  different parts of the UI — change them together when shifting tones.
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
