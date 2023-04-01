## .zshrc_configs

## clean_global_config
*config that can be used globally, but first you need to install __antigen > [installation](https://github.com/zsh-users/antigen) and typewritten > [installation](https://typewritten.dev/#/installation)__*

```bash
# custom options for typewritten, Global Setting
export TYPEWRITTEN_PROMPT_LAYOUT="pure"
export TYPEWRITTEN_COLOR_MAPPINGS="primary:white;secondary:white"
export TYPEWRITTEN_COLORS="arrow:white;symbol:white"
export TYPEWRITTEN_SYMBOL=""
export TYPEWRITTEN_ARROW_SYMBOL=""
export TYPEWRITTEN_CURSOR="underscore"

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
```

## tmux_global_config

***before using it, you need to install tmux tpm*** [Installation](https://github.com/tmux-plugins/tpm) or just run:
```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```