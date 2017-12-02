---
layout: post
title:      "Expanding Upon My Insulation-Quotes Rails App With a jQuery Front End"
date:       2017-11-30 18:31:11 -0500
permalink:  expanding_upon_my_insulation-quotes_rails_app_with_a_jquery_front_end
---



Adding dynamic behavior to your Rails application with JavaScript is a nice way to make it more user friendly and intuitive to use. Changing page content without reloading and executing network requests in the background are my personal favorites.

Rails gives us a great foundation with objects we can create and persist to a database and the CRUD operations that make it so easy to operate on those objects. But with every creation or update of a new object instance we’re immediately redirected to a new page. Sometimes that is what we want, but a lot of times it can be slow and isn’t really necessary. This is where JavaScript come in.

What I’ve done with my Rails app is create my own API with [ActiveModelSerializers](https://github.com/rails-api/active_model_serializers), which takes my ruby objects and converts them into JSON objects so I can pull data from those anywhere in my app. ActiveModelSerializers saves us from having to build our own JSON strings one by one.

Now we have our API, what's next? In order to prevent our pages from refreshing everytime we make a server request, what we need to do is hijack the click event of a link to fire an ajax request instead. That ajax request asks for the JSON data we can so conveniently get from our previously created API and gives us that data in the response. The last step is to do something with the response, you may want to append certain JSON elements to the DOM.

One example of what you can do with this is to create a form which when submitted 'spits' out the response right on that same page, no more redirects!
