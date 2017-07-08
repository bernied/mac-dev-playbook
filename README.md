# Mac Development Ansible Playbook

This repository includes an Ansible Playbook used to setup a Mac Development environment. It is forked from [Geerlingguy's github playbook](https://github.com/geerlingguy/mac-dev-playbook).

This playbook installs and configures most of the software I use on my Mac for web and software development.

## Installation

  1. [Install Ansible](http://docs.ansible.com/ansible/intro_installation.html#latest-releases-on-mac-osx).
  2. Ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer).
  3. Clone this repository to your local drive (`git clone https://github.com/bernied/mac-dev-playbook.git`).
  4. Change into the `mac-dev-playbook` directory (`cd mac-dev-playbook`).
  5. Run `$ ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles.
  6. Run `ansible-playbook main.yml -i inventory -K` inside this directory. Enter your account password when prompted.
  7. Hit return when prompted for `Enter Mac Store email?` and `Enter Mac Store password?`.
  8. You may have to hit `Ok` in a Java installation dialog box and Enter your user/password for your github account.

> Note: If some Homebrew commands fail, you might need to agree to Xcode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case.

## Overriding Defaults

Not everyone's development environment and preferred software configuration is the same.

You can override any of the defaults configured in `default.config.yml` by creating a `config.yml` file and setting the overrides in that file. For example, you can customize the installed packages and apps with something like:

    homebrew_installed_packages:
      - cowsay
      - git
      - go

    mas_installed_apps:
      - { id: 443987910, name: "1Password" }
      - { id: 498486288, name: "Quick Resizer" }
      - { id: 557168941, name: "Tweetbot" }
      - { id: 497799835, name: "Xcode" }

Any variable can be overridden in `config.yml`; see the supporting roles' documentation for a complete list of available variables.

## Included Applications / Configuration (Default)

Packages (installed with Homebrew) and Applications (installed with Homebrew Cask):

  See [default.config.yml](https://github.com/bernied/mac-dev-playbook/blob/master/default.config.yml)


My [dotfiles](https://github.com/bernied/dotfiles) are also installed into the current user's home directory, including the `.macos` dotfile for configuring many aspects of macOS for better performance and ease of use.

Finally, there are a few other preferences and settings added on for various apps and services.

## Future additions

### Things that still need to be done manually

It's my hope that I can get the rest of these things wrapped up into Ansible playbooks soon, but for now, these steps need to be completed manually (assuming you already have Xcode and Ansible installed, and have run this playbook).

  1. Set Term as the default Terminal theme (it's installed, but not set as default automatically).
  2. Install [Sublime Package Manager](http://sublime.wbond.net/installation).
  3. Install all the apps that aren't yet in this setup (see below).
  4. Remap Caps Lock to Escape (requires macOS Sierra 10.12.1+).
  5. Set trackpad tracking rate.
  6. Set mouse tracking rate.
  7. Configure extra Mail and/or Calendar accounts (e.g. Google, Exchange, etc.).

### Applications/packages to be added:

These are mostly direct download links, some are more difficult to install because of custom installers or other nonstandard install quirks:

`None`

### Configuration to be added:

  - I have vim configuration in the repo, but I still need to add the actual installation:
    ```
    mkdir -p ~/.vim/autoload
    mkdir -p ~/.vim/bundle
    cd ~/.vim/autoload
    curl https://raw.githubusercontent.com/tpope/vim-pathogen/master/autoload/pathogen.vim > pathogen.vim
    cd ~/.vim/bundle
    git clone git://github.com/scrooloose/nerdtree.git
    ```


## Author

[Bernhard Damberger](https://github.com/bernied) - Only made minor tweaks.

[Jeff Geerling](http://www.jeffgeerling.com/), 2014 (originally inspired by [MWGriffin/ansible-playbooks](https://github.com/MWGriffin/ansible-playbooks)).
