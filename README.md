# ember-defenestrate

Throw your editor tabs out the window!

## Overview

ember-defenestrate attempts to simplify your ember application development workflow by treating your components and routes holistically. Instead of:

* dashboard/route.js
* dashboard/template.hbs
* dashboard/controller.js
* components/accounts-menu/component.js
* components/accounts-menu/template.hbs
* components/accounts-menu/style.scss
* components/accounts-menu/accounts-menu-item/component.js
* components/accounts-menu/accounts-menu-item/template.hbs
* components/accounts-menu/accounts-menu-item/style.scss

ember-defenestrate will offer you a parallel source tree with:

* dashboard.mbr
* components/accounts-menu.mbr
* components/accounts-menu/accounts-menu-item.mbr

The benefit is that when you're working on the `accounts-menu` which appears in the `dashboard` template, you can do it with 3 editor tabs open, rather than as many as 9.

## Important notes

At the time of this writing, `ember-defenestrate` is a proof-of-concept tool. As such it has a number of important caveats:

1. It is written in ruby. It should be rewritten in Javascript, like all the other cool software.
2. It is not actually a gem, making installation and usage a bit awkward.
3. `ember-defenestrate` only supports the Ember.js pod structure and the new Module Unification structure. If you’re using the classic Ember.js project structure, this version won’t work for you.
4. `ember-defenestrate`’s files can’t live in the same directory as your Ember.js project. This is because of limitations in Broccoli, as well as greedy file watchers that step on each other. A future version of `ember-defenestrate` will hopefully overcome this limitation.
5. There is no support for tests at this time. Mostly, this is because tests live in a different tree in the Ember.js project structure. Secondarily, not every developer would want to see their tests inline.

## Installation

To install, find a nice directory somewhere:

    cd /projects
    git clone https://github.com/pauldoerwald/ember-defenestrate.git
    cd ember-defenestrate
    bundle install
    sudo ln -s ember-defenestrate/ember-defenestrate /usr/local/bin/  # optional

## Usage

Let's assume you have an Ember.js project titled `bookstore` in `/projects/bookstore`. You’ll need to create a corresponding directory for the .mbr files.

    cd /projects
    mkdir bookstore-mbr
    cd bookstore-mbr
    /projects/ember-defenestrate/ember-defenestrate ../bookstore .

The first parameter to `ember-defenestrate` is the Ember.js application source directory. The second parameter is the destination directory for the .mbr files.

`ember-defenestrate` will noisily create a clone of your directory tree, as outlined above.

To stop ember-defenestrate, hit `ctrl-c`.

In your editing workflow, you’ll probably want two editors open: one for `bookstore-mbr` and one for `bookstore`. Sometimes it makes sense to work with the original file (e.g. `config/environment.js`, `app/router.js`), and sometimes it makes sense to work with the `.mbr` file (components, routes).

## Syntax highlighting

So far I have only created one syntax, for Sublime Text, called “Sublime Ember”. I have included the necessary syntax file, but getting it installed is outside the scope of this document at this time. 

## Next Steps

1. Rewrite in Javascript as a proper `npm` module
2. Create a proper syntax file for more than just Sublime Text
3. Create a superior way to handle the naturally independent files such as `config/environment.js`, `app/router.js`, etc.
4. Support the classic Ember.js project structure
5. Integrate with `broccoli` (this would probably require changes to broccoli to allow generating files inside the project tree rather than in the build tree)

