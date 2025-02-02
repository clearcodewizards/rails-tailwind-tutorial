# Rails 8 with tailwind css tutorial
This tutorial gives you a brief insight into Rails 8. 

## Prerequisite
For this tutorial we need Ruby 3.3.x or higher, so if you already have Ruby 3.3.x you can skip these steps and start directly with step [Create Rails 8 app](#create-rails-8-app)

### Debian/Ubuntu
- gcc
- git
- make
- zlib1g-dev
- libyaml-dev
- libssl-dev

Install via apt:
```
$ sudo apt install gcc make zlib1g-dev libyaml-dev libssl-dev
```

### MacOS
- brew (https://brew.sh/)

## Rbenv
Rbenv is a version manager tool for the Ruby programming language on Unix-like systems. It is useful for switching between multiple Ruby versions on the same machine and for ensuring that each project you are working on always runs on the correct Ruby version.

### Install
#### Debian/Ubuntu
```
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```

Now install ruby-build as a plugin, so you can actually install Ruby:
```
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
```

#### MacOS
```
$ brew install rbenv ruby-build
```

### Initialize
Run rbenv init and put it into your rc file to have rbenv initialized whenever you start a new shell.

#### Debian/Ubuntu
```
$ .rbenv/bin/rbenv init
```

#### MacOS
```
$ rbenv init
```

## Ruby 3.3.x
Install Ruby 3.3.x or higher and set it as the default:
```
$ rbenv install 3.3.7
$ rbenv global 3.3.7
```

## Create rails 8 app
First you need to install the rails gem
```
$ gem install rails -v 8.0.1
```

Bootstrap your Rails 8 app with propshaft (new asset pipeline) and css tailwind.
```
$ rails new --css=tailwind store
```

If you use an editor that supports devcontainer like vscode you can create your rails app with a devcontainer.
```
$ rails new --css=tailwind --devcontainer store
```

### Rails development environment
We will be using foreman for our development environment so we can make changes to Rails which will be directly active.
Add foreman in Gemfile under group **:development**
```
$ cd blog
~/blog $ vi Gemfile
...snip...
group :development do
  gem "foreman"
...snip...
```

Now run bundle install and we are ready to go.
```
~/blog $ bundle install
```

## Start the rails 8 app
Just run bin/dev and you should get the default Rails page.
```
~/blog $ bundle exec bin/dev
```

By default it will listen on http://localhost:3000, you can change this in file Procfile.dev:
```
web: bin/rails server -b 0.0.0.0 -p 3000
```
This will let the rails server listen on all the network interfaces, which is not advised from a security standpoint.

## Rubocop Ruby linter
From Rails 7.2+ rubocop-rails-omakase is used to have better linter defaults for Rails.

But there is one default which contradict Ruby so my suggestion is to override it in .rubocop.yml:
```
Style/StringLiterals:
  EnforcedStyle: single_quotes
```

# Tutorial links to get you started with Rails
- [RailsGuides - Getting Started](https://guides.rubyonrails.org/getting_started.html)
- [MVC or actually RCMHV](docs/RCMHV.md)
- [Stimulus](https://blog.effectussoftware.com/stimulus-in-rails/)
- [Hotwire](https://hotwired.dev/)
