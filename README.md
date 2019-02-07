# NKS API Docs

The original Slate docs are [here](./slate.md).

## Setup

First, check out this repo.

If you're setting up natively on Mac, you're in luck. Run the following commands:

    brew install rbenv
    rbenv init

You might want to add this to your bash profile:

    eval "$(rbenv init -)"

Install latest ruby:

    rbenv install 2.4.2

Allow all apps to use this version:

    rbenv global 2.4.2

Install bundler:

    gem install bundler

Now we're ready to get the doc site requirements. Switch to the project directory:

    bundle install
    bundle exec middleman server

Access the doc site at:

    http://localhost:4567

## Editing Basics

Each high level API resource should have its own file under:

    source/includes/_[resource_name].md

Then insert `_[resource_name].md` in the includes list in `index.html.md`.

Changes appear on the local doc site on refresh.
