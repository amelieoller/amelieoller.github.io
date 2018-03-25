---
layout: post
title: "Deploying Your Rails/JS App to Heroku - The Problems I Ran Into and How I Solved Them"
excerpt_separator: "<!--more-->"
categories:
  - JavaScript
  - Ruby
tags:
  - Heroku
  - Devise
  - OAuth2
---

When deploying my first Rails/JS (with Devise and Google's OAuth2) app to Heroku I ran into a few speedbumps. Now, admittedly a few of these are rookie mistakes and I might have not run into them had I know more at the time but maybe my mistakes can still help out somone else in the future.

<!--more-->

## First Rookie Mistake: Make Sure You Precompile Your ES6 Code

If you don't do this you might run into an error that looks something like this: `Precompiling assets failed`

* To figure out what exactly was wrong I ran `NODE_ENV=production RAILS_ENV=production rails assets:precompile --trace` in my local console, which gave me the necessary hints to solve the [problem](https://github.com/rails/webpacker/issues/530).
* Since I had very little ES6 code in my app at the time I decided to turn all ES6 to ES5 (it really wasn't that much)
* Better solution: Precompile your ES6!

## Devise Secret Not Set

By running the same command, `NODE_ENV=production RAILS_ENV=production rails assets:precompile --trace` I recieved another error message:

```
Devise.secret_key was not set. Please add the following to your Devise initializer: config.secret_key = '3f64971...'
```

Simply do what it says and add that line to your `config/initializers/devise.rb`.

## Run Your Migrations in Heroku

The home page worked at this point in time, but when I clicked on any link I would get my next error (definitely not the most helpful error message in the world): `We're sorry, but something went wrong.`

* Turns out I hadn't run `rake db:migrate` (and `rake db:seed`) in my heroku console yet. Doing that solved the problem. This [StackOverflow question](https://stackoverflow.com/questions/7669077/heroku-deployment-dead-pages-were-sorry-but-something-went-wrong) helped me get there.

## Add Your Heroku URL in Your Google Developer Console (When Using Google's OAuth2)

When trying to login through my Devise gem and through Google's OAuth2 I received a `redirect_uri_mismatch google oauth heroku` error.
The reason for this error is because I had only registered my localhost domain in my API console for this app. Again, [StackOverflow](https://stackoverflow.com/questions/11485271/google-oauth-2-authorization-error-redirect-uri-mismatch) saved the day.

### To fix this:

1.  Go to your [Google Developer Console](https://console.developers.google.com/apis/dashboard)
2.  Select your app at the top in the dropdown, if not already selected
3.  Go to credentials
4.  Go to your exisiting client (don't create a new one)
5.  At the bottom under _Authorized redirect URIs_ add your heroku app URL, like so: `https://your-app.herokuapp.com/users/auth/google_oauth2/callback` (your app might not be under users - compare it to your localhost url!)
6.  Save and you're done.

I hope this will help someone sometime.
