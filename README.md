# Ahoy Email

:construction: Coming soon - May 1, 2014

:envelope: Simple, powerful email tracking for Rails

Keep track of emails:

- sent
- opened
- clicked

## Installation

Add this line to your application’s Gemfile:

```ruby
gem 'ahoy_email'
```

And run the generator. This creates a model to store messages.

```sh
rails generate ahoy_email:install
rake db:migrate
```

## How It Works

Ahoy creates an `Ahoy::Message` record when an email is sent.

### Open

An invisible pixel is added right before the closing `</body>` tag to HTML emails.

If a recipient has images enabled in his / her email client, the pixel is loaded and an open is recorded.

### Click

Links in HTML emails are rewritten to pass through your server.

````
http://chartkick.com
```

becomes

```
http://www.yourdomain.com/ahoy/messages/rAnDoMtOken/click?url=http%3A%2F%2Fchartkick.com&signature=...
```

A signature is added to prevent [open redirects](https://www.owasp.org/index.php/Open_redirect).

### UTM Parameters

UTM parameters are added to each link if they don’t already exist.

By default, `utm_medium` is set to `email`.

### User

To specify the user, use:

```ruby
mail user: user, subject: "Awesome!", to: "..."
```

User is [polymorphic](http://railscasts.com/episodes/154-polymorphic-association), so use it with any model.

## TODO

- Subscription management (lists, opt-outs)

## Contributing

Everyone is encouraged to help improve this project. Here are a few ways you can help:

- [Report bugs](https://github.com/ankane/ahoy_email/issues)
- Fix bugs and [submit pull requests](https://github.com/ankane/ahoy_email/pulls)
- Write, clarify, or fix documentation
- Suggest or add new features
