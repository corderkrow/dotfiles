# coderkrow for opencode

Custom opencode TUI theme built from `.ai/rules/brand/RULES.md` — the
same `coderkrow` palette already used by Ghostty, Starship, Zed, herdr,
and COSMIC.

- ground `#111110` (never `#000`), text `#e8e6df` (never `#fff`)
- brand teal `#1a595a` on selection / focused states
- interactive accent `#3bb8ba`, signal cyan `#00d1d4` for keywords,
  headings, and active states only
- no purple, no gradients, flat surfaces

## How opencode themes work

opencode loads custom themes from JSON files in its themes directories.
Later directories override earlier ones:

```
~/.config/opencode/themes/*.json     # user-wide themes
<project-root>/.opencode/themes/     # project themes
```

A theme is selected with the `/theme` command inside the TUI, or with
`"theme"` in `tui.json`. The file name (minus `.json`) is the theme
name — `coderkrow.json` registers as `coderkrow`.

Reference: <https://opencode.ai/docs/themes/>

## Activate

`opencode/themes/coderkrow.json` in this repo is a complete opencode
theme (dark `hue` scale, teal/cyan accents, matching syntax and markdown
tokens). Pick one of the two install styles below.

### Option A — symlink (recommended for dotfiles)

```sh
mkdir -p ~/.config/opencode/themes
ln -sf ~/dotfiles/opencode/themes/coderkrow.json ~/.config/opencode/themes/coderkrow.json
```

### Option B — copy

```sh
mkdir -p ~/.config/opencode/themes
cp ~/dotfiles/opencode/themes/coderkrow.json ~/.config/opencode/themes/
```

Then select it inside opencode with `/theme` → `coderkrow`, or pin it
in `tui.json`:

```json
{
  "$schema": "https://opencode.ai/tui.json",
  "theme": "coderkrow"
}
```

### Reload

No restart needed — `/theme` applies immediately. A new TUI session
picks up file changes automatically.

## Verify

```sh
ls ~/.config/opencode/themes/coderkrow.json
```

Then run `/theme` inside opencode and confirm `coderkrow` is listed and
selectable. If it is missing, check the file is valid JSON and sits
directly under `themes/` (not nested).

## Tweak

- Edit the tokens in `opencode/themes/coderkrow.json`, keep hex
  lowercase. Syntax colors live under `base.syntax`, markdown under
  `base.markdown`, the dark hue scale under `dark.hue`.
- `cyan` is the accent/interactive alias — `blue`, `purple`,
  `accent`, and `interactive` all point at it. Change them together.
- Requires a truecolor terminal (`echo $COLORTERM` should report
  `truecolor` or `24bit`).
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
