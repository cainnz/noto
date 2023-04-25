## .zshrc_configs

## clean_global_config
*config that can be used globally, but first you need to install __antigen > [installation](https://github.com/zsh-users/antigen) and typewritten > [installation](https://typewritten.dev/#/installation)__*

```bash
# custom options for typewritten, Global Setting
# custom options for typewritten, Global Setting

export TYPEWRITTEN_PROMPT_LAYOUT="pure"
export TYPEWRITTEN_COLOR_MAPPINGS="primary:white;secondary:white"
export TYPEWRITTEN_COLORS="arrow:white;symbol:white"
export TYPEWRITTEN_SYMBOL=""
export TYPEWRITTEN_ARROW_SYMBOL=""
export TYPEWRITTEN_CURSOR="underscore"

# Aliasses
alias alaconfig="nvim ~/.config/alacritty/alacritty.yml"
alias zshconfig="nvim ~/.zshrc"
alias kittyconfig="nvim ~/.config/kitty/kitty.conf"
alias tmuxconfig="nvim ~/.tmux.conf"
alias nvimconfig="nvim ~/.config/nvim/init.vim"
alias rangerconfig="nvim ~/.config/ranger/rc.conf"
alias nvimplugin="nvim ~/.config/nvim/vim-plug/plugins.vim"
alias luaconfig="nvim ~/.config/nvim/lua/caiinz/init.lua"

source ~/antigen.zsh

# load the oh-my-zsh's library
antigen use oh-my-zsh

# Bundles from the default repo (robbyrussell's oh-my-zsh)
antigen bundle command-not-found
antigen bundle z
antigen bundle colored-man-pages
antigen bundle zsh-users/zsh-completions
antigen bundle zsh-users/zsh-syntax-highlighting
antigen bundle zsh-users/zsh-autosuggestions

# tells antigen that you are done
antigen apply

# sets typewritten as default, GLOBAL Setting
fpath+=$HOME/.zsh/typewritten
autoload -U promptinit; promptinit
prompt typewritten

# Useful aliasses with exa and icons
# Note: if using WSL2 Place these alisses all the way at the end!
alias la="exa --long --header --icons -a -l"
alias ls="exa --long --header --icons -a"
alias vi="nvim"
alias cat="bat"
alias lg="lazygit"
```

## tmux_global_config

***Before using it, you need to install tmux tpm*** [Installation](https://github.com/tmux-plugins/tpm) or just run:
```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

## then, copy the official .tmux.conf to ~/
***Note: on WSL config text needs to be copy from one place to the other, windows sucks I know***
- Open tmux
- Press ***Ctrl + I*** the "**I**" is CAPITILIZED!



