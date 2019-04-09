# appaquet's dotfiles
New version of my old [dotfiles](https://github.com/appaquet/app-vim)

## Shell & editor setup
* Checkout this repo recursively in your ~/
  * `git clone --recursive https://github.com/appaquet/dotfiles.git` ~/dotfiles

* Fish shell
  * To install
    * Ubuntu: `sudo apt install fish`
    * MacOS: `brew install fish` and follow instructions about adding fish to `/etc/shells`
  * Change your shell
    * Ubuntu: `chsh -s /usr/bin/fish`
    * MacOS: `chsh -s /usr/local/bin/fish`
  * Symlink fish's config folder: `mkdir -p ~/.config/fish/ && ln -s ~/dotfiles/fish/config.fish ~/.config/fish/`
  * Log out and log back (you'll get errors as not everyhing is setup yet)
  * Install oh-my-fish framework
    * `curl -L https://get.oh-my.fish | fish`
  * Install plugins & themes
    * `foreign-env` / `fenv` to import ~/.profile variables: `omf install foreign-env`
    * `bobthefish` theme: `omf install bobthefish` and then `omf theme bobthefish`

  * **Notes**
    * You can still use your `~/.profile` as you would do in bash thanks to the `foreign-env` plugin that sources your `~/.profile`
    * You can put any local specifc fish config in `~/.config/fish/local.fish`

* [fzf](https://github.com/junegunn/fzf) (shell fuzzy shell history finder & fuzzy file finder)
  * To install
    * `cd ./fzf && ./install`

* Neovim
   * To install, see https://github.com/neovim/neovim/wiki/Installing-Neovim
     * Make sure to update alternatives on Ubuntu
     * On MacOS, you may need to install [python neovim](https://ricostacruz.com/til/neovim-with-python-on-osx): `pip3 install neovim --upgrade`
   * Symlink config folder: `ln -s ~/dotfiles/nvim ~/.config/nvim`
   * Install plugins `nvim +BundleInstall +qall`
   * Finish YouCompleteMe plugin installation
     * `cd /home/appaquet/.vim/bundle/YouCompleteMe`
     * `./install.py`

* Tmux
   * Symlink tmux conf: `ln -s ~/dotfiles/tmux/tmux.conf ~/.tmux.conf`
   * Create empty local conf: `touch ~/.tmux.conf.local`

  * **Notes**
    * You can put any local specifc fish config in `~/.tmux.conf.local`

* [Autojump](https://github.com/wting/autojump) (Fast jumping to directories)
  * To install
    * Ubuntu: `sudo apt install autojump`
    * MacOS: `brew install autojump`
  * You can add the bootstrap script to your `~/.config/fish/local.fish`
    * MacOS: `[ -f /usr/local/share/autojump/autojump.fish ]; and source /usr/local/share/autojump/autojump.fish`
    * Ubuntu: `[ -f /usr/share/autojump/autojump.fish ]; and source /usr/share/autojump/autojump.fish`

* [RipGrep](https://github.com/BurntSushi/ripgrep) (A very fast grep / ack replacement)
  * To install
    * Ubuntu: `sudo apt install ripgrep`
    * MacOS: `snap install --classic ripgrep`

* [Alacritty](https://github.com/jwilm/alacritty) (A GPU accelared terminal written in Rust)
  * Main advantage of Alacritty is it's cross platform and configurable via a configuration file
  * To install:
    * Follow instructions on GitHub
    * Install patched fonts
      * `git clone https://github.com/powerline/fonts`
      * `cd fonts; ./install.sh`
    * Symlink config folder: `mkdir -p ~/.config/alacritty/; ln -s ~/dotfiles/alacritty/alacritty.yml ~/.config/alacritty/alacritty.yml`

## Languages setup
* [Rust](rust.md)

## Usage
### Neovim
* My leader key is bound to `\` (backslash)

* Useful custom commands
  * `E` or `New` to create a new file in the directory as the current buffer's file
  * `Delete` delete the file in current buffer without messing up vim's layout
  * `Rename` rename the current file and correctly replace current buffer with new file
  * `Ack` launches ack in a split buffer

* Useful custom mappings
  * `<leader> 1 through 9 ` to switch between opened buffers
  * `<leader>]` to switch to next buffer
  * `<leader>[` to switch to previous buffer
  * `<leader>w` to save current buffer
  * `<leader>x` to save and then execute current buffer (as long as it's chmod +x)
  * `<leader>r` to save current buffer and then execute `rsync.sh` in working dir
  * `<leader>q` to close the current buffer (equivalent to `:q`)
  * `<leader>w` to close the current buffer by trying not to messup the layout
  * `<leader><tab>` to switch between tab and spaces
  * `<ctrl>e` or `<leader>e` to toggle Nerdtree (files)
  * `<leader>d` if YouCompleteMe is available, go to definition
  * `<ctrl>p` fuzzy finding file
  * `<ctrl>a` fuzzy find the current word in files using ack
  * `<leader> m` to toggle mouse support (useful to allow select + copy)

* You can check [`init.vim`](nvim/init.vim) for more commands / mappings

### fzf (in shel)
* In shell
  * `<ctrl>t` for fuzzy file find
  * `<ctrl>r` for fuzzy history find

### tmux
* `<ctrl>b e` to turn on synchronized panes
* `<ctrl>b E` to turn off synchronized panes
* `<ctrl>b m` to toggle mouse support (useful to allow select + copy)

### Autojump
* In shell
  * `j somefolder` to jump to a folder that contains somefolder that you cd'ed to previously
  * `jc somefolder` to jump to a child folder
  * `jo [folder]` to jump to a folder using the system's file manager

### Ripgrep
* In shell
  * `rg <pattern>` to find any files that contain the given pattern
* In vim
  * `Rg <pattern>` to ripgrep the given pattern
  * `<leader>r` to ripgrep the current word

## TODO
- [ ] RVM, NVM and Python
- [ ] https://nerdfonts.com/
- [ ] Git config
  - https://git-scm.com/docs/git-rerere
  - Track
  push.default=current
  rerere.enabled=true
- [ ] Standardize colors to https://github.com/chriskempson/base16
  - https://github.com/chriskempson/base16-shell
  - https://github.com/chriskempson/base16-shell/issues/162
