# coderkrow dark for Zed

Dark-only theme built from `.ai/rules/brand/RULES.md` code-block spec:

- bg `#111110`, surface `#1a1a18`, text `#e8e6df`, muted `#888780`
- code surface (editor, gutter, terminal) = card surface `#1a1a18` — chrome stays `#111110`, active tab merges into editor
- active line `#22221e` (1.09:1, visible without glow)
- keywords/accent `#00d1d4`, strings `#3bb8ba`, comments `#888780` (italic, dimmed to `#71706a` for long sessions)
- no purple, no gradients, no shadows, flat borders only
- weights 400/500/italic only, no bold

## Install (local theme, per https://zed.dev/docs/themes#build-your-theme)

```sh
mkdir -p ~/.config/zed/themes
cp zed/theme/coderkrow-dark.json ~/.config/zed/themes/
```

Then in Zed: `theme selector: toggle` → `coderkrow dark`.
Pin it:

```json
{
  "theme": {
    "mode": "dark",
    "light": "coderkrow dark",
    "dark": "coderkrow dark"
  }
}
```
