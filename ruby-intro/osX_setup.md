# HomeBrew

## Install Homebrew

	ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

 see http://www.sitepoint.com/up-and-running-with-rbenv/

If you don't have command line developer tools, install xcode, or select install when dialog "xcode-select" prompts for it.

	$ brew update
	$ brew install rbenv ruby-build

prepend ~/.rbenv/shims to your $PATH

	export RBENV_ROOT=${HOME}/.rbenv
	export PATH=~/.rbenv/shim:$PATH
	if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi

	source ~/.rbenv/completions/rbenv.zsh

or

	source ~/.rbenv/completions/rbenv.bash

mkdir -p $RBENV_ROOT/plugins
git clone https://github.com/rkh/rbenv-whatis.git $RBENV_ROOT/plugins/rbenv-whatis
git clone https://github.com/rkh/rbenv-use.git $RBENV_ROOT/plugins/rbenv-use

rbenv install 2.1.2

rbenv global 2.1.2
ruby -v

gem install bundler

rbenv rehash