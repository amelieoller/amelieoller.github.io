---
layout: post
title: "Expanding Upon My Insulation-Quotes Rails App With a jQuery Front-End"
excerpt_separator: "<!--more-->"
updated: "2018-01-12T09:23:00Z"
categories:
  - Ruby
  - JavaScript
tags:
  - Rails
  - jQuery
---

Adding dynamic behavior to your Rails application with JavaScript is a nice way to make it more user friendly and intuitive to use. Changing page content without reloading and executing network requests in the background are my personal favorites.

<!--more-->

Rails provides a great foundation for creating a well rounded CRUD app. You can create and persist objects to a database and operate on them easily with simple CRUD actions. But with every creation or update of a new object instance we’re immediately redirected to a new page; sometimes that is what we want, but often enough it results in frustration by the user because of slow and unnecessary page reloads. **JavaScript to the rescue.**

A little while back I created a Rails app [Insulation Quotes](https://github.com/amelieoller/insulation-quotes) that allows for easy creation of quotes for insulation professionals. To enhance this app I added some JavaScript to make it easier and faster to use:

1. I created my own API within my Rails app with [ActiveModelSerializers](https://github.com/rails-api/active_model_serializers), which takes ruby objects and converts them into JSON objects so I can pull data from those anywhere in my app. ActiveModelSerializers saves you from having to build our own JSON strings one by one.
2. In order to prevent pages from refreshing every time we make a server request, what you need to do is hijack the click event of a link to fire an ajax request instead. That ajax request asks for the JSON data we can so conveniently get from our previously created API and gives us that data in the response.
3. The last step is to do something with the response; you could append certain JSON elements to the DOM for example or when getting back the data from a form, 'spit' out the response right on that same page, **no more redirects**!