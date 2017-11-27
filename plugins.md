---
layout: default
title: Plugins
url: /plugins
previous: /faqs
next: /credits
---

<em class="t-gray">Extensions that use the RubyGems plugin API.</em>

As of RubyGems 1.3.2, RubyGems will load plugins installed in gems or
`$LOAD_PATH`.  Plugins must be named 'rubygems\_plugin' (.rb, .so, etc)
and placed at the root of your gem's #require\_path.  Plugins are
discovered via `Gem::find_files` then loaded.

The following list of RubyGems plugins is probably not exhaustive. If you know of plugins that we missed, feel free to update this page.

* [executable-hooks](#executable-hooks)
* [gem-browse](#gem-browse)
* [gem-ctags](#gem-ctags)
* [gem-empty](#gem-empty)
* [gem_info](#gem_info)
* [gem-init](#gem-init)
* [gem-compare](#gem-compare)
* [gem-man](#gem-man)
* [gem-nice-install](#gem-nice-install)
* [gem-orphan](#gem-orphan)
* [gem-patch](#gem-patch)
* [gem-toolbox](#gem-toolbox)
* [gem-wrappers](#gem-wrappers)
* [graph](#graph)
* [maven_gem](#maven_gem)
* [manpages](#manpages)
* [open_gem](#open_gem)
* [push_safety](#push_safety)
* [rbenv-gem-rehash](#rbenv-gem-rehash)
* [rubygems-desc](#rubygems-desc)
* [rubygems-openpgp](#rubygems-openpgp)
* [rubygems-sandbox](#rubygems-sandbox)
* [rubygems_snapshot](#rubygems_snapshot)
* [specific_install](#specific_install)
* [rubygems-tasks](#rubygems-tasks)
* [rubygems_plugin_generator](#rubygems_plugin_generator)


## executable-hooks

[https://github.com/mpapis/executable-hooks](https://github.com/mpapis/executable-hooks)

Extends rubygems to support executables plugins.

In gem lib dir create rubygems_executable_plugin.rb:

    Gem.execute do |original_file|
      warn("Executing: #{original_file}")
    end


## gem-browse

[https://github.com/tpope/gem-browse](https://github.com/tpope/gem-browse)

Adds four commands:

- `gem edit` opens a gem in your editor
- `gem open` opens a  gem  by name in your editor
- `gem clone` clones a gem from GitHub
- `gem browse` opens a gem's homepage in your browser


## gem-empty

[https://github.com/rvm/gem-empty](https://github.com/rvm/gem-empty)

Adds command `gem empty` to remove all gems from current `GEM_HOME`.


## gem-ctags

[https://github.com/tpope/gem-ctags](https://github.com/tpope/gem-ctags)

Adds a `gem ctags` command to invoke the Exuberant Ctags indexer on already-installed gems, and then automatically invokes it on gems as they are installed.


## gem_info

[https://github.com/oggy/gem_info](https://github.com/oggy/gem_info)

Adds a `gem info` command with fuzzy matching on name and version. Designed for scripting use.


## gem-init

[https://github.com/mwhuss/gem-init](https://github.com/mwhuss/gem-init)

Adds `gem init` to create a barebones gem.


## gem-compare

[https://github.com/fedora-ruby/gem-compare](https://github.com/fedora-ruby/gem-compare)

Adds `gem compare` command that can help you to track upstream changes in the released
.gem files by comparing gemspec values, gemspec and Gemfile dependencies and files.


## gem-man

[https://github.com/defunkt/gem-man](https://github.com/defunkt/gem-man)

The `gem man` command lets you view a gem's man page.


## gem-nice-install

[https://github.com/voxik/gem-nice-install](https://github.com/voxik/gem-nice-install)

Tries to install system dependencies needed to install your gems with binary extensions
using standard `gem install` command. This currently works only for Fedora, but
hopefully will be extended.


## gem-orphan

[https://github.com/sakuro/gem-orphan](https://github.com/sakuro/gem-orphan)

Adds a `gem orphan` command that finds and lists  gems on which no other gems are depending.


## gem-patch

[https://github.com/strzibny/gem-patch](https://github.com/strzibny/gem-patch)

Adds `gem patch` command, which enables you to apply patches directly on `.gem` files.
Supports both RubyGems 1.8 and RubyGems 2.0.


## gem-toolbox

[https://github.com/gudleik/gem-toolbox](https://github.com/gudleik/gem-toolbox)

Adds six commands:

- `gem open` - opens a gem in your default editor
- `gem cd` - changes your working directory  to the gem's source root
- `gem readme` - locates and displays a gem's readme file
- `gem history` - locates and display's a gem's changelog
- `gem doc` - Browse a gem's documentation in your default browser
- `gem visit` - Open a gem's homepage in your default browser


## gem-wrappers

[https://github.com/rvm/gem-wrappers](https://github.com/rvm/gem-wrappers)

Create gem wrappers for easy use of gems in cron and other system locations.
By default wrappers are installed when a gem is installed.

Adds this commands:

- `gem wrappers regenerate` - force rebuilding wrappers for all gem executables
- `gem wrappers` - show current configuration


## graph

[https://github.com/seattlerb/graph](https://github.com/seattlerb/graph)

Adds a `gem graph` command to output a gem dependency graph in graphviz's dot format.


## maven_gem

[https://github.com/jruby/maven_gem](https://github.com/jruby/maven_gem)

Adds `gem maven` to install any Maven-published Java library as though it were a gem.


## manpages

[https://github.com/bitboxer/manpages](https://github.com/bitboxer/manpages)

Exposes manpages inside of a gem to the `man` command without the need to call `gem man` or
another command to read the man page of a gem.


## open_gem

[https://github.com/adamsanderson/open_gem](https://github.com/adamsanderson/open_gem)

Adds two commands:

- `gem open` opens a gem in your default editor
- `gem read` opens a gem's rdoc in your default browser


## push_safety

[https://github.com/jdleesmiller/push_safety](https://github.com/jdleesmiller/push_safety)

Applies a whitelist to `gem push` to prevent accidentally pushing private gems to the public RubyGems repository.


## rbenv-gem-rehash

[https://github.com/sstephenson/rbenv-gem-rehash](https://github.com/sstephenson/rbenv-gem-rehash)

Automatically runs `rbenv rehash` after installing or uninstalling gems.

> This plugin is deprecated since its behavior is now included in
> rbenv core.


## rubygems-desc

[https://github.com/chad/rubygems-desc](https://github.com/chad/rubygems-desc)

Adds `gem desc` to describe a gem by name.


## rubygems-openpgp

[https://github.com/grant-olson/rubygems-openpgp](https://github.com/grant-olson/rubygems-openpgp)

Adds commands and flags to allow OpenPGP signing of gems.

- `gem sign foo.gem` to sign a gem.
- `gem verify foo.gem --trust` to verify a gem.
- `gem build foo.gemspec --sign` to sign at build time.
- `gem install foo --verify --trust` to verify on install.


## rubygems-sandbox

[https://github.com/seattlerb/rubygems-sandbox](https://github.com/seattlerb/rubygems-sandbox)

Manages command-line gem tools and dependencies with a `gem  sandbox` command. This lets you install things like flay and rdoc outside of the global rubygems repository.


## rubygems_snapshot

[https://github.com/rogerleite/rubygems_snapshot](https://github.com/rogerleite/rubygems_snapshot)

Adds `gem snapshot` to create exports of all your current gems into a single file that you can import later.


## specific_install

[https://github.com/rdp/specific_install](https://github.com/rdp/specific_install#readme)

Allows you to install an "edge" gem straight from its GitHub repository, or install one from an arbitrary web URI.


## rubygems-tasks

[https://github.com/postmodern/rubygems-tasks](https://github.com/postmodern/rubygems-tasks#readme)

rubygems-tasks provides agnostic and unobtrusive Rake tasks for building, installing and releasing Ruby Gems.


## rubygems_plugin_generator

[https://github.com/brianstorti/rubygems_plugin_generator](https://github.com/brianstorti/rubygems_plugin_generator)

`rubygems_plugin_generator` is a plugin that generates plugins. Just run `gem plugin <name>` and you are good to go.
