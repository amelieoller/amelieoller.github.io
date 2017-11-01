---
layout: post
title:      "Insulation Quotes – My First “Real” Rails Application"
date:       2017-11-01 19:47:52 -0400
permalink:  insulation_quotes_my_first_real_rails_application
---


My first Ruby on Rails project turned out to be more challenging but also more fun than I expected. I wanted to build something that would actually serve a purpose and not just another to-do application.

The app lets you create quotes for insulation projects (I know, not the most exiting thing in the world but I built it for my husband’s company – hoping it’ll be used).

You can create a new quote with multiple applications (e.g. insulation in the wall/ceiling/floor) and add accessories to the quote. The quote will automatically calculate the type of insulation you should use for a specific application and sort it by which one is the most cost effective.

## Some things I learned building this app:
* Separation of concerns is important! Keep your code where it belongs when you’re following a MVC structure (in all fairness, I still need to work on that, but I’m taking one step at a time).
* Not to be redundant, but clean up your views (separate your concerns). Putting repetitive code into partials and helper methods will make your life so much easier, make it more readable, and cut down time when you want to add a new form field, for example.
* Make something work, then refactor. My main point being... refactor! It is important to make your code work like it should, it helps starting from the bottom and moving your way up but it is also important to take that “messy” code and clean it up. - Refactoring can actually be kind of fun!
* It really helps me to create a seed file so I can see what my data is doing and I can imagine what the app will look like with some real world data.

But most of all: Have fun with it! Especially if you’re doing a project you choose and you’re passionate about it’ll all come a lot easier to you.

[Link to the github repo.](https://github.com/amelieoller/insulation-quotes)
