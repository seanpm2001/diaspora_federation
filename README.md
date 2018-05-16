# diaspora* federation library
### A library that provides functionalities needed for the diaspora\* federation protocol

**master:** [![Build Status master](https://travis-ci.org/diaspora/diaspora_federation.svg?branch=master)](https://travis-ci.org/diaspora/diaspora_federation) |
**develop:** [![Build Status develop](https://travis-ci.org/diaspora/diaspora_federation.svg?branch=develop)](https://travis-ci.org/diaspora/diaspora_federation)

[![Code Climate](https://codeclimate.com/github/diaspora/diaspora_federation/badges/gpa.svg)](https://codeclimate.com/github/diaspora/diaspora_federation)
[![Test Coverage](https://codeclimate.com/github/diaspora/diaspora_federation/badges/coverage.svg)](https://codeclimate.com/github/diaspora/diaspora_federation/coverage)
[![Dependency Status](https://img.shields.io/librariesio/github/diaspora/diaspora_federation.svg)](https://libraries.io/github/diaspora/diaspora_federation)
[![Inline docs](https://inch-ci.org/github/diaspora/diaspora_federation.svg?branch=master)](https://inch-ci.org/github/diaspora/diaspora_federation)
[![Gem Version](https://badge.fury.io/rb/diaspora_federation.svg)](https://badge.fury.io/rb/diaspora_federation)

[Gem Documentation](http://www.rubydoc.info/gems/diaspora_federation/) |
[Protocol Documentation](https://diaspora.github.io/diaspora_federation/) |
[Bugtracker](https://github.com/diaspora/diaspora_federation/issues)

This repository contains two gems:

* `diaspora_federation` provides the functionality for de-/serialization and de-/encryption of Entities in the protocols used for communication among the various installations of diaspora\*.
* `diaspora_federation-rails` is a rails engine that adds the diaspora\* federation protocol to a rails app.

## Usage

Add the gem to your ```Gemfile```:

```ruby
gem "diaspora_federation-rails"
```

Mount the routes in your ```config/routes.rb```:

```ruby
mount DiasporaFederation::Engine => "/"
```

Configure the engine in ```config/initializers/diaspora_federation.rb```:

```ruby
DiasporaFederation.configure do |config|
  # the pod url
  config.server_uri = AppConfig.pod_uri

  config.define_callbacks do
    on :fetch_person_for_webfinger do |diaspora_id|
      person = Person.find_local_by_diaspora_id(diaspora_id)
      if person
        DiasporaFederation::Discovery::WebFinger.new(
          # ...
        )
      end
    end

    on :fetch_person_for_hcard do |guid|
      # ...
    end
  end
end
```

## Contributing

See [our contribution guide](/CONTRIBUTING.md) for more information on how to contribute to the diaspora\* federation library.

## License

[GNU Affero General Public License](/LICENSE).
