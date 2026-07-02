# dotfiles

Ghostty + zsh (oh-my-zsh, powerlevel10k) config, managed with GNU stow.

## Layout

```
ghostty/   -> ~/.config/ghostty/  (config, tab-style.css, themes/)
zsh/       -> ~/.zshrc, ~/.p10k.zsh
```

## New machine setup

```bash
# 1. dependencies
sudo dnf/apt install zsh eza fzf stow git

# 2. oh-my-zsh + theme + plugins
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
git clone https://github.com/Aloxaf/fzf-tab ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fzf-tab
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# 3. remove files the OMZ installer created, then stow
rm -f ~/.zshrc
git clone git@github.com:radipleven/dotfiles.git ~/dotfiles
cd ~/dotfiles && stow ghostty zsh

# 4. default shell
chsh -s $(which zsh)
```

Fonts: none needed - ghostty has JetBrains Mono with nerd font symbols.

Neovim config is separate: `git clone git@github.com:radipleven/nvim-config.git ~/.config/nvim`

## Machine-local config

Anything sensitive or machine-specific (work URLs, tokens, cluster helpers)
goes in `~/.zshrc.local` — untracked, sourced at the end of `.zshrc`.
Never commit company info here.

## Stow cheatsheet

```bash
cd ~/dotfiles
stow <pkg>      # link
stow -D <pkg>   # unlink
stow -R <pkg>   # relink after moving files
```
