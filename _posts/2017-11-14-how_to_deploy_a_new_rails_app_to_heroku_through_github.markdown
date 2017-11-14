---
layout: post
title:      "How to Deploy a New Rails App to Heroku Through Github"
date:       2017-11-14 22:10:07 +0000
permalink:  how_to_deploy_a_new_rails_app_to_heroku_through_github
---



How to Deploy a New Rails App to Heroku Through Github
The following article takes you through all the steps from initializing your new Rails app to deploying it to Heroku through GitHub. There are a few extra steps, e.g. adding bootstrap and creating pages with content, which are not essential to this process but make things look nicer.

## Use PostgreSQL as Your Database

When creating a new Rails application SQLite3 is the default database used. However you cannot use SQLite3 with Heroku, luckily for us, Rails also supports MySQL (including MariaDB) and PostgreSQL. Since PostgreSQL is the go-to database for Heroku, we will stick with that. To create a new Rails app and change the default database to PostgreSQL, type `rails new my-new-app --database=postgresql` in your terminal (replace ‘my-new-app’ with your apps name). `cd` into the new directory to get started.


![](https://i.imgur.com/YTZCDus.gif)

## Add Some Pages to Your App [optional]

Create whichever pages you like - this is just to add some content so we can see if everything is working correctly. I started out with a simple greeting on the home page. In `config/routes.rb` add `root 'welcome#home'` and generate a new welcome controller with `rails g controller welcome`. Add a `home` action to your WelcomeController and a `home.html.erb` in the `app/views/welcome` folder with whatever text you like.

Spin up a server with `rails s` and navigate to http://localhost:3000 to take a look at your new homepage.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_132578EB74DFFF7477D384C731B12DB70545F6A3CEF694B8DD483D80A8415074_1510445818780_Peek+2017-11-11+15-11+Add+some+pages+to+your+app.gif)

## Add Bootstrap Support [optional]

I like my applications to have at least a little styling from the start, to add bootstrap support simply add the following lines in these files:

- In `app/assets/javascripts/application.js` add:
    //= require jquery
    //= require jquery_ujs
    //= require bootstrap

before `//= require_tree .`.


- In `app/assets/stylesheets/application.css` add:
     @import 'bootstrap-sprockets';
     @import 'bootstrap';

to the bottom of the file and rename the file to have the extension `.css.scss`.


- Add these gems to your `Gemfile`:
    gem 'bootstrap-sass'
    gem 'jquery-rails'

and run `bundle install`.

To see if this worked start up a server with `rails s` and navigate to http://localhost:3000, you should see the font change.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_132578EB74DFFF7477D384C731B12DB70545F6A3CEF694B8DD483D80A8415074_1510696336635_Peek+2017-11-11+15-23+Add+bootstrap+support.gif)

## Move Your Files Into a GitHub Repo

Create a new repository on GitHub and copy its link. Run `git remote add origin https://github.com/your-name/your-new-app` (pasting your repo link) in your apps folder. Add all your files with `git add .` and commit with `git commit -m` `"``Initial commit``"` or whichever commit message you’d prefer. Push to Github with `git push origin master`. Next, we will link this repo to our Heroku app.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_132578EB74DFFF7477D384C731B12DB70545F6A3CEF694B8DD483D80A8415074_1510446037585_Peek+2017-11-11+15-26+Move+your+files+into+a+git+repo.gif)

## Deploy to Heroku

Go to https://dashboard.heroku.com/apps and sign up for an account if you don’t have one yet. Push the Create New App button , name your new Heroku app and create it, then choose GitHub as your deployment method and type in your repo name. Choose Enable Automatic Deployments if you wish and hit Deploy Branch. The deployment will run for a little while so be patient. After that’s done a View button will pop up, click on it and check out your masterpiece.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_132578EB74DFFF7477D384C731B12DB70545F6A3CEF694B8DD483D80A8415074_1510446046312_Peek+2017-11-11+15-30+Deploy+to+heroku.gif)

## Using a Database [optional but helpful]

To see how your app will run with some database content, create a new resource with `rails g resource Item name:string`. Go to your `config/database.yml` and find the name of your development database, e.g. `my_new_app_development`.

### Create a new Database

To create a new database in PostgreSQL, type the following in your terminal (make sure the database name ‘my_new_app_development’ matches the one in your database.yml file):

    sudo -u postgres psql
    postgres=# CREATE DATABASE my_new_app_development;

Close the session with `CTRL + d` and run `rake db:migrate`. Your database should be all set. To test everything out, create a new object in your rails console, `rails c`, e.g. `Item.create(name: 'Puzzle')`.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_132578EB74DFFF7477D384C731B12DB70545F6A3CEF694B8DD483D80A8415074_1510446081348_Peek+2017-11-11+15-44+Using+a+database+create+a+new+database.gif)

### Add Appropriate Views

Add some views to display your objects. Create an index action in your ItemController saving all your objects in an instance variable. Create a new index view in your `views/items` folder and iterate over your newly created instance variable to display your objects names for example.

Create a link to this page on your welcome home page `<%= link_to 'Item Index', items_path %>` for easier access. 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_132578EB74DFFF7477D384C731B12DB70545F6A3CEF694B8DD483D80A8415074_1510446211165_Peek+2017-11-11+16-00git+push.gif)

### ...Back to Heroku

Make sure you add, commit and push you new changes to GitHub. Now go back to your heroku app, if you have automatic deployment enabled, wait a while for everything to update and refresh your page, you should see your new content. In order to use the database on Heroku you have to run `rake db:migrate` in your Heroku console, then all your pages should work.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_132578EB74DFFF7477D384C731B12DB70545F6A3CEF694B8DD483D80A8415074_1510446060104_Peek+2017-11-11+16-02+go+back+to+heroku.gif)


Have fun creating your new live Rails app!

