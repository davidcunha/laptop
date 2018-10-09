[<img width="110" src="https://avatars3.githubusercontent.com/u/38539999?s=200&v=4g" />](https://picuscreative.com)

# Laptop

Laptop is a script to set up an macOS laptop for web and mobile development based on [Thoughbot](https://thoughtbot.com/) [laptop project](https://github/thoughtbot/laptop).

It can be run multiple times on the same machine safely.
It installs, upgrades, or skips packages
based on what is already installed on the machine.

## Requirements

We support:

- macOS Mavericks (10.9)
- macOS Yosemite (10.10)
- macOS El Capitan (10.11)
- macOS Sierra (10.12)

Older versions may work but aren't regularly tested.
Bug reports for older versions are welcome.

## Install

Download the script:

```sh
curl --remote-name https://raw.githubusercontent.com/picuscreative/laptop/master/mac
```

Review the script (avoid running scripts you haven't read!):

```sh
less mac
```

Execute the downloaded script:

```sh
sh mac 2>&1 | tee ~/laptop.log
```

Optionally, review the log:

```sh
less ~/laptop.log
```

## Debugging

Your last Laptop run will be saved to `~/laptop.log`.
Read through it to see if you can debug the issue yourself.
If not, copy the lines where the script failed into a
[new GitHub Issue](https://github.com/picuscreative/laptop/issues/new) for us.
Or, attach the whole log file as an attachment.

## What it sets up

macOS tools:

- [Homebrew] for managing operating system libraries.

[homebrew]: http://brew.sh/

Unix tools:

- [Exuberant Ctags] for indexing files for vim tab completion
- [Git] for version control
- [OpenSSL] for Transport Layer Security (TLS)
- [RCM] for managing company and personal dotfiles
- [The Silver Searcher] for finding things in files
- [Tmux] for saving project state and switching between projects
- [Watchman] for watching for filesystem events
- [Zsh] as your shell
- [Oh My Zsh] will not make you a 10x developer...but you might feel like one.

[exuberant ctags]: http://ctags.sourceforge.net/
[git]: https://git-scm.com/
[openssl]: https://www.openssl.org/
[rcm]: https://github.com/thoughtbot/rcm
[the silver searcher]: https://github.com/ggreer/the_silver_searcher
[tmux]: http://tmux.github.io/
[watchman]: https://facebook.github.io/watchman/
[zsh]: http://www.zsh.org/
[oh my zsh]: http://ohmyz.sh/

Image tools:

- [ImageMagick] for cropping and resizing images

Programming languages, tools, package managers, and configuration:

- [ASDF] for managing programming language versions
- [Bundler] for managing Ruby libraries
- [Node.js] and [NPM], for running apps and installing JavaScript packages
- [Ruby] stable for writing general-purpose code
- [Vagrant] for development virtual machines
- [Varying Vagrant Vagrants] for Wordpress development with Vagrant

[bundler]: http://bundler.io/
[imagemagick]: http://www.imagemagick.org/
[node.js]: http://nodejs.org/
[npm]: https://www.npmjs.org/
[asdf]: https://github.com/asdf-vm/asdf
[ruby]: https://www.ruby-lang.org/en/
[vagrant]: https://www.vagrantup.com/
[varying vagrant vagrants]: https://varyingvagrantvagrants.org/

Day to day dependencies:

- Visual Studio Code
- Google Chrome
- Google Backup and Sync
- Gyazo
- Filezilla
- Firefox
- Iterm2
- Postman
- SequelPro
- Skype
- Slack
- SourceTree
- Spectacle
- Toggl
- VirtualBox

It should take less than 30 minutes to install (depends on your machine and network conditions).

## Customize in `~/.laptop.local`

Your `~/.laptop.local` is run at the end of the Laptop script.
Put your customizations there.
For example:

```sh
#!/bin/sh

brew bundle --file=- <<EOF
brew "Caskroom/cask/dockertoolbox"
brew "go"
brew "ngrok"
brew "watch"
EOF

default_docker_machine() {
  docker-machine ls | grep -Fq "default"
}

if ! default_docker_machine; then
  docker-machine create --driver virtualbox default
fi

default_docker_machine_running() {
  default_docker_machine | grep -Fq "Running"
}

if ! default_docker_machine_running; then
  docker-machine start default
fi

fancy_echo "Cleaning up old Homebrew formulae ..."
brew cleanup
brew cask cleanup

if [ -r "$HOME/.rcrc" ]; then
  fancy_echo "Updating dotfiles ..."
  rcup
fi
```

Write your customizations such that they can be run safely more than once.
See the `mac` script for examples.

Laptop functions such as `fancy_echo` and
`gem_install_or_update`
can be used in your `~/.laptop.local`.

See the [wiki](https://github.com/thoughtbot/laptop/wiki)
for more customization examples.

## Contributing

Edit the `mac` file.
Document in the `README.md` file.
Follow shell style guidelines by using [ShellCheck] and [Syntastic].

```sh
brew install shellcheck
```

[shellcheck]: http://www.shellcheck.net/about.html
[syntastic]: https://github.com/scrooloose/syntastic

Thank you [Thoughbot](https://thoughtbot.com/) and [contributors!](https://github.com/picuscreative/laptop/graphs/contributors)

## License

[MIT License](https://opensource.org/licenses/MIT) - [PICUS](https://picuscreative.com)
