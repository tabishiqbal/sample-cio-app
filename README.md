##Sample Rails App with Context.IO 2.0 API

This is a sample Rails application that uses the Context.IO API to connect to an email account and fetch back data.

* [Read more about Context.IO](https://context.io/docs/2.0)
* [Read the Ruby Context.IO gem documentation](http://www.rubydoc.info/gems/contextio/frames)
* [Context.IO Ruby gem on Github](https://github.com/contextio/contextio-ruby)

###Get up and running

1. Fork this repo and git clone it to your machine
2. Run bundle install (gem install bundler if you do not have bundler)
3. Run `rake db:create`
4. Run `rake db:migrate`
5. Run `bundle exec figaro install`. An `application.yml` file will be created (and added to your gitignore files automagically).
6. Ensure you have a Context.IO key and secret (if you do not, go here to [sign up for a developer account](https://context.io/#signup).) If you do not know where to find your Context.IO key and secret, [click here](https://console.context.io/#settings) (login required).
7. Open the `application.yml` file located under the `config` folder and add your ContextIO key and secret there. If you want to keep the naming convention to the Figaro ENV variables already in this app, use `contextio_key` and `contextio_secret` as your names.
8. Fire up your Rails server `rails s`
9. Go to `localhost:3000` and voila, your app is there. Go ahead and sign up a sample user.

###Dependencies

* We're using Devise to handle user registrations and sessions. You may use something different in your app. We're using Devise because it is pretty easy to get up and running, most people are familiar with this gem, and it is very well documented. Your signup flow may be different.
* This app uses [Figaro](https://github.com/laserlemon/figaro) to store your API keys securely. Please ensure you `bundle exec figaro install` to generate an `application.yml` file, where you can store your Context.IO key and secret.
* We're using the `gist-embed-rails` gem to display gists with sample code. Feel free to get rid of those if you don't need them anymore. We're also using `jquery-turbolinks` to handle Turbolinks weirdness with the gists. Get rid of it if you no longer want the gists!

###Signing up users

The way the flow works currently, a user signs up for the app (i.e. a user in the database is created), then they link their inbox to their account in the app. There are currently no user checks to ensure the user that signs up in this app is the same as the one that is linked with ContextIO. This is by design currently just to keep things easy.

You may also notice the user is created then signed in. This was necessary in order to ensure that when the user was redirected back from the "oauth dance", the user wouldn't have to sign in again. You may choose a different user experience for your app.

###Errors?

You may encounter a postgress error when you start up your rails server. This may mean there is already a postgres database running that for some reason is conflicting. If you get that error, simply do this from your terminal:

```
pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
```

Questions? Email `support@context.io`.
