---
layout: post
title:      "Expanding Upon My Insulation-Quotes Rails App With a jQuery Front End"
date:       2017-11-30 23:31:10 +0000
permalink:  expanding_upon_my_insulation-quotes_rails_app_with_a_jquery_front_end
---



Adding dynamic behavior to your Rails application with JavaScript is a nice way to make it more user friendly and intuitive to use. Changing page content without reloading and executing network requests in the background are my personal favorites.

Rails gives us a great foundation with the objects we can create and persist to a database and the CRUD operations that make it so easy to operate on those objects. But with every creation or update of a new object instance we’re immediately redirected to a new page. Sometimes that is what we want, but a lot of times it can be slow and isn’t even necessary. This is where JavaScript come in.

What I’ve done with my pure Rails app is create my own API with ActiveModelSerializers, which takes my ruby objects and converts them into JSON objects.

This is the gist of almost any modification I made: 

1. You hijack the click event of a link to fire an ajax request
2. I that click event, we fire an ajax request to get JSON data for the response
3. With response data we do something



