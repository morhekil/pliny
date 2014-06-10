# Fork of Pliny with no DB dependencies

This is a fork of awesome [Pliny](https://github.com/interagent/pliny) that
removes all databases dependencies. It allows you to generate API skeleton
that you can use with any DB you, or without DB backing at all.

# Pliny

Opinionated template Sinatra app for writing excellent APIs in Ruby.

[![Build Status](https://travis-ci.org/interagent/pliny.svg?branch=master)](https://travis-ci.org/interagent/pliny)

It bundles some of the patterns we like to develop these apps:

- Config: `ENV` wrapper for explicit defining what config vars are mandatory and optional
- Endpoints: the Sinatra equivalent of a Rails Controller
- Initializers: tiny files to configure libraries/etc (equivalent of Rails)
- Mediators: plain ruby classes to manipulate models
- Models: very thin wrappers around the database

And gems/helpers to tie these together and support operations:

- [CORS middleware](lib/pliny/middleware/cors.rb) to allow JS developers to consume your API
- [Honeybadger](https://www.honeybadger.io/) for tracking exceptions
- [Log helper](test/log_test.rb) that logs in [data format](https://www.youtube.com/watch?v=rpmc-wHFUBs) [to stdout](https://adam.heroku.com/past/2011/4/1/logs_are_streams_not_files)
- [Rspec](https://github.com/rspec/rspec) for lean and fast testing
- [Puma](http://puma.io/) as the web server, [configured for optimal performance on Heroku](config/puma.rb)
- [Rack-test](https://github.com/brynary/rack-test) to test the API endpoints
- [Request IDs](lib/pliny/middleware/request_id.rb)
- [RequestStore](http://brandur.org/antipatterns), thread safe option to store data with the current request
- [RR](https://github.com/rr/rr/blob/master/doc/03_api_overview.md) for amazing mocks and stubs
- [Versioning](lib/pliny/middleware/versioning.rb) to allow versioning your API in the HTTP Accept header

## Getting started

Install the gem:

```bash
$ gem install pliny
```

And initialize a new app:

```bash
$ pliny-new myapp
$ cd myapp && bin/setup
```

Pliny also bundles some generators to help you get started:

```bash
$ bundle exec pliny-generate model artist
created model file ./lib/models/artist.rb
created test ./test/models/artist_test.rb

$ bundle exec pliny-generate mediator artists/creator
created base mediator ./lib/mediators/base.rb
created mediator file ./lib/mediators/artists/creator.rb
created test ./test/mediators/artists/creator_test.rb

$ bundle exec pliny-generate endpoint artists
created endpoint file ./lib/endpoints/artists.rb
add the following to lib/routes.rb:
  mount Endpoints::Artists
created test ./spec/endpoints/artists_spec.rb
created test ./spec/acceptance/artists_spec.rb

$ bundle exec pliny-generate schema artists
created schema file ./docs/schema/schemata/artist.yaml
rebuilt ./docs/schema.json
```

To test your application:

```bash
bundle exec rake
```

Or to run a single test suite:

```bash
bundle exec rspec spec/acceptance/artists_spec.rb
```

## Development

Run tests:

```
bundle install
git submodule update --init
rake
```

## Meta

Created by Brandur Leach and Pedro Belo.
