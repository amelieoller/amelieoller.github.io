---
layout: post
title:  "How I Built a Small Ruby/Sinatra Web App (Favorite Places)"
date:   2017-09-25 18:13:45 -0400
---

Creating a Ruby/Sinatra web app from scratch isn’t the easiest thing in the world, especially because in order to create a well structured one you have to follow many conventions and rules. This is great news though, it makes your job easier, because you don’t have to make those decisions that were already made for you.

Here I explain roughly how I set up my app ([Favorite Places](https://github.com/amelieoller/favorite-places)), the tools I used and the concepts around it.

This app lets you sign up and create your favorite places(place name, city, country). You can view, edit and delete your own entries but only view other people's entries. To install the app:


1. Clone the repo
2. run `rake db:migrate`
3. run `shotgun` and open the provided link in your browser

# MVC

## MVC (Model-View-Controller)

It would be possible to create our application all in one file, with hundreds maybe thousands of lines of code in it - but that would get problematic quickly. You want to separate your application, so writing, reading and debugging becomes a lot easier and more pleasant - not just for you but possible contributors as well.

One popular *separation of concerns* structure is MVC or Model-View-Controller:

- Models: Models are the "brains” of your application, this is the place to manipulate your data.
- Views: Views provide the user interface of your application, everything the user can see and interact with is stored in your views.
- Controllers: Controllers are the layer between the views and the models, it connects the two and makes them talk to each other.

[More on the Model-View-Controller Structure.](https://blog.codinghorror.com/understanding-model-view-controller/)

These are the naming conventions for an MVC folder structure:

| **Component** | **Pluralization** | **Location**    | **File**             | **Constant**    |
| ------------- | ----------------- | --------------- | -------------------- | --------------- |
| Table         | plural            | Database        | songs                |                 |
| Model         | singular          | app/models      | song.rb              | Song            |
| Controller    | plural            | app/controllers | songs_controller.rb  | SongsController |
| Views         | plural            | app/views/songs | index.erb, show.erb… |                 |

## File/Folder Structure

When you are staring with a blank file, it’s always nice to have some kind of template to lean on, so you don’t loose your mind completely. The folder structure I am outlining here is pretty standard and not necessarily specific to the application I built, therefore it can be used for many different Sinatra web projects.

![Folder Structure](https://i.imgur.com/BAqihdf.png)


### The `app` Directory

This directory holds the main part of our application, it neatly contains our models, views, and controllers.


### The `models` Directory

This folder contains our models, each model file represents a component of your application - in this case User, Place, and Country. The application controller is what ties the other controllers together and is generally required for an application such as this one. It contains the `configure` section and `helpers`.


### The `views` Directory

This directory holds different views, which the user is going to see. The views are again grouped into folders for each component. The index and layout (provides a layout for all your erb files) files in the main directory are not specific to any component.

The views files are in the `[erb](http://www.stuartellis.name/articles/erb/)` [file format](http://www.stuartellis.name/articles/erb/) (Embedded Ruby) which allows you to write plane old html interspersed with Ruby elements.


### The `config` Directory

This contains your `environment.rb` file, connecting all of the files in our application to the appropriate gems and each other.


### The `db` Directory

This directory holds your database and database migrations. To create a new migration simply run `rake db:create_migration NAME=create_users` with the name to match your migration - and rake will create a migration for you with the appropriate time stamp.


### The `public` Directory

This holds the assets for your front end such as CSS styleheets, JavaScript files, and image files.


### The `spec` Directory

If you were to run test for your application, this is where they would be stored.


### The `config.ru` File

You need a `config.ru` when building Rack based applications. It loads your application environment, code, libraries, and specifies which controllers to load. 


### The `Gemfile`

This holds a list of all the gems that are required for the application. Running `bundle install` in your command line will install all the listed gems and dependencies. To create a new `Gemfile` simply type `bundle init` in your command line (make sure your’re in your projects folder).


### The `Rakefile` 

In the `Rakefile` you can specify your own rake tasks. To see all of the rake tasks that are available to you simply run `rake -T`.


### Other Files

You may want to add a `README.md` to your directory to help other programmers understand your application, figure out how to use it and learn how they may contribute. The `LICENSE.md` file contains your license. 


## CRUD

CRUD is an acronym for Create, Read, Update, and Delete, these are the four basic functions of [persistent storage](https://en.wikipedia.org/wiki/Persistence_(computer_science)).

**Create**
When you build a controller action in your model that renders a form to create a new instance of your model, that is the *create* part in Sinatra. 

**Read**
The *read* part is to show your user a specific instance of a class or all of them.

**Update**
A controller action that renders and update form and another that receives the information of the posted form, that would be our *update*.

**Delete**
If we destroy an instance of our class that would be the *delete* action. This, as opposed to the others is only displayed as a delete button on the users end (for a specific instance).

## Tools
### ORM/ActiveRecord

Databases can get pretty scary, that’s why we need help talking to them. Building our own methods to talk to our database is tedious and not necessary anymore - This is where ORM come in.

ORM or Object Relational Mapping is the part that sits between your database and your application. The convention is to map (or equate) ruby classes with database tables and the instances of those classes with the rows of gthe table. ActiveRecord is a Ruby library that does exactly that, it connects classes to relational SQL Databases.

So essentially ActiveRecord is an ORM that helps you deal with databases or as [rubyonrails.org](http://guides.rubyonrails.org/active_record_basics.html) explains it: “ActiveRecord is the M in MVC - the model - which is the layer of the system responsible for representing business data and logic.”

For this application I’m using the *sqlite3* database engine.

### Sinatra

Sinatra is a Domain Specific Language for writing web applications. It is dependent on Rack (which creates the interface behind Sinatra) and an alternative to other frameworks such as Ruby on Rails but much more light-weight. In a nutshell Sinatra provides us with pre-written methods that we can use to turn for example our CLI application into a web application.

### Git/Github

If you do decide to make your project public, I recommend using version control so other people can understand the changes you’ve made. Even if you don’t want anyone to see your code, it’s a great option for understanding your code after weeks, months or even years.

## Stumbling Blocks

One specific thing that I was trying to figure out for a while was how to delete a specific session message after you refresh a page. The problem I had was that upon refreshing a page and after a session message had already been loaded, it would just load again and again with each refresh. 

The solution ended up being a lot easier that I thought. Instead of using `@message = session[:message]` you simply write `@message = session.delete(:message)`. This will delete the session message with every refresh.



