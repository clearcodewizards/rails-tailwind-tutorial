# Rails 7 with tailwind css tutorial
This tutorial gives you a brief insight into Rails 7. 

## Prerequisite
For this tutorial we need Ruby 3.x, so if you already have Ruby 3.x you can skip these steps and start directly with step [Create Rails 7 app](#create-rails-7-app)
- gcc
- make
- zlib1g-dev
- libyaml-dev
- libssl-dev

For Debian/Ubuntu you can run:
```
$ sudo apt install gcc make zlib1g-dev libyaml-dev libssl-dev
```
For MacOS you can run:
```
$ brew install gcc make zlib libyaml openssl
```

## Rbenv
Rbenv is a version manager tool for the Ruby programming language on Unix-like systems. It is useful for switching between multiple Ruby versions on the same machine and for ensuring that each project you are working on always runs on the correct Ruby version.
### Install
```
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```
Run rbenv init and put it into your rc file to have rbenv initialized whenever you start a new shell.
```
$ .rbenv/bin/rbenv init
```
For instance with bash:
```
$ vi .bashrc
...snip...
eval "$($HOME/.rbenv/bin/rbenv init - bash)"
```
Now install ruby-build as a plugin, so you can actually install Ruby:
```
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
```
## Ruby 3.2.2
Install Ruby 3.2.2 and set it as the default:
```
$ rbenv install 3.2.2
$ rbenv global 3.2.2
```
## Create rails 7 app
First you need to install the rails gem
```
$ gem install rails -v 7.0.7.2
```
Bootstrap your Rails 7 app with propshaft (new asset pipeline), importmap and css tailwind. Propshaft will be the default in Rails 8 so lets start using it right now.
```
$ rails new --asset-pipeline=propshaft --javascript=importmap --css=tailwind rails7
```
### Rails development environment
We will be using foreman for our development environment so we can make changes to Rails which will be directly active.
Add foreman in Gemfile under group **:development**
```
$ cd rails7
~/rails7 $ vi Gemfile
...snip...
group :development do
  gem "foreman"
...snip...
```
Now run bundle install and we are ready to go.
```
~/rails7 $ bundle install
```
## Start the rails 7 app
Just run bin/dev and you should get the default Rails page.
```
~/rails7 $ bundle exec bin/dev
```
By default it will listen on http://localhost:3000, you can change this in file Procfile.dev:
```
web: bin/rails server -b 0.0.0.0 -p 3000
```
This will let the rails server listen on all the network interfaces, which is not advised from a security standpoint.

# Tutorial links to get you started with Rails
- [RailsGuides - Getting Started](https://guides.rubyonrails.org/getting_started.html)
- [RailsGuides - Routing](https://guides.rubyonrails.org/routing.html)
- [Stimulus](https://blog.effectussoftware.com/stimulus-in-rails/)
- [Assets](docs/assets.md) WIP
- [MVC or actually RCMHV](docs/RCMHV.md) WIP
