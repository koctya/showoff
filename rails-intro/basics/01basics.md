!SLIDE subsection
# Rails Tutorial


!SLIDE
.notes modified to use haml, sass, rspec, etc..

# Tutorial
based on [Rails Girls Guides](http://guides.railsgirls.com)

## Creating the application

We’re going to create a new Rails app called Note.
using [Bootstrap-sass](https://github.com/twbs/bootstrap-sass)

!SLIDE
## Install Rails

	➜  gem install rails

	➜  rails -v
	Rails 4.1.6

	➜  sqlite3 --version
	3.7.13 2012-07-17 17:46:21 ...

!SLIDE

### Next, create a new Application

	mkdir projects

	cd projects

	rails new notes -T

	cd note

!SLIDE

### Rails app dir structure.

	File/		Folder	Purpose
	app/		Contains the controllers, models, views,
				helpers, mailers and assets for your app.
	bin/		Contains scripts that starts your app
	config/		Configure your application's routes,
				database, and more.
	config.ru	Rack configuration for Rack based servers
				used to start the application.
	db/			Contains your current database schema,
				as well as the database migrations.

	Gemfile			These files allow you to specify what
	Gemfile.lock	gem dependencies are needed for your
					Rails application.

!SLIDE

### Rails app dir structure.

	lib/		Extended modules for your application.
	log/		Application log files.
	public/		The only folder seen by the world as-is.
				Contains static files and compiled assets.
	Rakefile	This file locates and loads tasks that
				can be run from the command line.

	README.rdoc	This is a brief instruction manual for
				your application. You should edit this
				file to tell others what your application
				does, how to set it up, and so on.
	test/		Unit tests, fixtures, and other test files.
	tmp/		Temporary files (cache, pid, session files).
	vendor/		A place for all third-party code.
				In a typical Rails application this
				includes vendored gems.


!SLIDE

## Rake

	rake routes

	rake -T

!SLIDE
.notes talk about bundler, Gemfile
## Bundler,  RubyGems
Edit Gemfile, after:

	gem 'sass-rails', '~> 4.0.3'
add:

	@@@ ruby
	gem 'haml-rails', 			'~> 0.5'
	gem 'autoprefixer-rails', 	'~> 3.1'

!SLIDE
Near end of file add:

	@@@ ruby
	group :development do
	  gem 'awesome_print',      '~> 1.2.0'
	  gem 'pry-rails',          '~> 0.3.2'
	  gem 'pry-nav',            '~> 0.2.3'
	  gem 'better_errors',      '= 1.1.0'
	  gem 'binding_of_caller',  '= 0.7.2'
	end

Install Gems for rails app.

	bundle install

!SLIDE
## Add to Git

	git init

	git add .

	git commit -m "Initial Rails App Generation"

	rails s

!SLIDE


Edit `config/application.rb` after the line

	@@@ ruby
	module Collectable
	  class Application < Rails::Application

add;

	@@@ ruby
      config.sass.preferred_syntax = :sass


Open http://localhost:3000 in your browser.

You should see “Welcome aboard” page, which means that the generation of your new app worked correctly.

Hit **CTRL-C** in the terminal to quit the server.


!SLIDE incremental
.notes What is Rails scaffolding? (Explain the command, the model name and related database table, naming conventions, attributes and types, etc.) What are migrations and why do you need them?

## Create Note scaffold

We’re going to use Rails’ scaffold functionality to generate a starting point that allows us to list, add, remove, edit, and view things; in our case notes.

	rails generate scaffold note name:string \
		description:text picture:string

The scaffold creates new files in your project directory, but to get it to work properly we need to run a couple of other commands to update our database and restart the server.

	bin/rake db:migrate
	rails server
Open http://localhost:3000/notes in your browser.

 	git add .
  	git commit -m "scaffolded notes"

!SLIDE

## Environments

	export RAILS_ENV=development

	export RAILS_ENV=test

	export RAILS_ENV=production

!SLIDE

### Database configuration; `config/database.yml`

	@@@ yaml
	default: &default
	  adapter: sqlite3
	  pool: 5
	  timeout: 5000

	development:
	  <<: *default
	  database: db/development.sqlite3

	test:
	  <<: *default
	  database: db/test.sqlite3

	production:
	  <<: *default
	  database: db/production.sqlite3

!SLIDE
# Design
.notes Talk about the relationship between HTML and Rails.

What part of views is HTML and what is Embedded Ruby (ERB)?

What is MVC and how does this relate to it?

(Models and controllers are responsible for generating the HTML views.)

The app doesn’t look very nice yet. Let’s do something about that.

We’ll use the Twitter Bootstrap project to give us nicer styling really easily.

!SLIDE
## Add Bootstrap gem
Edit Gemfile and add thee following line

	gem 'bootstrap-sass', 		'~> 3.2'

!SLIDE
## Import Bootstrap styles in `app/assets/stylesheets/application.css.scss`

	@@@ css
	@import "bootstrap-sprockets";
	@import "bootstrap";

!SLIDE

## Require Bootstrap Javascripts in `app/assets/javascripts/application.js`

	@@@ javascript
	//= require jquery
	//= require bootstrap-sprockets

!SLIDE

Open `app/views/layouts/application.html.erb`

	@@@ html
	<!DOCTYPE html>
	<html>
	<head>
	  <title>Notes</title>
	  <%= stylesheet_link_tag    'application',
	  	media: 'all', 'data-turbolinks-track' => true %>
	  <%= javascript_include_tag 'application',
	  	'data-turbolinks-track' => true %>
	  <%= csrf_meta_tags %>
	</head>
	<body>

	<%= yield %>

	</body>
	</html>


!SLIDE
Rename it to `app/views/layouts/application.html.haml`

`git mv app/views/layouts/application.html.erb app/views/layouts/application.html.haml`

!SLIDE
And replace contents with;

	@@@ ruby
	!!!
	%html
	  %head
	    %title Notes
	    = stylesheet_link_tag    'application',
			media: 'all', 'data-turbolinks-track' => true
	    = javascript_include_tag 'application',
			'data-turbolinks-track' => true
	    = csrf_meta_tags
	  %body
		.container
	      = yield

!SLIDE

Let’s also add a navigation bar and footer to the layout.

In the same file, under `%body` add

	@@@ ruby
	%nav.navbar.navbar-default.navbar-fixed-top{
		:role => "navigation"}
	  .container
	    .navbar-header
	      %button.navbar-toggle{
			  "data-target" => ".navbar-collapse",
			  "data-toggle" => 	"collapse",
			  :type => "button"}
	        %span.sr-only Toggle navigation
	        %span.icon-bar
	        %span.icon-bar
	        %span.icon-bar
	      %a.navbar-brand{:href => "/"} The Note app
	    .collapse.navbar-collapse
	      %ul.nav.navbar-nav
	        %li.active
	          %a{:href => "/notes"} Notes

!SLIDE

and after `= yield`add the following indented the same level as `%body`

	@@@ ruby
	%footer
	  .container
	    Hickory Ground 2014

!SLIDE

Now let’s also change the styling of the notes table. Open `app/assets/stylesheets/application.scss` and at the bottom add

	@@@ css
	body { padding-top: 100px; }
	footer { margin-top: 100px; }
	table, td, th { vertical-align: middle; border: none; }
	th { border-bottom: 1px solid #DDD; }

Now make sure you saved your files and refresh the browser to see what was changed. You can also change the HTML & CSS further.

In case your Terminal shows you an error message that sort of implies there is something wrong with your JavaScript or CoffeeScript, install nodejs. This issue should not appear when you’ve used the RailsInstaller (but when you’ve installed Rails via gem install rails).


!SLIDE

# Adding picture uploads

We need to install a piece of software to let us upload files in Rails.

Open Gemfile in the project directory using your text editor and under the line

	@@@ ruby
	gem 'sqlite3'
add

	@@@ ruby
	gem 'carrierwave'
.notes Explain what libraries are and why they are useful. Describe what open source software is.

!SLIDE

In the terminal run:

	bundle
Now we can generate the code for handling uploads. In the terminal run:

	rails generate uploader Picture
At this point you need to restart the Rails server process in the terminal.

!SLIDE

Hit CTRL-C in the terminal to quit the server. Once it has stopped, you can press the up arrow to get to the last command entered, then hit enter to start the server again.

This is needed for the app to load the added library.

Open app/models/note.rb and under the line

	@@@ ruby
	class Note < ActiveRecord::Base
add

	@@@ ruby
	mount_uploader :picture, PictureUploader

!SLIDE

Open app/views/notes/_form.html.haml and change

	@@@ ruby
	= f.text_field :picture
to

	@@@ ruby
	= f.file_field :picture

!SLIDE
Sometimes, you might get an `TypeError: can’t cast ActionDispatch::Http::UploadedFile to string.`

If this happens, in file `app/views/notes/_form.html.haml` change the line

	@@@ ruby
	= form_for(@note) do |f|
to

	@@@ ruby
	= form_for @note, :html => {:multipart => true} do |f|

!SLIDE

In your browser, add new note with a picture. When you upload a picture it doesn’t look nice because it only shows a path to the file, so let’s fix that.

Open `app/views/notes/show.html.haml` and change

	@@@ ruby
	= @note.picture
to

	@@@ ruby
	= image_tag(@note.picture_url, :width => 600) if @note.picture.present?

Now refresh your browser to see what changed.


!SLIDE
.notes Talk about routes, and include details on the order of routes and their relation to static files.

# Fine tune the routes

Open http://localhost:3000. It still shows the “Welcome aboard” page.

Let’s make it redirect to the notes page.

Open `config/routes.rb` and after the first line add

	@@@ ruby
	root :to => redirect('/notes')

Test the change by opening the root path (that is, http://localhost:3000/ or your preview url) in your browser.

> Rails 3 users: You will need to delete the index.html from the /public/ folder for this to work.

!SLIDE

Edit `.gitignore` and add dir `/public/uploads` at end

save code

	git add .
or

	git add -p

	git commit -m "Add picture uploader"

!SLIDE
# Create static page in your app

Lets add a static page to our app that will hold information about the author of this application — you!

	rails generate controller pages info

This command will create you a new folder under app/views called /pages and under that a file called `info.html.haml` which will be your info page.

It also adds a new simple route to your routes.rb.

	@@@ ruby
	get "pages/info"

Now you can open the file `app/views/pages/info.html.haml` and add information about you in HTML.

To see your new info page, take your browser to [http://localhost:3000/pages/info](http://localhost:3000/pages/info).


!SLIDE
## Add Info to Nav bar
Edit `app/views/layouts/application.html.haml`
Below the lines;

	@@@ ruby
	%li.active
	  %a{:href => "/notes"} Notes
add

	@@@ ruby
    %li.active
      %a{:href => "/pages/info"} Info

!SLIDE

	git add .

	git commit -m "Add info page"

!SLIDE
.notes Talk about testing and Behavior-Driven Development.

# Test your app with RSpec

RSpec is a Ruby testing framework, that describes our application’s behavior in a syntax that doesn’t look much like Ruby.

It outputs test results in your terminal.


!SLIDE

## Install Rspec

For starters, let’s install RSpec and all of its dependencies.

Edit `Gemspec`, add the line;

	@@@ ruby
	group :test, :development do
	  gem 'rspec-rails',        '~> 3.0.0'
	end

Then we call

	bundle
	rails generate rspec:install

in our project directory. This creates `rails_helper.rb`, `spec_helper.rb` in the `spec` folder, and `.rspec`.

!SLIDE

Rubyists often use the words ‘test’ and ‘specification’ interchangeably, that’s why you’ll store your tests in the ‘specs’ folder. Save your test as `note_spec.rb` (`<name_of_spec>_spec.rb`).

Inside that new file, write:

Next, let’s describe one of our specifications

	@@@ ruby
	describe Note do
	  it "has a name" # your examples (tests) go here
	end

!SLIDE

In your terminal run

	rspec spec

which will output that your test is pending as it’s not yet implemented.

!SLIDE
Let’s do something about that!

	@@@ ruby
	describe Note do
	  it "has a name" do
	    expect(:name).to be
	  end
	end

should give you a more satisfying output.


!SLIDE

### Marking to-do’s with tests

Yeah! To-do lists. Awesome. A nifty RSpec feature is the functionality to mark certain tests as pending.

Leaving out the `do` and the `end` in the example body, like so

	it "has a Name"

will mark a test as pending. For bigger applications, where you want to tackle one test at a time, you can also add an x in front of an example, making it read

	@@@ ruby
	describe Note do
	  xit "has a name" do
	end
or use the word pending in your example.

!SLIDE

run rspec with the flag; (can be added to .rspec)

	--format documentation

Happy testing!

