Middleman Delpoy -- Deploy a [middleman](http://middlemanapp.com/) built site over rsync or via git (e.g. gh-pages on github).

[![Build Status](https://secure.travis-ci.org/tvaughan/middleman-deploy.png)](http://travis-ci.org/tvaughan/middleman-deploy)

===

## QUICK START

### Step 1

    gem install middleman-deploy

### Step 2

    middleman init example-site
    cd example-site

### Step 3

Edit `Gemfile`, and add:

    gem "middleman-deploy", "~>0.0.1"

Then run:

    bundle install

### Step 4a - Rsync setup

First be sure that `rsync` is installed.

#### These settings are required.

Edit `config.rb`, and add:

    activate :deploy do |deploy|
      deploy.method = :rsync
      deploy.user = "tvaughan"
      deploy.host = "www.example.com"
      deploy.path = "/srv/www/site"
    end

Adjust these values accordingly.

#### These settings are optional.

To use a particular SSH port, add:

      deploy.port = 5309

Default is `22`.

To remove orphaned files or directories on the remote host, add:

      deploy.clean = true

Default is `false`.

### Step 4b - Git setup

First be sure that you have already placed your project under revision
control using git.

Edit `config.rb`, and add:

    activate :deploy do |deploy|
      deploy.method = :git
    end

#### These settings are optional.

To use a particular remote, add:

      deploy.remote = "some-other-remote-name"

Default is `origin`. Run `git remote -v` to see a list of possible
remotes.

To use a particular branch, add:

      deploy.branch = "some-other-branch-name"

Default is `gh-pages`. Run `git branch -a` to see a list of possible
branches.

### Step 5

    middleman build [--clean]
    middleman deploy [--clean]

### NOTES

Inspired by the rsync task in [Octopress](https://github.com/imathis/octopress).
