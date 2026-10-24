# Contributing to dotfiles

Thank you for considering a contribution. This project follows the
[Contributor Covenant](https://www.contributor-covenant.org/) code of conduct.
By participating, you agree to uphold it.

Please read [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md) before contributing.
Report unacceptable behavior to alvaro.farias@proton.me.

## How to contribute

### Report issues

1. Check existing [issues](https://github.com/corderkrow/dotfiles/issues) for duplicates.
2. Open a new issue with:
   - What you expected vs. what happened.
   - Steps to reproduce, OS / shell / tool versions.
   - Relevant config snippet or screenshot (redact secrets).

### Submit changes

1. Fork the repo and branch from `main`:
   ```sh
   git clone https://github.com/<you>/dotfiles.git
   cd dotfiles
   git checkout -b feat/my-change
   ```
2. Keep changes small and scoped — one theme, one tool, one fix per PR.
3. Test configs locally before pushing (see below).
4. Update `RELEASES.md` under `Unreleased` when behavior changes.
5. Push and open a pull request against `main` with:
   - What changed and why.
   - Test evidence (commands run, terminal/editor screenshots for theme changes).
   - Linked issue number, if any.

## Local testing

Dotfiles have no test suite; verification is manual:

- Shell / prompt: symlink or copy the changed file, reload (`source ~/.zshrc`),
  confirm startup time and prompt segments.
- Ghostty: install `ghostty/coderkrow.conf` (dark) or
  `ghostty/coderkrow-light.conf` (light) as
  `~/.config/ghostty/themes/coderkrow` / `.../coderkrow-light` (drop the
  extension — the installed name is the theme name), set `theme = coderkrow` /
  `theme = coderkrow-light`, restart Ghostty; `ghostty +validate-config
  --config-file=ghostty/coderkrow-light.conf` validates the file.
- Starship: `ln -sf ~/dotfiles/starship/starship.toml ~/.config/starship.toml`,
  open a git repo and check segments.
- Zed: copy `zed/theme/coderkrow-dark.json` and
  `zed/theme/coderkrow-light.json` to `~/.config/zed/themes/`, then select
  `coderkrow dark` or `coderkrow light` in Zed.
- herdr: `ln -sf ~/dotfiles/herdr/config.toml ~/.config/herdr/config.toml`
  (dark) or `ln -sf ~/dotfiles/herdr/config-light.toml
  ~/.config/herdr/config.toml` (light), then
  `herdr server reload-config`; `herdr config check` validates the
  result (see `herdr/INSTALL.md`).
- COSMIC: import `cosmic/coderkrow-dark.ron` via Settings → Appearance.

Do not commit secrets, tokens, machine-specific paths, or history files.

## Style guide

- Match the `coderkrow dark` palette: background `#111110`, surface
  `#1a1a18`, foreground `#e8e6df`, teal accents `#1a595a` / `#2e7f80` /
  `#3bb8ba` / `#00d1d4`. The light variant uses ground `#f5f4f0`, surface
  `#faf9f6`, ink `#1d1d1b`, the same teals, and deep teal `#1a595a` for
  code that would be cyan in dark.
- Flat theme style only: no gradients, no extra accent colors.
- Mirror palette changes across Ghostty, Starship, Zed, opencode, herdr,
  and COSMIC where applicable.
- Keep shell configs fast: lazy-load tooling, no plugin bloat.
- Follow existing per-directory `INSTALL.md` format for docs.

## Commit and PR conventions

- Clear, scoped messages: `feat(ghostty): ...`, `fix(starship): ...`,
  `docs: ...`.
- One logical change per commit.
- PRs should pass a clean `git diff --check` (no whitespace errors).

## Releases

Changelog lives in [`RELEASES.md`](./RELEASES.md), based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versioning follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Attribution

Contribution process inspired by the
[Contributor Covenant](https://www.contributor-covenant.org/) philosophy:
explicit shared values, welcoming participation, and fair enforcement
per `CODE_OF_CONDUCT.md`.
