#Linux/Dotfiles
#Public/Notta
## Clean .zshrc

> [!Info] This config can be used globally
> Alisseses can be commented out, or set up manually

```bash
# Created by newuser for 5.8.1
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

#Linux/Tmux
## Tmux

> [!Info] Config can be used globally
>It sets several fundamental settings, and vim like pane selection

```bash
set -g default-terminal "screen-256color"
set -ga terminal-overrides ",xterm-256color*:Tc"
#set -g default-terminal "tmux-256color"
#set -ga terminal-overrides ",*256col*:Tc"
set -g prefix2 C-a												# Secondary prefix

unbind-key C-b														# free the original bind-key key
set-option -g prefix C-a									# setting the prefix from C-b to C-a
bind-key C-a send-prefix

set-option -g base-index 1								# window index will start with 1
set-window-option -g pane-base-index 1 		# pane index will start with 1
set-option -g renumber-windows on

bind-key | split-window -h -c "#{pane_current_path}" # allows you to open new pane with current path
bind-key _ split-window -v -c "#{pane_current_path}"

# nvim like movement
bind-key -r h select-pane -L              # go left
bind-key -r j select-pane -D              # go down
bind-key -r l select-pane -R              # go right
bind-key -r k select-pane -U              # go up

# kill pane without asking me to kill it!
unbind-key x               								# unbind-key “x” from it’s current job of “ask and then close”
bind-key x kill-pane       								# rebind-key it to just “close”
bind-key X kill-session                   # key combo for killing the entire session - <prefix> + shift + x

# Window: Movements
bind-key L last-window
bind-key -r C-h select-window -t :-       # cycle through the windows for quick window selection
bind-key -r C-l select-window -t :+

# The default key binding are Ctr+ Up/Down/Left/Right for one row movements , Alt + Up/Down/Left/Right for five row movements.
# Let's add one more to the set (Vim way)
# Vim Style
bind-key -r H resize-pane -L 2            # resize a pane two rows at a time.
bind-key -r J resize-pane -D 2
bind-key -r K resize-pane -U 2
bind-key -r L resize-pane -R 2

# these settings are added for testing porpuses they were taken from the github-nvim-theme
# Undercurl
set -g default-terminal "${TERM}"
set -as terminal-overrides ',*:Smulx=\E[4::%p1%dm'  # undercurl support
set -as terminal-overrides ',*:Setulc=\E[58::2::%p1%{65536}%/%d::%p1%{256}%/%{255}%&%d::%p1%{255}%&%d%;m'  # underscore colours - needs tmux-3.0

# toggle mouse
set -g mouse on
```

#Linux/Tmux 

> [!Info] Personal config
> It needs a few extra steps to be taken in order for it to work, ex. Install Tmux TPM

```bash
set -g default-terminal "screen-256color"
set -ga terminal-overrides ",xterm-256color*:Tc"
#set -g default-terminal "tmux-256color"
#set -ga terminal-overrides ",*256col*:Tc"
set -g prefix2 C-a												# Secondary prefix

unbind-key C-b														# free the original bind-key key
set-option -g prefix C-a									# setting the prefix from C-b to C-a
bind-key C-a send-prefix

set-option -g base-index 1								# window index will start with 1
set-window-option -g pane-base-index 1 		# pane index will start with 1
set-option -g renumber-windows on

bind-key | split-window -h -c "#{pane_current_path}" # allows you to open new pane with current path
bind-key _ split-window -v -c "#{pane_current_path}"

# nvim like movement
bind-key -r h select-pane -L              # go left
bind-key -r j select-pane -D              # go down
bind-key -r l select-pane -R              # go right
bind-key -r k select-pane -U              # go up

# kill pane without asking me to kill it!
unbind-key x               								# unbind-key “x” from it’s current job of “ask and then close”
bind-key x kill-pane       								# rebind-key it to just “close”
bind-key X kill-session                   # key combo for killing the entire session - <prefix> + shift + x

# Window: Movements
bind-key L last-window
bind-key -r C-h select-window -t :-       # cycle through the windows for quick window selection
bind-key -r C-l select-window -t :+

# The default key binding are Ctr+ Up/Down/Left/Right for one row movements , Alt + Up/Down/Left/Right for five row movements.
# Let's add one more to the set (Vim way)
# Vim Style
bind-key -r H resize-pane -L 2            # resize a pane two rows at a time.
bind-key -r J resize-pane -D 2
bind-key -r K resize-pane -U 2
bind-key -r L resize-pane -R 2

# these settings are added for testing porpuses they were taken from the github-nvim-theme
# Undercurl
set -g default-terminal "${TERM}"
set -as terminal-overrides ',*:Smulx=\E[4::%p1%dm'  # undercurl support
set -as terminal-overrides ',*:Setulc=\E[58::2::%p1%{65536}%/%d::%p1%{256}%/%{255}%&%d::%p1%{255}%&%d%;m'  # underscore colours - needs tmux-3.0

# toggle mouse
set -g mouse on

# tpm plugins
#set -g @plugin 'egel/tmux-gruvbox'
#set -g @tmux-gruvbox 'dark' # or 'light'
set -g @plugin 'tmux-plugins/tmux-yank'
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'wfxr/tmux-fzf-url'
#set -g @plugin "arcticicestudio/nord-tmux"
#set -g @plugin 'odedlaz/tmux-onedark-theme'
#set -g @plugin 'jimeh/tmux-themepack'
set -g @plugin 'srcery-colors/srcery-tmux'

# this plugin is pretty cool but it does not work without Powerline fonts
#set -g @plugin 'Determinant/tmux-colortag'
#TMUX_COLORTAG_USE_POWERLINE=yes

# sets specific tmux theme
#set -g @themepack 'powerline/default/green'

set -g @plugin 'tmux-plugins/tmux-prefix-highlight'
set -g @plugin 'tmux-plugins/tmux-net-speed'
#set -g @plugin 'samoshkin/tmux-plugin-sysstat' # `sysstat_ntemp` and `sysstat_itemp` are temperatures of nvidia card and intel card, these scripts are available in my fork: https://github.com/sainnhe/tmux-plugin-sysstat

#source ~/.config/tmux/themes/Catppuccin.conf
#source ~/.config/tmux/themes/sonokai-shusia.tmux.conf
#source ~/.config/tmux/themes/nightfox.conf


# Initialize TMUX plugin manager (keep this line at the very bottom of the tmux.conf"
run '~/.tmux/plugins/tpm/tpm'
```
