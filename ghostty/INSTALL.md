# coderkrow for Ghostty

Custom Ghostty themes built from `.ai/rules/brand/RULES.md` — the same
`coderkrow` palette already used by Starship, Zed, opencode, herdr, and
COSMIC. One file per variant:

| File | Variant | Ground / text |
| ---- | ------- | ------------- |
| `ghostty/coderkrow.conf` | dark | `#111110` / `#e8e6df` |
| `ghostty/coderkrow-light.conf` | light | `#f5f4f0` / `#1d1d1b` |

Brand hues are identical in both: teal `#1a595a`, teal-mid `#2e7f80`,
teal-light `#3bb8ba`, signal cyan `#00d1d4`. Only the ground, the ink,
and the neutral/ANSI steps change.

- ground `#111110` (dark) / `#f5f4f0` (light) — never `#000` / `#fff`
- text `#e8e6df` (dark) / `#1d1d1b` (light) — never `#fff` / `#000`
- brand teal `#1a595a` on the dark selection background; teal tint
  `#c3dede` on the light one
- signal cyan `#00d1d4` for the dark cursor and active states only — it
  is 1.72:1 on the light ground, so light uses deep teal `#1a595a`
  (7.28:1) for the cursor and `#2b7677` / `#1a595a` for ANSI cyan
- no purple, no gradients, flat surfaces

## How Ghostty themes work

Ghostty loads theme files from its themes directory and selects one by
name in its config file:

```
~/.config/ghostty/themes/coderkrow        # installed theme file (dark)
~/.config/ghostty/themes/coderkrow-light  # installed theme file (light)
~/.config/ghostty/config                  # contains `theme = ...`
```

Ghostty resolves a theme by the **installed file name, literally** — it
does not append an extension. The repo files end in `.conf`, so they are
installed under the extensionless name (`…/themes/coderkrow-light`), and
the config selects them as `theme = coderkrow-light`. Selecting
`theme = coderkrow-light` while the themes directory holds only
`coderkrow-light.conf` fails with
`theme "coderkrow-light" not found, tried path "..."`.

A theme file is an ordinary Ghostty config file, so it uses the same keys
— both files here set `font-family`, background/foreground, cursor,
selection, the 16-color ANSI palette, and `palette-generate` for the
extended ANSI range.

Reference: <https://ghostty.org/docs/config>

## Activate

Pick one variant (or the light/dark pair), and one install style.

### Option A — symlink (recommended for dotfiles)

```sh
mkdir -p ~/.config/ghostty/themes
ln -sf ~/dotfiles/ghostty/coderkrow.conf       ~/.config/ghostty/themes/coderkrow
ln -sf ~/dotfiles/ghostty/coderkrow-light.conf ~/.config/ghostty/themes/coderkrow-light
```

Then set in `~/.config/ghostty/config`:

```
theme = coderkrow          # dark
# theme = coderkrow-light  # light
```

### Option B — copy

```sh
mkdir -p ~/.config/ghostty/themes
cp ~/dotfiles/ghostty/coderkrow.conf       ~/.config/ghostty/themes/coderkrow
cp ~/dotfiles/ghostty/coderkrow-light.conf ~/.config/ghostty/themes/coderkrow-light
```

The copy drops the `.conf` extension on purpose — the installed name is
the theme name. Then set `theme = coderkrow` or `theme = coderkrow-light` in
`~/.config/ghostty/config`. Use this style if you keep local Ghostty
settings that diverge from the repo.

### Follow the system appearance

One `theme` line can carry both files and switch with the desktop's
light/dark mode:

```
theme = light:coderkrow-light,dark:coderkrow
```

`light:` / `dark:` also accept absolute paths, which works before the
files are installed into the themes directory.

### Reload

Ghostty applies the theme on launch. Open a new window, or reload the
config from the running instance. No daemon restart needed.

## Verify

Validate either file with Ghostty's own parser — it rejects unknown keys
and unparsable colors:

```sh
ghostty +validate-config --config-file=~/dotfiles/ghostty/coderkrow.conf
ghostty +validate-config --config-file=~/dotfiles/ghostty/coderkrow-light.conf
```

Both must exit `0` with no output.

`+validate-config` also resolves `theme = ...` against the themes
directory, so it catches a name/extension mismatch. To check the live
config:

```sh
ghostty +validate-config --config-file=~/.config/ghostty/config
ghostty +list-themes | grep coderkrow   # both names must be listed
```

Then open a new Ghostty window and confirm:

- dark: background near-black `#111110`, foreground warm off-white
  `#e8e6df`, selection teal `#1a595a`, cursor cyan `#00d1d4`
- light: background warm off-white `#f5f4f0`, foreground ink `#1d1d1b`,
  selection teal tint `#c3dede`, cursor deep teal `#1a595a`
- colored `ls`, a `git diff`, and a shell prompt stay readable in the
  active variant

If Ghostty falls back to a default theme, check that a file exists at
`~/.config/ghostty/themes/<name>` and that `theme = <name>` matches that
installed name exactly — a `.conf` suffix left on the installed file
makes the name `coderkrow-light.conf`.

## Tweak

- Edit the tokens in `ghostty/coderkrow.conf` and
  `ghostty/coderkrow-light.conf` together, keep hex lowercase, then open
  a new window.
- `selection-background` and `cursor-color` control different parts of
  the UI — change them together when shifting accents.
- The light file keeps the dark file's slot-to-hue mapping and moves each
  ANSI color to a legible step on `#f5f4f0` (every text-bearing slot is
  ≥ 4.5:1). Signal cyan `#00d1d4` is fills/glows only and is deliberately
  absent from the light palette.
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
