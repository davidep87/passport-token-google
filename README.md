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

    $ npm install passport-token-google2

## Usage

#### Configure Strategy

The Google authentication strategy authenticates users using a Google
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a app ID and app secret.

    const GoogleStrategy = require('passport-token-google2').Strategy

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

GET request need to have `id_token` sent as `access_token` in either the query string or set as a header.  If a POST is being preformed they can also be included in the body of the request.


#### Loopback 3.X support
Complaint with UserIdentity and User model of loopback

The module can be used to authenticate `id_token` sent by client side(android,ios or web) on the loopback as `access_token` in the callbackPath as GET argument.


Add this to providers.json as described in [tutorial!](https://loopback.io/doc/en/lb3/Third-party-login-using-Passport.html).

```
 "google-login": {
    "provider": "google",
    "module": "passport-token-google2",
    "clientID": "{google-client-id-1}",
    "clientSecret": "{google-client-secret-1}",
    "callbackPath": "/auth/google/token",
    "scope": ["email", "profile"],
    "failureFlash": true,
    "json": true,
    "session": false

  }
```


