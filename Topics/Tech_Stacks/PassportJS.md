# Passport.js

## Table of contents
### [Introduction](#introduction)
### [Prerequisites](#prerequisites)
### [Setup and Installation](#setup-and-installation)
### [Strategies](#strategies)
### [Sessions](#sessions)
### [Authentication Requests](#authentication-requests)
### [Summary](#summary)

## Introduction

Passport.js is a widely used middleware for authentication and authorization in Node.js-based web applications. Its primary purpose is to simplify the process of user authentication by offering a flexible and modular framework. This flexibility allows developers to integrate Passport.js with many different authentication strategies such as verifying local username and password credentials, OAuth (for example, via Google or Facebook), and OpenID. 

## Prerequisites

You should have Node.js already installed. This guide assumes that you have a good understanding of JavaScript and basic web development concepts. We are also assuming that you are working with an Express.js based application, the framework Passport is most commonly used with it.

## Setup and Installation

To install Passport.js, you can run the following npm command. 

```
npm install passport
```

Once Passport.js has been installed, you can start using it by including the following import in your JavaScript file. 

``` JavaScript
const passport = require('passport');
```

To use Passport in an Express.js based application, you can initialize Passport in your app with the following line assuming you declared your application as `app`.

``` JavaScript
app.use(passport.initialize());
```

## Strategies

A Passport.js strategy is the method by which Passport logs in users and authenticates them. There are over 500 strategies that you can use with Passport. In this guide we will be looking specifically at the local strategy, however there are other common strategies such as OAuth with Google, Facebook, etc., or OpenID.

### Local Strategy

Passport local strategy is the verification of local username and password credentials stored in a database. 

Firstly, to use this strategy we need to install it with the following command.

```
npm install passport-local
```

And import it with the following line.

``` JavaScript
const LocalStrategy = require('passport-local').Strategy;
```

Now we can configure the Passport local strategy with the following code.

``` JavaScript
passport.use(new LocalStrategy(
  function(username, password, done) {
    User.findOne({ username: username }, function (err, user) {
      if (err) { return done(err); }
      if (!user) { return done(null, false); }
      if (!user.verifyPassword(password)) { return done(null, false); }
      return done(null, user);
    });
  }
));
```

Essentially, we use the `passport.use` function to tell Passport which strategy we want to use. The `LocalStrategy` constructor takes in a callback function as a an argument. This callback function is referred to as the "verify" function, because it's the function that verifies the user's credentials passed in.

The verify function `function(username, password, done) { ... }` is where you define the logic to verify the user's credentials.
`username` and `password` are the credentials submitted by the user through a login form.
`done` is a callback function that is called to indicate whether the authentication was successful or not.

In the above code, the body of the verify function is just an example of what the logic to verify the user's credentials might look like. Your actual code might vary based on the requirements of your application.

## Sessions

Another useful aspect of Passport.js is that it will take care of persistent login sessions for us. Essentially, HTTP is a stateless protocol, meaning that each request to an application is understood in isolation, without any knowledge of previous requests. This means that we need a way for web applications to keep track of logged in users. This is where sessions come in. A session is established by setting an HTTP cookie in the user's browser, which the browser sends to the server on every request. Thus, the server is able to keep track of authenticated users creating a persistent login session. 

Firstly, we need to import and initialize the Passport session middleware. 

``` JavaScript
const session = require('express-session');

app.use(session({
  secret: 'your-secret-key',
  resave: false,
  saveUninitialized: false
}));
```

Now we can make use of Passport sessions with the following code.

``` JavaScript
passport.serializeUser(function(user, done) {
  done(null, user.id);
});

passport.deserializeUser(function(id, done) {
  User.findById(id, function (err, user) {
    done(err, user);
  });
});
```

In order for persistent login sessions to work, Passport must serialize the authenticated user to the session. Passport provide methods `serializeUser`, which is called during login, and `deserializeUser`, which is called on all subsequent requests. 

Passport does not impose restrictions on how user information is stored, so you provide your own serialization and deserialization logic to Passport. In general, we simply provide the user ID for serialization and find the user by ID for deserialization as demonstrated in the above code.

## Authentication Requests

Now that we have configured our strategy and session middleware, we are finally ready to begin using Passport's authentication middleware in our login and logout routes. 

``` JavaScript
app.post('/login', 
  passport.authenticate('local', { failureRedirect: '/login-failure' }),
  function(req, res) {
    res.redirect('/login-success');
  }
);

app.get('/logout', (req, res) => {
  req.logout();  // Passport's logout method
  res.redirect('/');
});
```

For login requests, we use `passport.authenticate` as middleware for the route. It's also important to mention that we also use `passport.authenticate` for any route that requires authentication, i.e. checking that the user is logged in. For logout requests, we use `req.logout`, which is a function provided by Passport to log the user out of the current session. 

## Summary
In this guide we learned about Passport.js and how to use it in our Express.js based application. We learned how to use Passport strategies, sessions, and how to use the middleware in our authentication routes. We see how Passport is extremely useful because of its flexibility and unobtrusiveness.

To learn more, you can check out the official documentation at https://www.passportjs.org/docs/.

