# Introduction to Ruby on Rails

## Objective
In this guide, we will cover setting up a Rails application and a few basic knowledge about layouts and principles of a Rails application

## Prerequisite
This guide assumes that you have prior experience with Ruby, a programming language. You might find a steep learning curve if you dive straight into Rails.

Here are some useful resources to learn Ruby:
- [Official Ruby Website](https://www.ruby-lang.org/en/documentation/)
- [Ruby Tutorial For Beginners](https://www.rubyguides.com/ruby-tutorial/)

## What is Rails?
Rails is a framework for web application development in the Ruby programming language. Its relationship to Ruby is similar to the one between Django and Python. The benefit of leveraging Rails is that it allows developers to write less code while still achieving more compared to other languages and frameworks. What makes Rails different from other frameworks is that it is opinionated software, designed with particular rules and preferences on how developers should write code. 

## Two Major Principles in Rails
### Don't Repeat Yourself
This principle states that, in a software system, there should be a single, unambiguous, and authoritative representation for each piece of knowledge. Code is more robust and extensible as it prevents developers from repeatedly writing the same information.

### Convention Over Configuration
This principle states that the best approach in web development is to establish conventions, rather than specifying endless configuration files.

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

## Resources
For more information on Rails, here are some useful websites:
- [Rails Guides](https://guides.rubyonrails.org/getting_started.html). This guide covers all the topics mentioned in my article but at a more granular level.
- [GoRails](https://gorails.com/start)