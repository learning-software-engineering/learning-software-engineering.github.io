# Introduction to Ruby on Rails

## Objective
In this guide, we will cover how to set up a Rails application and introduce important knowledge about its layouts, architecture, and principles with examples.

## Prerequisite
This guide assumes that you have prior experience with Ruby, a programming language. You might find a steep learning curve if you dive straight into Rails.

Here are some useful resources to learn Ruby:
- [Official Ruby Website](https://www.ruby-lang.org/en/documentation/)
- [Ruby Tutorial For Beginners](https://www.rubyguides.com/ruby-tutorial/)

## What is Rails?
Ruby on Rails, often simply called 'Rails', a robust framework designed for developing web applications using the Ruby programming language. It shares a similar relationship with Ruby as Django does with Python, serving as a specialized toolset built upon its respective language. Rails stands out in the web development field because it is designed to follow two important principles (which will be introduced in the next section) --- "Don't Repeat Yourself" and "Convention Over Configuration". By adhering to these two principles, developers can write significantly less code to achieve the same, or even more, functionality than they would using other languages or frameworks. This efficiency is one of Rails' most significant advantages, allowing for quicker development of complex web applications without sacrificing quality or scalability.

## Two Major Principles in Rails
### Don't Repeat Yourself (DRY)
The DRY principle emphasizes having a single, unambiguous source of truth in a software system. By adhering to this principle, developers avoid redundancy, which not only makes the codebase more maintainable and less prone to errors but also makes it easier to modify or update the system. For beginners, this principle is particularly beneficial as it encourages understanding the underlying patterns and abstractions in programming, rather than just copying and pasting code. This leads to a deeper grasp of programming concepts and a cleaner, more efficient coding style.

### Convention Over Configuration
This principle advocates for predefined conventions to guide programming practices, rather than relying on extensive and often complex configuration files. By following established conventions, developers can rapidly progress with development without getting bogged down in configuring every aspect of the application. For beginners, this approach is especially advantageous as it reduces the learning curve associated with understanding configuration of applications. It allows them to focus on building functional parts of the application, making the process of learning Rails more intuitive and less overwhelming.

## Why Use Rails?
Rails is famous for its efficiency in building up an application. Developers can quickly set up the basic structure of an application since Rails provides pre-built structures and libraries (e.g., Active Record for database interactions and Action View for handling views). Therefore, developers are able to focus on the unique features of their software solution rather than figuring out the boilerplate code. The development process is significantly accelerated, which is invaluable in a fast-paced environment or when working on proof-of-concept projects. The next section will walk through the steps to quickly set up and develop a survey application.

## Quick Setup to Create a New Rails Application
### Installation Ruby, SQLite3, and Rails

1. To check if Ruby is installed. If not, please check [this website](https://www.ruby-lang.org/en/documentation/installation/) to download Ruby.
```bash
$ ruby --version
```

2. Check if SQLite3 is installed. If not, check [the SQLite3 website](https://www.sqlite.org/index.html) for installation.
```bash
$ sqlite3 --version
```

3. Install Rails using `gem install` command from RubyGems.
```bash
$ gem install rails
```
After installation, check if Rails is installed correctly.
```bash
$ rails --version
```

### Create a New Application
In this guide, we will create a application called Survey.
```bash
$ rails new survey
```
Then, we enter the folder called survey
```bash
$ cd survey
```
Inside survey folder, we expect to see the file structure looks like this (see more details on the purpose of each file [here](https://guides.rubyonrails.org/getting_started.html)): \
survey/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;app/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bin/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;config/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;config.ru \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;db/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Gemfile \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Gemfile.lock \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lib/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;log/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;public/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Rakefile \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;README.md \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;storage/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;test/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tmp/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;vendor/ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.gitattributes \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.gitignore \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.ruby-version

### Spin Up the Server!
To start the web server, enter this command:
```bash
$ bin/rails server
```
Now, open your browser and enter `http://localhost:3000`. You should see the default Rails page. Congratulations! You have started your first Rails Applicaiton successfully!

### MVC Architecture
Rails follows the Model-View-Controller (MVC) architecture, organizing the application into three interconnected layers. The Model defines the data entities in the application, the View is responsible for user interfaces, and the Controller defines the application's business logic. For more information on MVC, check out this article: [MVC: Model, View, Controller](https://www.codecademy.com/article/mvc). 

### "Hello World" in Rails
After understanding the concept of MVC, there is still one missing piece before we can make the application work: a route. A route maps a request to a controller, which then executes a series of actions in response to the request. Here is a useful article that explains what a route is: [Understanding Route in Software Development](https://reintech.io/term/understanding-route-in-software-development).

In the routes file provided by Rails, `config/routes.rb`, type the following code:
```ruby
Rails.application.routes.draw do
  get "/surveys", to: "surveys#index"

end
```
The route above defines the mapping between `GET /surveys` request and the `index` action in `SurveysController`.

To create the `SurveysController` with an `index` action, in the terminal, run this command (*Note: `--skip-routes` is included because the route has been defined.*):
```bash
$ bin/rails generate controller Surveys index --skip-routes
```
Rails will execute this command and create a bunch of files for you:
```
create  app/controllers/surveys_controller.rb
invoke  erb
create    app/views/surveys
create    app/views/surveys/index.html.erb
invoke  test_unit
create    test/controllers/surveys_controller_test.rb
invoke  helper
create    app/helpers/surveys_helper.rb
invoke    test_unit
```

Among those generated files, the most crucial one is the controller file, `app/controllers/surveys_controller.rb`.
```ruby
class SurveysController < ApplicationController
  def index
  end
end
```
Currently, the `index` action has no defined logic. In Rails, when an action does not explicitly render a view, Rails automatically renders the view that matches the controller name and action. This is an implementation of the Convention Over Configuration Principle. In this case, the `index` action will automatically render `app/views/surveys/index.html.erb`.

Next, replace the content in `app/views/surveys/index.html.erb` by the following codes:
```html
<h1>Hello, World!</h1>
```

Now, go to `http://localhost:3000/surveys` to confirm "Hello, World!" is displayed!

### Data Models
So far, we have briefly introduced View and Controller. In this section, we will demonstrate how to set up data models.

A model is a Ruby class that is used to represent data, and it can interact with the application's database through a feature of Rails called Active Record.

To store data of survey, we can use the following command to generate the model `Survey`:
```bash
$ bin/rails generate model Survey question:text
```
This command creates the following files:
```
invoke  active_record
create    db/migrate/<timestamp>_create_surveys.rb
create    app/models/survey.rb
invoke    test_unit
create      test/models/survey_test.rb
create      test/fixtures/surveys.yml
```
The two files we will focus on are `db/migrate/<timestamp>_create_surveys.rb` and `app/models/survey.rb`. One is for data migration and one is for the model.

After opening the migration file, you can see this:
```ruby
class CreateSurveys < ActiveRecord::Migration[7.1]
  def change
    create_table :surveys do |t|
      t.text :question

      t.timestamps
    end
  end
end
```
This chunk of code illustrates how to constructe the `survey` table. By default, the `create_table` method adds an `id` column as a primary key which can increment automatically. The first row would have `id` of 1 and second row would have `id` of 2, and so on.

One column is defined for `survey` table: `question`. And it is an text attribute as indicated by `t.text`. The last part `t.timestamps` would automatically define two additional columns, `created_at` and `updated_at`, which stores the creation time and update time.

To make all the fields defined effective, we need to run the following command:
```bash
$ bin/rails db:migrate
```

The following outputs indicate the success of migration:
```
==  CreateSurveys: migrating ===================================
-- create_table(:surveys)
   -> 0.0018s
==  CreateSurveys: migrated (0.0018s) ==========================
```
Now, we have finished building every piece in MVC.

## References
For more information on Rails, here are some useful websites:
- [Rails Guides](https://guides.rubyonrails.org/getting_started.html). This guide covers all the topics mentioned in my article but at a more granular level.
- [GoRails](https://gorails.com/start)