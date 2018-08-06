# fluentd-ui

[![Build Status](https://travis-ci.org/fluent/fluentd-ui.svg?branch=master)](https://travis-ci.org/fluent/fluentd-ui)
[![Gem Version](https://badge.fury.io/rb/fluentd-ui.svg)](http://badge.fury.io/rb/fluentd-ui)
[![Code Climate](https://codeclimate.com/github/fluent/fluentd-ui/badges/gpa.svg)](https://codeclimate.com/github/fluent/fluentd-ui)

fluentd-ui is a browser-based [fluentd](http://www.fluentd.org) and [td-agent](https://docs.treasuredata.com/articles/td-agent) manager that supports following operations.

* Install, uninstall, and upgrade Fluentd plugins
* start/stop/restart fluentd process
* Configure Fluentd settings such as config file content, pid file path, etc
* View Fluentd log with simple error viewer

[Official documentation](http://docs.fluentd.org/articles/fluentd-ui) \| [Changelog](./ChangeLog.md)


## Requirements

- ruby 2.2.2 or later (since v1.0.0)
- fluentd v1.0.0 or later (also supports td-agent 3)
  - Currently, fluentd v1 and td-agent 3 support is in alpha state

And some additional packages (Debian / Ubuntu)

- build-essential
- libssl-dev
- libxml2-dev
- libxslt1-dev
- ruby-dev

## Development

    $ git clone https://github.com/fluent/fluentd-ui
    $ cd fluentd-ui
    $ bundle install
    $ bin/rails s

Also you need a [chromedriver](https://sites.google.com/a/chromium.org/chromedriver/downloads) or chromiumdriver for test.

    $ npm install -g chromedriver
    Or,
    $ brew install chromedriver
    Or,
    $ sudo apt install chromium-driver

NOTE: `chromedriver` executable binary should be located under your `$PATH`.

## Building fluentd-ui.gem

    # Generate pre-compiled assets
    $ RAILS_ENV=production bin/rails assets:precompile

    # fluentd-ui X.X.X built to pkg/fluentd-ui-X.X.X.gem.
    $ RAILS_ENV=production bin/rails build

    # Push to rubygems.org
    $ bin/rails release
