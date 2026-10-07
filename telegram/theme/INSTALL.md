# coderkrow for Telegram Desktop

Custom Telegram Desktop theme built from `.ai/rules/brand/RULES.md` — the
same `coderkrow` palette already used by Ghostty, Starship, Zed, opencode,
herdr, and COSMIC.

- ground `#111110` (never `#000`), surface `#1a1a18`, text `#e8e6df`
  (never `#fff`)
- teal `#1a595a` / `#2e7f80` for buttons, selection, and outgoing bubbles
- links, sent ticks, and inline accents `#3bb8ba`; signal cyan `#00d1d4`
  reserved for active states
- no purple, no gradients, flat borders, no shadows

## How Telegram Desktop themes work

A theme is a plain text file of `key: value;` color pairs. Rename it to
`.tdesktop-theme` and Telegram imports it directly:

```
~/dotfiles/telegram/theme/coderkrow-dark.tdesktop-theme
```

Telegram stores the imported theme under its own data directory; it does
not read the file in place at runtime. Re-import after editing.

A packaged theme (`.zip` renamed to `.tdesktop-theme`) may also contain a
`background.jpg` / `tiled.jpg` (`background` = fixed, `tiled` = repeated).
This theme ships **without** a background image — the flat `#111110`
ground is intentional and matches the rest of the stack.

Reference: <https://github.com/telegramdesktop/tdesktop/wiki/Theme-Reference>
and the sample palette in
<https://github.com/telegramdesktop/tdesktop/blob/dev/Telegram/Resources/default.tdesktop-theme>.

## Activate

`telegram/theme/coderkrow-dark.tdesktop-theme` in this repo is a complete,
single-file theme.

### Option A — import from disk (recommended)

1. Telegram Desktop → **Settings** → **Chat Settings** → **Theme**.
2. Click the folder icon / **Create a new theme**, choose
   `telegram/theme/coderkrow-dark.tdesktop-theme`, and apply.
3. The theme appears under "Custom themes".

Or symlink it somewhere convenient first:

```sh
mkdir -p ~/.local/share/coderkrow
ln -sf ~/dotfiles/telegram/theme/coderkrow-dark.tdesktop-theme \
  ~/.local/share/coderkrow/coderkrow-dark.tdesktop-theme
```

### Option B — double-click / open with

With file associations set, double-clicking the `.tdesktop-theme` file
opens the "Apply theme?" dialog in Telegram.

### Reload

Telegram copies the palette on import. After editing the source file,
re-import it (Settings → Chat Settings → Theme → folder icon) to pick up
the change.

## Verify

After applying, confirm:

- Chrome and chat list render near-black `#111110`; message list and
  compose area use surface `#1a1a18`.
- Send button and unread badges are teal `#2e7f80`; links and sent ticks
  are teal-light `#3bb8ba`.
- Active toggle / selection accents read as cyan `#00d1d4`.
- Nothing is pure black or pure white, and no purple appears anywhere.

If the import fails, check every line ends with `;`, colors are `#rrggbb`
or `#rrggbbaa`, and referenced constants (e.g. `windowFg`) are defined
before use.

## Tweak

- Edit `telegram/theme/coderkrow-dark.tdesktop-theme`; keep hex
  lowercase. The `COLOR_*` block at the top is the single source of
  truth — change a token there and every reference follows.
- `windowBg` is the ground; `msgInBg` / `msgOutBg` are the bubbles.
  Lighten `msgOutBg` if outgoing bubbles need more separation from
  incoming.
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
