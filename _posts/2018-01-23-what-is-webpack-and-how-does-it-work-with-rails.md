---
layout: post
title: "What is Webpack and How Does it Work with Rails?"
excerpt_separator: "<!--more-->"
categories:
  - Ruby
  - JavaScript
tags:
  - Webpack
  - Webpacker Gem
  - Rails
---

I had been a little fuzzy on how to explain webpack, so I did some more research to get a clearer picture. Essentially this is what webpack does: **It takes modules with dependencies and turns those into static assets**. Said another way, webpack takes all of our assets and dependencies and creates a bundle that is ready for production. Awesome! 
<!--more-->Check out this illustration to get a better picture:

![Webpack](./assets/images/webpack-dependencies.png)
*webpack.js.org*

## Why Webpack?
Before webpack we would have to load our JavaScript resources and libraries through different script tags like this:

```html
<!DOCTYPE html>
<html>

<head>
  <title>Page Title</title>
  <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"
    crossorigin="anonymous">
  <script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
    crossorigin="anonymous"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl"
    crossorigin="anonymous"></script>
  <script type="text/javascript" src="script1.js"></script>
  <script type="text/javascript" src="script2.js"></script>
  <script type="text/javascript" src="another_script.js"></script>
  <script type="text/javascript" src="and_more.js"></script>
  <script type="text/javascript" src="last_one_i_swear.js"></script>
...

```

You can probably already guess what can go wrong with this. The order of these script tags is very important, errors can pop up from a wrong hierarchy, certain functions may be called before others or variables can be overwitten. In addition to that with all these files you are making a lot of HTTP request, which can greatly reduce the speed of your application.

## Webpack to the Rescue
With webpack we get a better solution to this: we can require assets like JavaScript, CSS and images files and they are only loaded when we need them for the page. We can hypothetically split our app into different files and load only the ones we need for that page.

Webpack also helps with transformations: Sass or LESS can be built into CSS, and what we write in es6 can be transformed into vanilla JavaScript (this is especially great for JavaScript because it is constantly changing and webpack lets you compile it down to the js your browser can understand). All these things can be configured and automated with the help of webpack; how those files (or modules) are loaded is dependent on how we configure webpack.

## Webpack + Rails = Webpacker (Official Rails Gem for Bundling JavaScript Assets with Webpack)
Just like with non-Rails apps, Rails apps, when they grow large, can have quite a few dependencies. Figuring out which script files depend on each other can be quite daunting, so, starting with Rails 5.1, your new Rails application comes with the webpacker gem out of the box. This gem lets you use Webpack to manage the JavaScript part of your application.

Prerequisites
* Ruby 2.2+
* Rails 4.2+
* Node 6.4.0+
* Yarn

Getting webpack to work with you new Rails app has never been easier: `rails new myapp --webpack`. This command creates a new Rails app with a few caveats. If you look at your folder structure you will find a new folder `app/javascript`, this is where you will essentially build your entire JavaScript app - it even comes with a few example files to get you started. 

To learn more about the file structure and how to integrate webpack into an exisiting Rails app, check out this [Webpacker Readme](https://github.com/rails/webpacker).
