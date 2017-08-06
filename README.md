# Passport-Token-Google
### This is an updated version of [Passport-Google-Token](https://github.com/Jcbobo88/passport-google-token)
### This update contain a minor fix related to the new API Version 3

[Passport](http://passportjs.org/) strategy for authenticating with [Google](http://www.google.com/)  access tokens using the OAuth 2.0 API.

This module lets you authenticate using Google in your Node.js applications.
By plugging into Passport, Google authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/) and [Koa](http://koajs.com).

## Installation

    $ npm install passport-token-google

## Usage

#### Configure Strategy

The Google authentication strategy authenticates users using a Google
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a app ID and app secret.

    const GoogleStrategy = require('passport-token-google').Strategy

    passport.use(new GoogleStrategy({
        clientID: GOOGLE_CLIENT_ID,
        clientSecret: GOOGLE_CLIENT_SECRET
      },
      function(accessToken, refreshToken, profile, done) {
        fetchGoogleUser(profile, accessToken)
          .then((user) => done(null, user))
          .catch((err) => {
            // Handle the error
            done(null, {})
          });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate('google-token')` to authenticate requests.

    router.get('/auth/google/token', passport.authenticate('google-token'), someFunction);

GET request need to have `access_token` and optionally the `refresh_token` in either the query string or set as a header.  If a POST is being preformed they can also be included in the body of the request.
