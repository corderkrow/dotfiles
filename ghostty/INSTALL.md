# coderkrow for Ghostty

Custom Ghostty theme built from `.ai/rules/brand/RULES.md` — the same
`coderkrow` palette already used by Starship, Zed, opencode, herdr, and
COSMIC.

- ground `#111110` (never `#000`), text `#e8e6df` (never `#fff`)
- brand teal `#1a595a` on selection background
- interactive accent `#3bb8ba`, signal cyan `#00d1d4` for cursor and
  active states only
- no purple, no gradients, flat surfaces

## How Ghostty themes work

Ghostty loads theme files from its themes directory and selects one by
name in its config file:

```
~/.config/ghostty/themes/coderkrow   # theme file
~/.config/ghostty/config             # contains `theme = coderkrow`
```

Reference: <https://ghostty.org/docs/config>

## Activate

`ghostty/coderkrow` in this repo is a complete Ghostty theme file
(16-color ANSI palette, cyan cursor, teal selection). Pick one of the
two install styles below.

### Option A — symlink (recommended for dotfiles)

```sh
mkdir -p ~/.config/ghostty/themes
ln -sf ~/dotfiles/ghostty/coderkrow ~/.config/ghostty/themes/coderkrow
```

Then set in `~/.config/ghostty/config`:

```
theme = coderkrow
```

### Option B — copy

```sh
mkdir -p ~/.config/ghostty/themes
cp ~/dotfiles/ghostty/coderkrow ~/.config/ghostty/themes/coderkrow
```

Then set `theme = coderkrow` in `~/.config/ghostty/config`. Use this
style if you keep local Ghostty settings that diverge from the repo.

### Reload

Ghostty applies the theme on launch. Open a new window, or reload the
config from the running instance. No daemon restart needed.

## Verify

Open a new Ghostty window and confirm:

- background is near-black `#111110`, foreground is warm off-white
  `#e8e6df`
- selection highlight is teal `#1a595a`
- cursor is cyan `#00d1d4`

If Ghostty falls back to a default theme, check that the file exists at
`~/.config/ghostty/themes/coderkrow` and that `theme = coderkrow` is
spelled exactly that way in `~/.config/ghostty/config`.

## Tweak

- Edit the tokens in `ghostty/coderkrow`, keep hex lowercase, then open
  a new window.
- `selection-background` and `cursor-color` control different parts of
  the UI — change them together when shifting accents.
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
