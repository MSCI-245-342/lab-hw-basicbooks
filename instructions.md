# Rails CRUD - The BasicBooks App

This lab and homework assignment are designed to get you familiar with:
+ Initializing a new Rails app
+ The structure of Rails apps
+ Creating a model
+ Creating dev data
+ How to return a simple HTML page
+ How to return data from the database
+ How to POST an HTML FORM and view the data in Rails

## Lab and Homework

This assignment is part lab and part homework.  You are expected to work with your team at least through getting Rails up and running and committed to your repository before the end of lab.  If you finish this before the end of lab, you are welcome to continue working with your team on the homework until the end of lab.  Once lab is over, you should continue working on the homework independently.  Remember to appropriately acknowledge any assistance given or received as part of lab on your homework submission.

## Learning Web Frameworks

Rails is an industrial strength web framework.  Shopify is built with Rails.  GitHub is built with Rails.  Airbnb is on Rails.  And so forth.

With this power comes an additional does of complexity.  The complexity comes from Rails having many moving parts, and from the enforcement of the model-view-controller (MVC) design pattern.  MVC is extremely useful for managing the design of apps, but it will seem strange at first, and it will be challenging to keep track of everything that is going on.

While I will try to guide you in the most efficient manner to learning the critical bits you need to know, there is a tremendous amount of knowledge needed to become a successful engineer of web apps with a web framework.  You will need to develop an ability to turn to other books, manuals, and websites to learn what you need to know.  This is the life of a professional engineer.  The professional engineer always needs to learn more, and you must develop the ability to learn from reading and then doing.

The following book is the most helpful and is availble via the library:

1. [Learning Rails 5](https://ocul-wtl.primo.exlibrisgroup.com/permalink/01OCUL_WTL/5ob3ju/alma999986583426005162). While this is about Rail 5, and we're using Rails 6, almost everything is the same between Rails 5 and 6 at the level we will do work in MSCI 245 and 342.  In chapter 6, the book uses `form_for` rather than `form_with`, but other than their names, there is very little different between them.  Rails combined the functionality of `form_tag` and `form_for` into one new form method called `form_with`.  Certainly there are some other differences, but they are not significant to the concepts explained in the book, which are the important things to learn. The [course textbook](http://www.saasbook.info/) unfortunately is Rails 4 and is getting out of date on several details about Rails.  The textbook is good for learning conceptual knowledge, but for actually programming of Rails, refer to more recent sources.  Always be aware of which version of Rails somone is providing advice about.  

There is also important documentation that you are going to need to refer to:

1. Guide: [Active Record Basics](https://edgeguides.rubyonrails.org/active_record_basics.html)

1. Guide: [Active Record Query Interface](https://edgeguides.rubyonrails.org/active_record_querying.html)

1. Guide: [Active Record Migrations](https://edgeguides.rubyonrails.org/active_record_migrations.html), References: [Schema Definitions](https://api.rubyonrails.org/v6.0.3.2/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html) and  [table-definition (inside the do block of create_table)](https://api.rubyonrails.org/v6.0.3.2/classes/ActiveRecord/ConnectionAdapters/TableDefinition.html)

The following book is written in a tutorial style, which impedes its use as a source of information, but it is very good if you want to see step by step instructions and well written explanations:

1. [Ruby on Rails Tutorial, 6th Ed](https://ocul-wtl.primo.exlibrisgroup.com/permalink/01OCUL_WTL/1jjglgg/alma999986595715005162)

The following may be useful to you, but "Learning Rails 5" plus the Rails Guides will likely suffice:

1. [The Rails 5 Way, Fourth Ed.](https://ocul-wtl.primo.exlibrisgroup.com/permalink/01OCUL_WTL/5ob3ju/alma999986579602405162)

1. [Agile Web Development with Rails 6](https://ocul-wtl.primo.exlibrisgroup.com/permalink/01OCUL_WTL/5ob3ju/alma999986618645205162)

### Advice from fellow students

One problem with these assignments in MSCI 245, and with software tutorials in general, is that the pressure of getting work done can lead to skimming the content and trying like mad to just copy and paste code as fast as possible until the assignment is done.  

In MSCI 342, I asked students what advice they had for MSCI 245 students.  The most common piece of advice was to make sure you understand what you are doing rather than copying and pasting.  When a homework assignment shows you how to do something, you need to understand why you're doing it.  As one student said, if you robotically copy and paste, you'll come to regret not acquiring the knowledge, for it will be needed on exams, the final project, and for all of MSCI 342.

# Getting Rails up and running

You are reading these directions on Codio having cloned the repository to a directory named `basicbooks`.  First:

```
cd basicbooks
```

**STOP!** Double check that you are in a directory named `basicbooks`.  Do:
```
pwd
```
to "print working directory" and see that the path shown ends with `/basicbooks`.

*If you are not in a directory named* `basicbooks`, go back to the homework instructions and make sure you have correctly cloned the repository as shown.  Everything depends on you getting this right.  

### You are in the repository directory `basicbooks`

Now, copy and paste the following and run it from the command prompt (unless otherwise noted, these commands will always be run from the command prompt, and I won't keep reminding you where to run them).

**Warning:** This is a very long command.  Students often fail to copy the entire command, which messes stuff up.  Be sure you carefully copy the whole command.

```
rails new . --database=postgresql --skip-javascript --skip-turbolinks --skip-action-mailer --skip-action-mailbox --skip-action-text --skip-active-storage --skip-action-cable --skip-spring --skip-bundle 
```

The `rails new .` creates your new app in this directory.  This directory is called the **app root** directory for the new app.  The name of your directory is important because it will be used as the name of the app and will prefix the names of the development and test databases.

In the Codio setup for MSCI 245 and MSCI 342, we do not have a good way to test web apps built using javascript.  Thus, both `--skip-javascript` and `--skip-turbolinks` are used to disable parts of Rails that depend on javascript.  The other "skip" options are to exclude parts of Rails you are unlikely to need to use and which simply clutter up your app and make learning Rails harder. 

Then, open up the `Gemfile` and comment out the `jbuilder` and `tzinfo-data` gems.  To comment out a line, place a `#` character at the start of the line as such:

```ruby
# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
#gem 'jbuilder', '~> 2.7'
```
and
```ruby
# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
#gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
```

Then, in the terminal, at the command prompt:

```
 bundle install
```
This may take several minutes to run.

The command `bundle` looks at the Gemfile and downloads and installs the Ruby gems needed for your Rails app.  It places detailed dependency info into a file named Gemfile.lock.  These files capture the specific versions of the software needed to make sure your app works as you have designed and tested it.  We always keep our Gemfile and Gemfile.lock files in our git repository.  Whenever you change or add a gem to your Gemfile, you need to run `bundle install` again.

Next, add the following to `config/environments/development.rb` after "`Rails.application.configure do`":

```ruby
config.hosts << /[a-z0-9]+\-[a-z0-9]+\-3000\.codio\.io/
```

The above is needed to allow us to view our web app while in development mode on the Codio server.  Each student gets their own Codio server, which is a linux machine running in the Amazon cloud.  Unlike MSCI 240, where it might have been encouraged for you to locally develop your code on your personal computer, the environment configuration needs in MSCI 245 and 342 are so significant, that you should be doing all of your work on Codio.  Do not waste your time trying to get Rails and Postgresql to run on your personal computers.

While we will not do much with automated testing in MSCI 245, our Rails app is configured to work with [Minitest](https://github.com/seattlerb/minitest).  When we make projects in MSCI 245 and 342, we will always make the following configuration changes to make testing work better for us on Codio.

In `test/test_helper.rb` comment out:

```ruby
# parallelize(workers: :number_of_processors)
```

By commenting out `parallelize(workers: :number_of_processors)`, this will force our automated tests to run 1 at a time.  This is very handy if we want to use the byebug debugger to debug tests or see how testing works.  

In `test/test_helper.rb` also comment out:

```ruby
#fixtures :all
```

The use of fixtures, for testing, complicates our work, and we'll avoid using them.

In `test/application_system_test_case.rb`, comment out: 

```ruby
driven_by :selenium, using: :chrome, screen_size: [1400, 1400]
```

and add:

```ruby
driven_by :rack_test
```

So, you'll end up with:

```ruby
#driven_by :selenium, using: :chrome, screen_size: [1400, 1400]
driven_by :rack_test
```

The `:rack_test` driver cannot process javascript, but it runs very quickly.  The issue with using `:selenium` and Chrome as our system test driver is that I haven't been able to get these components to install correctly on Codio.  Projects in MSCI 342 should not use javascript, and so this will not be an issue.

Then create a file in the basicbooks directory named `Procfile` and put this command in the file as per the [heroku instructions](https://devcenter.heroku.com/articles/deploying-rails-applications-with-the-puma-web-server):
```
web: bundle exec puma -C config/puma.rb
```

Then do:

```
rails db:create db:migrate
```

This will create your databases.  You should see output:
```
Created database 'basicbooks_development'
Created database 'basicbooks_test'
```
You should never directly access your `basicbooks_test` database, which is used by the testing tools. 

You will and should often look at your development database.

Let's look at the development database.

To do this, we use psql, which is the command line interface to Postgresql. 

To login to our database, we do:
```
psql -d basicbooks_development
```
To see all the commands in psql, we do `\?`.  Try it.  Press the space bar to page through them all.  Press `b` if you want to scroll up.  When you get to the end, press `q`.  The key presses stand for "back" and "quit".  Memorize them.

To list the tables, enter `\d`.  You should see:

```
               List of relations
 Schema |         Name         | Type  | Owner
--------+----------------------+-------+-------
 public | ar_internal_metadata | table | codio
 public | schema_migrations    | table | codio
(2 rows)
```

These are tables used by Rails.  Don't mess them up.

To escape from psql, enter `\q`.

### Checking that your install works

Run:

```
rails server -b 0.0.0.0
```

You will see that we are using the Puma webserver and that it is running on port 3000. 

At the top of your Codio window, you will see a dropdown menu titled "Project Index (static)". Click the white downward pointing arrow and select "Box URL". You will be transported to a new browser tab and you should see a message that says "Yay! You're on Rails!".  

If you don't get the "Yay!" message, now is the time to figure out what you didn't do correctly above.  You can open multiple terminals in Codio.  This allows you to do work in one terminal while your server runs in the other terminal.

You can shutdown your server by typing CTRL-C.  Usually the server will pick up changes to your code automatically, but configuration changes are unlikely to be picked up.  You can always stop your server with CTRL-C and start it running again if you have any doubt.

Once you get your install working, it is time to commit all of this code to the repository:
```
git add --all
git commit -m"Yay! I am on Rails!"
git push
```
We will be checking for your "Yay" commit message, and so please use the message as per above.  

I encourage you to go and check out your repository in GitHub, but please **never** directly edit any of your files via GitHub.  Please always edit them via your repository in Codio.  (If you do edit in GitHub, usually the correct fix is to do a `git pull` from Codio, but please, let's avoid the issue all together.)

### End of Lab

Everyone is expected to have made it to here before the end of lab.

## Before proceeding

If you are not caught up on the course lectures, you should go watch them first before doing more of the homework.  The lectures cover the concepts that you are going to be putting into practice in the homework.  

## Our BasicBooks App

Our BasicBooks App is going to be very basic.  It will allow us to view books in the database, and to experiment with POSTing data.

Well, we know that Rails apps are based on the MVC pattern (Model, View, Controller), and so it seems pretty sensible to figure out what the model(s), view(s), and controller(s) are going to be.  As you'll see as we go through this, we don't do them separately except for the model.  It works best for us to go back and forth between the controller and the views as we build the app.  This let's us test it as we progress in getting it up and running.  When we do development, we want to follow this process:

1. Write a bit of code or make a small change to the app.

1. Check that the app still works and/or does what we expect the new code to do.  If the app is broken or buggy, work on the app to fix it.  Do not add more functionality or other changes until you are back to a working app.  If the app is working, go to step 1 and add some more code.

### Model Making

Our app is going to have a very simple schema.  We will have a single entity set: books.  Each book has a title, an author, and our personal rating from 1 to 5.  This app is our personal app for keeping tracking of books and our opinion of them.  

We can ask Rails to generate a model for us.  When we ask for a model, we use the form of the entity name in CamelCase, i.e. Book not books.  

To make the model do:

```
rails generate model Book title:string author:string rating:integer
```
You'll get the following output:
```
      invoke  active_record
      create    db/migrate/20210625040017_create_books.rb
      create    app/models/book.rb
      invoke    test_unit
      create      test/models/book_test.rb
      create      test/fixtures/books.yml
```
You can ignore the files created in the `test` directory.  You will have a different number in front of your _create_books.rb file.  That number is a timestamp.

What you've done is make a "migration". This is a ruby script for making changes to the database. The beauty of this is that all of our work on the database is recorded in scripts that can be replayed to build a system exactly the same way on other machine, for example in our deploy version in the cloud on Heroku.

The migration can be found in `db/migrate/` in the specific file output in your terminal. Go open that file, and you will see:

```ruby
class CreateBooks < ActiveRecord::Migration[6.1]
  def change
    create_table :books do |t|
      t.string :title
      t.string :author
      t.integer :rating

      t.timestamps
    end
  end
end
```

Who needs stinkin' SQL DDL?  Even though you don't know the syntax above, you should be able to recognize that this is very similar to creating tables in SQL.  We didn't ask for a `t.timestamps` column, but Rails is going to use this to make some columns that it needs.

In addition to the migration, we also got our model created in `app/models/book.rb`.  If you open that file, you'll see:

```ruby
class Book < ApplicationRecord
end
```

Which is pretty simple.  The `Book` class inherits from ApplicationRecord. Read all about [ActiveRecord and ApplicationRecord](https://guides.rubyonrails.org/active_record_basics.html).

While we've made a migration, we haven't used it yet to change the database.  To add the table to the database, do:
```
rails db:migrate
```
which runs all migrations not yet run.  You will see a message saying that `create_table(:books)` was run.

Let's go and look into the database and see what happened:
```
psql -d basicbooks_development
```
The in psql, type `\d` to see the tables:
```
basicbooks_development=# \d
                List of relations
 Schema |         Name         |   Type   | Owner 
--------+----------------------+----------+-------
 public | ar_internal_metadata | table    | codio
 public | books                | table    | codio
 public | books_id_seq         | sequence | codio
 public | schema_migrations    | table    | codio
(4 rows)
```
Cool, eh?  We now have a books table and a books_id_seq sequence.  In postgresql, sequences are used to maintain a record of unique ids.  Don't mess with books_id_seq.

To describe the books table, enter `\d books`:
```
                                          Table "public.books"
   Column   |              Type              | Collation | Nullable |              Default              
------------+--------------------------------+-----------+----------+-----------------------------------
 id         | bigint                         |           | not null | nextval('books_id_seq'::regclass)
 title      | character varying              |           |          | 
 author     | character varying              |           |          | 
 rating     | integer                        |           |          | 
 created_at | timestamp(6) without time zone |           | not null | 
 updated_at | timestamp(6) without time zone |           | not null | 
Indexes:
    "books_pkey" PRIMARY KEY, btree (id)
```
We see that our Book model (singular Book) produces an entities table books (plural).  This is a Rails convention, and it is really nice.  The Book model will represent a row in the table, i.e. a single book.  The table, is a collection of entities, and thus it is named `books`.   You can also see how Rails by default gives each entity a unique id name `id`.  There are time extra columns in here that Rails needs: created_at and updated_at.  We don't ever directly manipulate these columns.  Also, we can see that Rail went ahead and put an index on our primary key (the `id` attribute).

Press `q` to exit the display of the table.

Enter `\q` to exit psql.

Now that we checked out our model in the database, we realize that the table allows the title, author, and rating fields to be null.  We want to set these columns to be `not null`.

When we run `rails db:migrate` and realize that we didn't mean to actually do the migration, we can undo the operation with `rails db:rollback`.  Do that now:
```
rails db:rollback
```
You should see a message telling you that you've reverted the "CreateBooks" migration and that it has dropped the books table.

Let's edit the migration.  Find it in `db/migrate` and change it to be:
```ruby
class CreateBooks < ActiveRecord::Migration[6.1]
  def change
    create_table :books do |t|
      t.string :title, null: false
      t.string :author, null: false
      t.integer :rating, null: false

      t.timestamps
    end
  end
end
```
What we're doing above is supplying options to the creation of the columns.  You can see all the options in the [docs for the `add_column` method](https://api.rubyonrails.org/v6.1.3.2/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-add_column).

Now rerun the migration:
```
rails db:migrate
```

Go into the database with `psql -d basicbooks_development` and verify that the books table now has not null constraints on the columns.

### Dev Data

It it handy for development to get some data in the database before proceeding.

Rails maintains 3 different environments: development, test, and production.  The development environment is setup for us to write code and play around with our database as needed.  We'll put data in the database in ways that help us develop the app faster.  The test environment is specially for the automated tests to use.  We do not touch the test database.  The production environment is for when we deploy our app to a server for others to use.  The only data we want to add to  the database for the production environment is the data the app would need for proper functioning.  We don't want "dev data" in our production database.  

We can achieve the goal of adding in dev data as we want, with keeping the production database clean with careful use of Ruby's database `db/seeds.rb` file.  The `seeds.rb` file is just Ruby code that is run when we execute the command `rails db:seed`.

First, edit the file to look like this:
```ruby
# This file should contain all the record creation needed to seed the database with its default values.
# The data can then be loaded with the rails db:seed command (or created alongside the database with db:setup).
#
case Rails.env
when "development"
  # add dev data here
when "production"
  # no seed data for production
end
```

The Book model, is a class that inherits all the functionality of a `ApplicationRecord` class.  This means that it has a `create` method that we can use to create new books in the database.  https://guides.rubyonrails.org/active_record_basics.html

Now, edit `db/seeds.rb` to be:

```ruby
# This file should contain all the record creation needed to seed the database with its default values.
# The data can then be loaded with the rails db:seed command (or created alongside the database with db:setup).
#
case Rails.env
when "development"
  Book.create( title: "Dune", author: "Frank Herbert", rating: 5 )
  Book.create( title: "Dandelion Wine", author: "Ray Bradbury", rating: 0 )
  Book.create( title: "The Hitchhiker's Guide to the Galaxy",
               author: "Douglas Adams", rating: 4 )
  Book.create( title: "James and the Giant Peach", author: "Roald Dahl", rating: 5 )
  Book.create( title: "Charlie and the Chocolate Factory", author: "Roald Dahl", rating: 3 )
  Book.create( title: "Matilda", author: "Roald Dahl", rating: 2 )
  Book.create( title: "The Lord Of The Rings", author: "J.R.R. Tolkien", rating: 0 )
  Book.create( title: "Ender's Game", author: "Orson Scott Card", rating: 4 )
  Book.create( title: "Dune", author: "Frank Herbert", rating: 5 )
  Book.create( title: "Slaughterhouse-Five", author: "Kurt Vonnegut", rating: 3 )
  Book.create( title: "Snow Crash", author: "Neal Stephenson", rating: 3 )
  Book.create( title: "Cryptonomicon", author: "Neal Stephenson", rating: 5 )
when "production"
  # no seed data for production
end
```

Save the file and then back in the terminal, do:

```
rails db:seed
```

to run the code.

Let's go look in psql and see that this worked:
```
psql -d basicbooks_development
```
Then we can run sql code directly from the prompt:
```
basicbooks_development=# select id, title, author, rating from books ;
 id |                title                 |      author      | rating 
----+--------------------------------------+------------------+--------
  1 | Dune                                 | Frank Herbert    |      5
  2 | Dandelion Wine                       | Ray Bradbury     |      0
  3 | The Hitchhiker's Guide to the Galaxy | Douglas Adams    |      4
  4 | James and the Giant Peach            | Roald Dahl       |      5
  5 | Charlie and the Chocolate Factory    | Roald Dahl       |      3
  6 | Matilda                              | Roald Dahl       |      2
  7 | The Lord Of The Rings                | J.R.R. Tolkien   |      0
  8 | Ender's Game                         | Orson Scott Card |      4
  9 | Dune                                 | Frank Herbert    |      5
 10 | Slaughterhouse-Five                  | Kurt Vonnegut    |      3
 11 | Snow Crash                           | Neal Stephenson  |      3
 12 | Cryptonomicon                        | Neal Stephenson  |      5
(12 rows)
```
Yay!  

Type `\q` to exit psql.

You can gain some experience with the Book model and how ActiveRecords work by using the rails console.  The rails console is just like irb, but it knows all about our Rail app automatically.

You can safely play around with the database by running rails console with the option --sandbox.  Any changes you make will be rolled back when you exit the console. Do:
```
rails console --sandbox
```
Then do:
```
Book.all.limit(2)
```
To ask the Movie model for all of the movies.  Notice how this is turned into SQL for you: `SELECT "books".* FROM "books" LIMIT $1  [["LIMIT", 2]]`.

To find the book with an id of 1, do:
```
Book.find(1)
```
You'll see that the method runs the SQL command: `SELECT "books".* FROM "books" WHERE "books"."id" = $1 LIMIT $2  [["id", 1], ["LIMIT", 1]]`.  

To print out all book titles, do:
```
Book.find_each { |b| puts b.title }
```
To delete the book with id=1, do:
```
Book.destroy(1)
```
and then list the movies again to verify it is gone:
```
Book.find_each { |b| puts b.title }
```
Type `quit` to exit the console.

## RESTful routes for books

If you haven't done it recently, now is a good time to commit your repo and push to GitHub.  This gives you a backup in case of disaster.

You can see the routes for our app by doing:
```
rails routes
```
As you can see, we are lacking in the routes department.  For our app to do anything, we need routes that a user can go to, which are then handled by our controller (to be made), which then renders our views (also to be made).

Routes are kept in `config/routes.rb`.  Open the file up.

Right now it is pretty sparse:
```ruby
Rails.application.routes.draw do
  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```

When we have an entity like books, Rails calls them a **resource**.  Rails provide a shortcut for making routes for resources.  After the `do`, and before the `end` in the `routes.rb` file, add:
```
resources :books
```
Save the file, and then run:
```
rails routes
```
We'll now have lots of routes:
```
   Prefix Verb   URI Pattern               Controller#Action
    books GET    /books(.:format)          books#index
          POST   /books(.:format)          books#create
 new_book GET    /books/new(.:format)      books#new
edit_book GET    /books/:id/edit(.:format) books#edit
     book GET    /books/:id(.:format)      books#show
          PATCH  /books/:id(.:format)      books#update
          PUT    /books/:id(.:format)      books#update
          DELETE /books/:id(.:format)      books#destroy
```
These are all important.  The GET /books route says it is handled by the books controller's index action.  It is considered the "default" handler, in that it is run when a user requests /books.  Usually, we have the index provide an overview of the resource, and often provide a list of the items.  For us, that would be a list of the books in the database.

Notice the routes that include an ":id".  For example GET movies/1 will be a request to show the movie with id=1.  You can ignore the "(.:format)" in these routes.

The "Prefix" means that Rails will make available in the controller, and the view, special helper methods that will return the path for the route.  For example there will be `books_path` and it will return "/books" and `new_book_path` will return "/books/new".  It is much better practice to call these helper methods rather than type the path directly.  In addition to these "_path" methods, there are also made "_url" methods, for example: books_url, new_book_url, etc.  These return the full url to the web page, for example: https://lola-concert-3000.codio.io/books .  We'll most often use the "_path" methods to produce relative paths.  The "_url" methods are used when we need to do a "redirect" in the controller.

# 3. A controller and views for movies.

We can ask Rails to make us a controller with the actions we need.  For a resource controller, we also use the plural form of the resource.  Do:
```
rails generate controller books index create new edit show update destroy --skip-routes
```
This gives us lots of good stuff:
```
      create  app/controllers/books_controller.rb
      invoke  erb
      create    app/views/books
      create    app/views/books/index.html.erb
      create    app/views/books/create.html.erb
      create    app/views/books/new.html.erb
      create    app/views/books/edit.html.erb
      create    app/views/books/show.html.erb
      create    app/views/books/update.html.erb
      create    app/views/books/destroy.html.erb
      invoke  test_unit
      create    test/controllers/books_controller_test.rb
      invoke  helper
      create    app/helpers/books_helper.rb
      invoke    test_unit
      invoke  assets
      invoke    scss
      create      app/assets/stylesheets/books.scss
```      
Each "create" above is a new file that has been created.  We now have a controller in `app/controllers/books_controller.rb` and we have views in `app/views` made for each of the controller's actions.  There is even more, but we can ignore this other stuff for now.

Take a look at `books_controller.rb`.  You'll see in it a class that inherits from ApplicationController and has empty methods for each of the actions we requested when we generated the controller.

Edit your controller to look like this:
```ruby
class BooksController < ApplicationController
  def index
    byebug
  end

  def create
    byebug
  end

  def new
  end

  def edit
  end

  def show
  end

  def update
  end

  def destroy
  end
end
```
We've added `byebug` to the index and create methods.  Recall that we have these routes defined that are for `/books`:
```
   Prefix Verb   URI Pattern               Controller#Action
    books GET    /books(.:format)          books#index
          POST   /books(.:format)          books#create
etc.
```
The routing decides which code to call depending on the HTTP request "Verb" and the URI Pattern.  If there is a GET request for `/books`, then the we will run the code in the `index` method of BooksController.  If it is a POST request fo the same path of `/books`, then we'll call the `create` method of the BooksController.  

Lets run the webserver and request `/books` in the browser, and see where the debugger stops us.  Do:
```
rails server -b 0.0.0.0
```
Use the Codio menu and to to the "Box URL".

Now, you will see you are at a url like "https://lola-concert-3000.codio.io/" but with a different hostname.  Append to the browser's url "/books" and hit the enter key.

The browser will sit there and spin.  Go back to Codio.

In the terminal where you started the server, you will see that you've dropped into the debugger!  This is so, so, cool.  

In Rails, you can place a `byebug` just about anywhere and debug what is going on with your code.  You can put `byebug` into any view, model, or controller.  This is a super powerful technique for debugging and just trying to figure out what Rails does.

You should see that we're in the `index` method:
```
[1, 10] in /home/codio/workspace/basicbooks/app/controllers/books_controller.rb
    1: class BooksController < ApplicationController
    2:   def index
    3:     byebug
=>  4:   end
    5: 
    6:   def create
    7:     byebug
    8:   end
    9: 
   10:   def new
(byebug) 
```

So, this tells us that when we request a URL with our web browser, the default is a GET request.  We will use HTML forms to generate POST requests.  

To exit the debugger, just type "continue".

Remove the byebug's from BooksController.

If you've stopped your webserver, start it back up again, and go to `/books` again.

You'll see a page that says:
```
Books#index

Find me in app/views/books/index.html.erb
```

Go open up `app/views/books/index.html.erb`:
```html
<h1>Books#index</h1>
<p>Find me in app/views/books/index.html.erb</p>
```
and we see the html that got displayed.  

Rails pairs up a view by default with controller actions (methods).  The BooksController's `index` method by default will "render" the view in `app/views/books/index.html.erb` at the end of the `index` method.  Likewise the BooksController's `create` method is going to render the view `app/views/books/create.html.erb` once the `create` method has exited.  

Okay, let's work on our controller.  Open up `app/controllers/books_controller.rb`.

We said that the index view should produce a list of books.  Remember that the controller mediates between the model and the view.  So, in the index action handler, we should ask the Book model for all of the entries and put them in an instance variable for the view to use:
```ruby
  def index
      @books = Book.all
  end
```
Remember that the default view to render at the end of an action is the view with the same name as the action.  So, open up `app/views/books/index.html.erb` and change it to loop through the books and display their titles:
```html
<h1>Books</h1>
<ul>
<% @books.each do |book| %>
  <li><%= book.title %></li>
<% end %>
</ul>
```
The above file is an [ERB template](https://guides.rubyonrails.org/action_view_overview.html#templates). ERB allows us to run ruby code between the `<% %>` and `<%= %>` tags.  Whatever is not inside these tags is simply printed out as the output of the view.  The `<% %>` tags are used for code that should not have its value printed out.  The `<%= %>` tags run the code inside them and then print out the value of the result.  Note that "puts" and "print" do not work in ERB.

The view has access to the `@books` instance variable we made in the controller.  Then we use a simple loop intermixed with simple html to make our list.

Go to /books on the website and see that it works.

For the 'show' action, recall that the route will be /books/id where id is a number.  Rails will grab the number and put it in the params hash with the key `:id`.  Let's see if this is true.

In the controller, put the following in the show action handler:
```
  def show
      byebug
  end
```
Now, you should still have a terminal with the puma webserver running.  After you go to /books/42 in the browser, go back to that terminal, and you should see:
```
Processing by BooksController#show as HTML
  Parameters: {"id"=>"42"}
Return value is: nil

[12, 21] in /home/codio/workspace/basicbooks/app/controllers/books_controller.rb
   12:   def edit
   13:   end
   14: 
   15:   def show
   16:     byebug
=> 17:   end
   18: 
   19:   def update
   20:   end
   21: 
(byebug) 
```
and we've been dropped into byebug.  To see what is in `params`, type `params` at the byebug prompt:
```
(byebug) params
#<ActionController::Parameters {"controller"=>"books", "action"=>"show", "id"=>"42"} permitted: false>
```
So, we see that it knows the controller is books, and the action is show, and id has been set to 42.  Try typing `params[:id]` and `params["id"]
```
(byebug) params[:id]
"42"
(byebug) params["id"]
"42"
```
These ruby symbols, e.g. :id, behave like immutable strings for hashes in Rails.  So, :id and "id" work the same as a key for the params hash.  Ruby convention is to use the symbols, e.g. `:id`.

Now, type `continue` to let the server finish processing the request.

As mentioned before, being able to debug in this fashion is super powerful.  

Okay, back to the show action and show view.  In the controller, let's get the movie requested:
```ruby
def show
      @book = Book.find params[:id] 
end
```
and in the view (app/views/books/show.html.erb), we'll show this book:
```erb
<h1>Book with id = <%= @book.id %></h1>
<table>
    <tr><td>Title:</td><td><%= @book.title %></td></tr>
    <tr><td>Author:</td><td><%= @book.author %></td></tr>
    <tr><td>Rating:</td><td><%= @book.rating %></td></tr>
</table>
```
Try it out by going to /books/1 , /books/2, etc. in your browser.

### New and Create

The BooksController#new method will cause the app/views/books/new.html.erb view to be rendered.  This view's job is to provide an HTML FORM that we can fill out to add a new book to the database.

In Rails, we need to use the tools Rails provides for creating forms, or we'll have problems.  We do **not** hack out our own HTML forms.  By using the Rails tools, we gain all sorts of security protections that Rails has already figured out.

To create a form, we use the following code in our `app/views/books/new.html.erb` file:
```erb
<h1>Add a Book to the DB</h1>

<%= form_with( model: @book, local: true) do |form| %>
    <!-- Insert into here the form buttons, etc.  We'll get to these in a moment. -->
<% end %>
```
The `<h1></h1>` tags are an HTML heading. The `<%= %>` tags run some ruby code and print out the value returned.  The `<% %>` tag without the equals sign, just lets us have ruby code without any output, and that is why the "end" statement is inside `<% %>`.

The code we're running here is the "form_with" method.  We're passing it a value for the  parameter "model:", and the value is `@book`.  What is this `@book`?  The `@` symbol tells us it is an instance variable, which means it must be from the BooksController.  When creating a new book, we supply the `form_with` a model object that **has not yet been saved to the database**.  Rails then uses its knowledge of the model, its name, and the routes in `routes.rb` to know that this form should be submitted (POSTed) to `/books`. 

The `local: true` option disables use of AJAX for submitting the form.  We will always use `local: true` because we are creating web apps without javascript.  If you forget to use `local: true`, you'll break automated testing.

Go ahead and edit your new.html.erb view to look like the above.  

We need to create the `@model` object in the BooksController's new method.  Edit the BookController's `new` method to look like:
```ruby
  def new
    @book = Book.new
  end
```

Then, be sure your webserver is running and go to `/books/new` in your web browser.  All you should see is "Add a Book to the DB" on the screen.  Didn't our code work?

To see the HTML that what was actually produced by our view, right click in the window and select "View Page Source".

You can see that there is a lot that Rails is producing for such a simple page!

Views in Rails are at least a two step process.  First, the ERB code in `app/views/layouts/application.html.erb` is run:
```erb
<!DOCTYPE html>
<html>
  <head>
    <title>Basicbooks</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```
In the above code, is the template for which all of our views use in our application.  The ERB code in our books' views are run at the point where the above code calls `yield`:
```erb
  <body>
    <%= yield %>
  </body>
```
Thus, all of our views render themselves into the HTML body of the web page.  If you want to change the look of every page in your app, editing the application.html.erb page is one way to do it.  

Go ahead and edit your application.html.erb page to give your app a title on every page of "Your Name's BasicBooks App".  For example, I'd edit mine to be "Mark Smucker's BasicBooks App".

Alright, so lets go back to looking at the HTML produced by our new.html.erb view.  Our `form_with` is producing the following HTML:
```html
<form action="/books" accept-charset="UTF-8" method="post"><input type="hidden" name="authenticity_token" value="q_LGNzt5W9Tu8GeI910AGpcJ8eVgB2QPAzyT6ZXTjf7qEMgkgnSKtWB6Gtc93aBMi_RWayql4JQ44sjKh0105w" />
</form>
```
We can see the form will POST to "/books".  The "authenticity_token" is to avoid hacks.  When we use Rails properly, we get leading edge website security features.  Do not hack up your own html forms!

Okay, so we need to add some input fields to our form and a submit button.

We can read about how to add these elements, known as tag helpers, in the [ActionView::Helpers::FormHelper manual page](https://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html).  If you read this (you should), you'll see we can add text_field, number_field, and a submit as follows to our new.html.erb view:

```erb
<h1>Add a Book to the DB</h1>

<%= form_with(model: @book, local: true) do |form| %>
  <div>
    <%= form.label :title %>
    <%= form.text_field :title %>
  </div>

  <div>
    <%= form.label :author %>
    <%= form.text_field :author %>
  </div>

  <div>
    <%= form.label :rating %>
    <%= form.number_field :rating %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```
We match the label and fields with names that match the attributes of the model, e.g. title, author, and rating.  None of this is our choice if we want Rails to work smoothly.  Go with the flow, and do it the Rails way.

Make the above changes and then get `/books/new` again in your browser and view the html.

Most importantly, notice the input tags:
```html
    <input type="text" name="book[title]" id="book_title" />
```

```html
   <input type="text" name="book[author]" id="book_author" />
```

```html
    <input type="number" name="book[rating]" id="book_rating" />
```
The `name` for each one is of the form `book[attribute]` where attribute is replaced with title, author, and rating.  While the name is just a string in HTML, Rails has choosen to make this string look like a Ruby hash.

Okay, in your BooksController, add `byebug` to the `create` method:
```ruby
  def create
    byebug
  end
```
Then, fill out the form on the /books/new page in your browser with a title of "Animal Farm", author "George Orwell", and rating "3".  Submit the form.  Go back to Codio and you should be in the debugger:
```
Processing by BooksController#create as HTML
  Parameters: {"authenticity_token"=>"[FILTERED]", "book"=>{"title"=>"Animal Farm", "author"=>"George Orwell", "rating"=>"3"}, "commit"=>"Create Book"}
Return value is: nil

[3, 12] in /home/codio/workspace/basicbooks/app/controllers/books_controller.rb
    3:     @books = Book.all
    4:   end
    5: 
    6:   def create
    7:     byebug
=>  8:   end
    9: 
   10:   def new
   11:     @book = Book.new
   12:   end
(byebug) 
```
In byebug, enter `params` to view the contents of the params variable.

The params variable is of type `ActionController::Parameters` and is displayed to us as a hash.  The keys and values of the hash are:

+ authenticity_token" =>  some super long string
+ "book"=>{"title"=>"Animal Farm", "author"=>"George Orwell", "rating"=>"3"}
+ "commit"=>"Create Book", 
+ "controller"=>"books", 
+ "action"=>"create"

Of interest to us is that one of these key value pairs is another hash named `books`:

+ "title"=>"Animal Farm"
+ "author"=>"George Orwell"
+ "rating"=>"3"

We can gain access these values as follows (do this in the debugger):
```
(byebug) book_params = params.require(:book).permit(:title, :author, :rating)
#<ActionController::Parameters {"title"=>"Animal Farm", "author"=>"George Orwell", "rating"=>"3"} permitted: true>
(byebug) book_params[:title]
"Animal Farm"
(byebug) book_params[:author]
"George Orwell"
(byebug) book_params[:rating]
"3"
```
We use the `params.require(:book).permit(:title, :author, :rating)` call to say "we must have a `:book` key and the only permitted parameters for it are title, author, and rating.  This is a way for us to avoid people trying to hack us by posting invalid forms to our web app.

To exit the debugger, type continue.

Now that we know how to access the parameters POSTed to us, we can write the create method:
```ruby
  def create
    book_params = params.require(:book).permit(:title, :author, :rating)
    @book = Book.new(book_params)

    if @book.save
      redirect_to @book, notice: 'Book was successfully created.'
      return
    else
      render :new
    end
  end
```
Be sure to edit the existing create method and not just cut and paste in a new one!

Now go to your browser, go to `/books/new` and submit the form with your Animal Farm data and see what happens.

Cool, eh?

### Commit and push

If you haven't done it recently, commit and push your code to GitHub to back it up.

# More forthcoming

This homework will be updated and will contain more steps and actual work to hand in.  Once updated, this will be announced to Campuswire.



