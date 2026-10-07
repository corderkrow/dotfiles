# Releases

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Expanded `README.md` with install, usage, theming, contributing, and
  Code of Conduct sections.
- `CODE_OF_CONDUCT.md` (Contributor Covenant v2.1, contact:
  alvaro.farias@proton.me).
- `RELEASES.md` changelog scaffold.
- `coderkrow` theme for herdr (`herdr/config.toml`) with install notes
  (`herdr/INSTALL.md`): `theme.custom` token overrides, dark default plus
  optional light auto-switch.
- `coderkrow dark` theme for Telegram Desktop
  (`telegram/theme/coderkrow-dark.tdesktop-theme`) with install notes
  (`telegram/theme/INSTALL.md`): dark-only, teal selection and outgoing
  bubbles, cyan active states.

## [0.1.0] - 2026-09-23

### Added

- `coderkrow dark` theme for Zed (`zed/theme/coderkrow-dark.json`) with
  install notes.
- Starship powerline config (`starship/starship.toml`) with
  `coderkrow_dark` palette, git / runtime / container segments.
- Ghostty `coderkrow` theme (`ghostty/coderkrow`): dark background,
  16-color ANSI palette, JetBrains Mono default.
- COSMIC desktop theme (`cosmic/coderkrow-dark.ron`).
- opencode agent config (`opencode.json`) and `coderkrow` TUI theme
  (`opencode/themes/coderkrow.json`).
- Terminal dev stack reference (`terminal-dev-stack.md`): Ghostty,
  Oh My Zsh, zoxide, fzf, atuin.
- MIT License.

[Unreleased]: https://github.com/corderkrow/dotfiles/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/corderkrow/dotfiles/releases/tag/v0.1.0
