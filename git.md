# Git
## git install for Mac
	brew install git
	brew install zsh
	sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

## ZSH_THEME
	open ~/.zshrc
add in file -> ZSH_THEME="agnoster"  
add in file -> prompt_context () { }

	cd ~/Downloads/
	git clone https://github.com/powerline/fonts.git
	cd fonts
	./install.sh
	
iTerm2 — Preferences, далее Profiles — Text и в поле Font выберите скачанный шрифт: Meslo LG или Droid Sans

## ssh keys
### check ssh keys
	ls -al ~/.ssh

### create ssh-key
	ssh-keygen -t ed25519  -C "your_email@example.com"

### starting the ssh agent
	eval "$(ssh-agent -s)"

### add ssh-key
	ssh-add ~/.ssh/id_ed25519

### copy ssh key
	pbcopy < ~/.ssh/id_ed25519.pub

## config --system --global --local
	git config --list --show-origin

### login & email
	git config --global user.name "name"
	git config --global user.email "email"

### .gitignore_global
	git config --global core.excludesfile ~/.gitignore_global

### core.editor
	git config --global core.editor "vim --nofork"
	git config --global core.editor "code --wait"
	git config --global core.editor /Applications/Xcode.app/Contents/MacOS/Xcode

### alias
	git config --global alias.co checkout
	git config --global alias.br branch
	git config --global alias.ci commit
	git config --global alias.st status
	git config --global alias.visual '!gitk'
	
	git config alias.sdiff '!'"git diff && git submodule foreach 'git diff'"
	git config alias.spush 'push --recurse-submodules=on-demand'
	git config alias.supdate 'submodule update --remote --merge'

### rerere
	git config --global rerere.enabled true

### rebase
	git config pull.rebase false ## merge

### submodule
	git config --global diff.submodule log
	git config push.recurseSubmodules check
	git config push.recurseSubmodules on-demand
	git config --global submodule.recurse true

### commit.template
	git config --global commit.template ~/.gitmessage.txt

### autocrlf
	git config --global core.autocrlf input
