# coderkrow for Starship

Custom Starship prompt built from `.ai/rules/brand/RULES.md` — the same
`coderkrow` palette already used by Ghostty, Zed, opencode, herdr, and
COSMIC.

- ground `#111110` (never `#000`), text `#e8e6df` (never `#fff`)
- brand teal `#1a595a` / `#2e7f80` on powerline segments
- interactive accent `#3bb8ba`, signal cyan `#00d1d4` for info and
  active states only
- no purple, no gradients, flat surfaces

## How Starship themes work

Starship does **not** load theme files from a directory. The whole
prompt — format string plus named palettes — lives in a single config
file:

```
~/.config/starship.toml      # Linux / macOS
```

This repo ships `starship/starship.toml` with a `coderkrow_dark` palette
(plus a gruvbox fallback) and a powerline `format` using OS, user,
directory, git, language runtimes, Docker / Conda / Pixi, and time
segments.

Reference: <https://starship.rs/config/>

## Activate

`starship/starship.toml` in this repo is a complete Starship config
carrying the theme. Pick one of the two install styles below.

### Option A — symlink (recommended for dotfiles)

If you do not already have a Starship config:

```sh
mkdir -p ~/.config
ln -sf ~/dotfiles/starship/starship.toml ~/.config/starship.toml
```

### Option B — merge into an existing config

Copy the `format`, `palette`, and `[palettes.coderkrow_dark]` keys from
`starship/starship.toml` into your existing `~/.config/starship.toml`.
Do not duplicate tables that already exist — merge their keys. Then set:

```toml
palette = "coderkrow_dark"
```

### Reload

Starship renders on every prompt, so no reload step exists. Open a new
shell or re-source your init:

```sh
eval "$(starship init zsh)"
```

Make sure your `~/.zshrc` contains the init line (see repository
`README.md`).

## Verify

```sh
starship explain
starship print-config
```

`explain` breaks down the current prompt segment by segment;
`print-config` prints the effective config. A missing or misspelled
`palette` key falls back silently — confirm `palette =
'coderkrow_dark'` is set.

## Tweak

- Edit the tokens under `[palettes.coderkrow_dark]`, keep hex
  lowercase, then open a new prompt (no restart needed).
- Powerline glyphs (`  `) assume a Nerd Font — JetBrainsMono Nerd
  Font recommended.
- Keep the palette in sync with the other themes — see the repository
  `README.md` and `.ai/rules/brand/RULES.md`.
