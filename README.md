# Stackpoint API Docs

The compressed docs site currently reside in the UI repo, which is debatable. Ideally we would have docs.stackpoint.io or something like that.

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

Each high level API resource should have it's own file under:

    source/includes/_<resource_name>.md

Then insert `_<resource_name>.md` in the includes list in `index.html.md`.

Changes appear on the local doc site on refresh.

Push to master when done, no PR necessary.

## Deploying Docs to quarter-master-frontend

### Pre-requisite

You need to have `quarter-master-frontend` checked out.

    export QM_FE_PATH=/foo/bar/quarter-master-frontend

First build the compressed version of the docs:

    bundle exec middleman build --clean

Remove the old compressed files:

    rm -rf $QM_FE_PATH/docs

Copy new doc files:

    cp -R build $QM_FE_PATH/docs

Now switch to FE directory, add the changes and make a PR/merge as usual.
