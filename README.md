# Rails 7 with tailwind css tutorial
This tutorial gives you a brief insight into Rails 7. 

## Prerequisite
For this tutorial we need Ruby 3.x, so if you already have Ruby 3.x you can skip these steps and start directly with step [Create Rails 7 app](#create-rails-7-app)

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

## Ruby 3.3.1
Install Ruby 3.3.1 and set it as the default:
```
$ rbenv install 3.3.1
$ rbenv global 3.3.1
```

## Create rails 7 app
First you need to install the rails gem
```
$ gem install rails -v 7.2.0
```

Bootstrap your Rails 7 app with propshaft (new asset pipeline) and css tailwind. Propshaft will be the default in Rails 8 so lets start using it right now.
```
$ rails new --asset-pipeline=propshaft --css=tailwind blog
```

If you use an editor that supports devcontainer like vscode you can create your rails app with a devcontainer.
```
$ rails new --asset-pipeline=propshaft --css=tailwind --devcontainer blog
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

## Start the rails 7 app
Just run bin/dev and you should get the default Rails page.
```
~/blog $ bundle exec bin/dev
```

By default it will listen on http://localhost:3000, you can change this in file Procfile.dev:
```
web: bin/rails server -b 0.0.0.0 -p 3000
```
This will let the rails server listen on all the network interfaces, which is not advised from a security standpoint.

# Tutorial links to get you started with Rails
- [RailsGuides - Getting Started](https://guides.rubyonrails.org/getting_started.html)
- [MVC or actually RCMHV](docs/RCMHV.md)
- [Stimulus](https://blog.effectussoftware.com/stimulus-in-rails/)
- [Hotwire](https://hotwired.dev/)
