# Terminal Dev Stack (Pop!_OS)

Stack de terminal para desarrollo:

- Ghostty (terminal emulator)
- Oh My Zsh (shell framework)
- zoxide (smart cd)
- fzf (fuzzy finder)
- atuin (history manager)

---

# Ghostty

Terminal emulator moderno con aceleración por GPU.

Config:

~/.config/ghostty/config

font-family = "JetBrainsMono Nerd Font"
font-size = 13

theme = GruvboxDarkHard

window-padding-x = 10
window-padding-y = 10

background-opacity = 0.95

cursor-style = block
cursor-style-blink = true

scrollback-limit = 10000000

copy-on-select = true
gtk-titlebar = false

---

# Oh My Zsh

Framework para Zsh.

Config:

~/.zshrc

ZSH_THEME="robbyrussell"

plugins=(
  git
  docker
  sudo
)

source $ZSH/oh-my-zsh.sh

---

# zoxide

Reemplazo moderno de cd.

Config:

eval "$(zoxide init zsh)"
alias cd="z"

Uso:

z proyecto
z ..

---

# fzf

Fuzzy finder para terminal.

Config:

[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh

export FZF_DEFAULT_OPTS="--height 40% --layout=reverse --border"

Atajos:

Ctrl + R (historial)
Ctrl + T (archivos)
Alt + C (directorios)

---

# atuin

Historial avanzado de shell.

Config:

eval "$(atuin init zsh)"

Opcional:

atuin login
atuin sync

Uso:

Ctrl + R

---

# Stack

Ghostty → Zsh → atuin → fzf → zoxide
