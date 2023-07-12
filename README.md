# Anthropic (WIP)

[![Gem Version](https://badge.fury.io/rb/anthropic.svg)](https://badge.fury.io/rb/anthropic)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/alexrudall/anthropic/blob/main/LICENSE.txt)
[![CircleCI Build Status](https://circleci.com/gh/alexrudall/anthropic.svg?style=shield)](https://circleci.com/gh/alexrudall/anthropic)

Use the [Anthropic API](https://anthropic.com/blog/anthropic-api/) with Ruby! 🤖❤️

This is very much a WIP and probably doesn't work as I don't have access to the Anthropic API as yet, but it will get a lot better once I do! Hopefully very soon :D

[Ruby AI Builders Discord](https://discord.gg/k4Uc224xVD)

[Rails AI Guides](https://railsai.com)

Follow me on [Twitter](https://twitter.com/alexrudall) for more Ruby / AI content!

### Bundler

Add this line to your application's Gemfile:

```ruby
gem "anthropic"
```

And then execute:

$ bundle install

### Gem install

Or install with:

$ gem install anthropic

and require with:

```ruby
require "anthropic"
```

## Usage

- Get your API key from [https://platform.anthropic.com/account/api-keys](https://platform.anthropic.com/account/api-keys)
- If you belong to multiple organizations, you can get your Organization ID from [https://platform.anthropic.com/account/org-settings](https://platform.anthropic.com/account/org-settings)

### Quickstart

For a quick test you can pass your token directly to a new client:

```ruby
client = Anthropic::Client.new(access_token: "access_token_goes_here")
```

### With Config

For a more robust setup, you can configure the gem with your API keys, for example in an `anthropic.rb` initializer file. Never hardcode secrets into your codebase - instead use something like [dotenv](https://github.com/motdotla/dotenv) to pass the keys safely into your environments.

```ruby
Anthropic.configure do |config|
    config.access_token = ENV.fetch("ANTHROPIC_API_KEY")
end
```

Then you can create a client like this:

```ruby
client = Anthropic::Client.new
```

#### Custom timeout or base URI

The default timeout for any request using this library is 120 seconds. You can change that by passing a number of seconds to the `request_timeout` when initializing the client.

```ruby
client = Anthropic::Client.new(
    access_token: "access_token_goes_here",
    request_timeout: 240
)
```

or when configuring the gem:

```ruby
Anthropic.configure do |config|
    config.access_token = ENV.fetch("ANTHROPIC_API_KEY")
    config.request_timeout = 240 # Optional
    config.extra_headers = {
        "X-Proxy-Refresh": "true"
    } # Optional
end
```

### Completions

Hit the Anthropic API for a completion:

```ruby
response = client.completions(
    parameters: {
        model: "claude-2",
        prompt: "Once upon a time",
        max_tokens: 5
    })
puts response["choices"].map { |c| c["text"] }
# => [", there lived a great"]
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. You can run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`.

### Warning

If you have an `ANTHROPIC_API_KEY` in your `ENV`, running the specs will use this to run the specs against the actual API, which will be slow and cost you money - 2 cents or more! Remove it from your environment with `unset` or similar if you just want to run the specs against the stored VCR responses.

## Release

First run the specs without VCR so they actually hit the API. This will cost 2 cents or more. Set ANTHROPIC_API_KEY in your environment or pass it in like this:

```
ANTHROPIC_API_KEY=123abc bundle exec rspec
```

Then update the version number in `version.rb`, update `CHANGELOG.md`, run `bundle install` to update Gemfile.lock, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at <https://github.com/alexrudall/anthropic>. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [code of conduct](https://github.com/alexrudall/anthropic/blob/main/CODE_OF_CONDUCT.md).

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Ruby Anthropic project's codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/alexrudall/anthropic/blob/main/CODE_OF_CONDUCT.md).
