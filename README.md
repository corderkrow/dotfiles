# ![dotfiles logo](./assets/foldercyanlinux_93146.svg) dotfiles

[![License: MIT](https://img.shields.io/github/license/corderkrow/dotfiles?style=for-the-badge)](./LICENSE)
[![Last commit](https://img.shields.io/github/last-commit/corderkrow/dotfiles?style=for-the-badge)](https://github.com/corderkrow/dotfiles/commits/main)
[![Issues](https://img.shields.io/github/issues/corderkrow/dotfiles?style=for-the-badge)](https://github.com/corderkrow/dotfiles/issues)
[![Pull Requests](https://img.shields.io/github/issues-pr/corderkrow/dotfiles?style=for-the-badge)](https://github.com/corderkrow/dotfiles/pulls)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg?style=for-the-badge)](./CODE_OF_CONDUCT.md)
[![OSS Lifecycle](https://img.shields.io/osslifecycle?file_url=https%3A%2F%2Fraw.githubusercontent.com%2Fcorderkrow%2Fdotfiles%2Fmain%2FOSSMETADATA&style=for-the-badge)](./OSSMETADATA)

Personal dotfiles with modern shell tooling, optimized for development.
Fast startup times, smart directory navigation, and modern CLI tools
plus a consistent `coderkrow` dark theme across terminal, prompt, editor,
and desktop.

Built for Pop!_OS / Linux. MIT licensed. Contributions welcome.

## Features

- **Fast startup:** minimal shell framework config, lazy-loaded tooling,
  no plugin bloat.
- **Smart navigation:** `zoxide` (frequency-aware `cd`), `fzf` (fuzzy
  file / directory / history search), `atuin` (syncable, searchable shell
  history).
- **Modern CLI stack:** Ghostty (GPU-accelerated terminal) + Zsh +
  Oh My Zsh + Starship prompt.
- **Consistent theme:** `coderkrow dark` palette (`#111110` / `#e8e6df` /
  `#1a595a` / `#00d1d4`) applied to Ghostty, Starship, Zed, opencode,
  herdr, COSMIC desktop, and Telegram Desktop.
- **Dev-ready prompt:** Starship powerline with OS, user, directory,
  git branch/status, language runtimes (C, C++, Rust, Go, Node, PHP,
  Java, Kotlin, Haskell, Python), Docker / Conda / Pixi contexts, and time.

## Repository layout

```text
.
├── cosmic/                  # COSMIC desktop theme (coderkrow-dark.ron + INSTALL.md)
├── ghostty/
│   ├── coderkrow             # Ghostty theme + font / window defaults
│   └── INSTALL.md            # Ghostty install notes
├── herdr/
│   ├── config.toml          # herdr custom theme (coderkrow)
│   └── INSTALL.md           # herdr install notes
├── starship/
│   ├── starship.toml         # Starship powerline prompt (coderkrow_dark palette)
│   └── INSTALL.md            # Starship install notes
├── zed/
│   └── theme/
│       ├── coderkrow-dark.json  # Zed theme (dark-only)
│       └── INSTALL.md           # Zed install notes
├── opencode/
│   ├── themes/
│   │   └── coderkrow.json    # opencode TUI theme
│   └── INSTALL.md            # opencode install notes
├── telegram/
│   └── theme/
│       ├── coderkrow-dark.tdesktop-theme  # Telegram Desktop theme (dark-only)
│       └── INSTALL.md                     # Telegram install notes
├── opencode.json             # opencode agent config / permissions
├── terminal-dev-stack.md     # Full terminal stack reference (Ghostty, OMZ, zoxide, fzf, atuin)
├── CODE_OF_CONDUCT.md        # Contributor Covenant v2.1
├── CONTRIBUTING.md           # Contribution guidelines
├── RELEASES.md               # Changelog (Keep a Changelog + SemVer)
└── LICENSE                   # MIT
```

See [`terminal-dev-stack.md`](./terminal-dev-stack.md) for the complete
terminal configuration reference.

## Requirements

- Linux (developed on Pop!_OS)
- `zsh`, `git`, `curl`
- [Ghostty](https://ghostty.org/) terminal
- [Oh My Zsh](https://ohmyz.sh/)
- [Starship](https://starship.rs/)
- [zoxide](https://github.com/ajeetdsouza/zoxide)
- [fzf](https://github.com/junegunn/fzf)
- [atuin](https://atuin.sh/) (optional, for synced history)
- [Zed](https://zed.dev/) (optional, for editor theme)
- [herdr](https://herdr.dev/) (optional, for terminal workspace theme)
- [Telegram Desktop](https://desktop.telegram.org/) (optional, for chat theme)
- Nerd Font (recommended: JetBrainsMono Nerd Font)

## Quick start

1. Clone:

   ```sh
   git clone https://github.com/corderkrow/dotfiles.git ~/dotfiles
   cd ~/dotfiles
   ```

2. Install shell tooling (Debian/Ubuntu/Pop!_OS):

   ```sh
   sudo apt update
   sudo apt install -y zsh git curl fzf
   chsh -s "$(command -v zsh)"
   ```

   ```sh
   # Oh My Zsh
   sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

   # Starship
   curl -sS https://starship.rs/install.sh | sh -s -- -y

   # zoxide
   curl -sS https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | bash

   # atuin (optional)
   curl --proto '=https' --tlsv1.2 -LsSf https://setup.atuin.sh | sh
   ```

3. Link configs:

   ```sh
   # Starship
   mkdir -p ~/.config
   ln -sf ~/dotfiles/starship/starship.toml ~/.config/starship.toml

   # Ghostty — coderkrow theme
   mkdir -p ~/.config/ghostty
   cp ~/dotfiles/ghostty/coderkrow ~/.config/ghostty/themes/coderkrow
   # then set `theme = coderkrow` in ~/.config/ghostty/config

   # Zed theme
   mkdir -p ~/.config/zed/themes
   cp ~/dotfiles/zed/theme/coderkrow-dark.json ~/.config/zed/themes/
   # Zed: theme selector → `coderkrow dark`

   # herdr theme
   mkdir -p ~/.config/herdr
   ln -sf ~/dotfiles/herdr/config.toml ~/.config/herdr/config.toml
   # see herdr/INSTALL.md; then: herdr server reload-config

   # COSMIC theme
   # Import cosmic/coderkrow-dark.ron via COSMIC Settings → Appearance,
   # or copy to your COSMIC themes directory.

   # Telegram Desktop theme
   # Settings → Chat Settings → Theme → folder icon → import
   # telegram/theme/coderkrow-dark.tdesktop-theme
   ```

4. Enable shell integrations in `~/.zshrc`:

   ```sh
   eval "$(starship init zsh)"
   eval "$(zoxide init zsh)"
   eval "$(atuin init zsh)"
   [ -f ~/.fzf.zsh ] && source ~/.fzf.zsh

   export FZF_DEFAULT_OPTS="--height 40% --layout=reverse --border"
   ```

## Usage

| Tool | Purpose | Key commands |
| ---- | ------- | ------------ |
| `z` (zoxide) | Smart `cd` | `z proyecto`, `z ..`, `zi` (interactive) |
| `fzf` | Fuzzy finder | `Ctrl+T` files, `Alt+C` dirs, `Ctrl+R` history |
| `atuin` | History search/sync | `Ctrl+R`, `atuin login`, `atuin sync` |
| Starship | Prompt | Git + runtime segments render automatically |

Stack order: `Ghostty → Zsh → atuin → fzf → zoxide`, with Starship
rendering the prompt.

## Theming

All themes share one palette — dark background `#111110`, surface
`#1a1a18`, foreground `#e8e6df`, teal accents `#1a595a` / `#2e7f80` /
`#3bb8ba` / `#00d1d4`:

- **Ghostty:** `ghostty/coderkrow` — 16-color ANSI palette, cyan cursor,
  teal selection.
- **Starship:** `starship/starship.toml` — `coderkrow_dark` palette with
  gruvbox fallback, powerline glyphs.
- **Zed:** `zed/theme/coderkrow-dark.json` — dark-only, flat borders,
  cyan keywords, teal strings, italic muted comments.
- **opencode:** `opencode/themes/coderkrow.json` — matching TUI theme.
- **herdr:** `herdr/config.toml` — `theme.custom` token overrides on a
  built-in base; dark-only with an optional light auto-switch. See
  `herdr/INSTALL.md`.
- **COSMIC:** `cosmic/coderkrow-dark.ron` — desktop theme.
- **Telegram Desktop:** `telegram/theme/coderkrow-dark.tdesktop-theme` —
  dark-only palette, teal selection and outgoing bubbles, cyan active
  states, flat surfaces. See `telegram/theme/INSTALL.md`.

To tweak: edit the palette in one theme file, mirror hex values across
the others, keep contrast for long sessions.

## Contributing

Issues and PRs welcome. Please read [`CONTRIBUTING.md`](./CONTRIBUTING.md)
for workflow, style, and testing notes.

Please also read [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md). Report
unacceptable behavior to alvaro.farias@proton.me.

## Releases

Changelog lives in [`RELEASES.md`](./RELEASES.md). Format based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), versioning
follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## License

MIT — see [`LICENSE`](./LICENSE). Copyright (c) 2026 coderkrow.
