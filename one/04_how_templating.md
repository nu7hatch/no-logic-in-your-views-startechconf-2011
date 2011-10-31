!SLIDE
.notes Ok my friends, but finally we have to talk about the backbone of our views. About the templates.
.notes When i submitted proposal for this conference few months ago i was just starting my experiment with logic-less templating systems. To be honest i expected that i will come here to sell my templating language as the best solution of your problems.
.notes Please, take a look at my Shaven templates compared to well known Mustache.
# And finally, templating!

* Shaven?
* Mustache?

!SLIDE
# Mustache

... word about mustache

!SLIDE
# Shaven

... word about shaven

!SLIDE
.notes As i said, 2 months ago i expected to present Shaven as the best solution. But as you see in that presentation, problem is not laying down in the templates but in the way of how our application is built.
# The winner is...

!SLIDE
# The winner is...

## Just pick up your favorite!

!SLIDE
# But remember one thing...

!SLIDE
.notes And now my friends, you may say, WTF? Some guy with crappy hairstyle is showing up here, saying that everything we've done so far is wrong and we should rewrite our Rails or Django apps with some MVCHPT pattern? 
# NO LOGIC IN YOUR VIEWS!

!SLIDE
.notes Of course not. I obviously hope that some new, nicely implemented MVP or MVC framework will become Rails-killer. But so far we have to deal with this. And we can do it by applying sort of good practices. 
# Logicless views in Rails?

* Treat controllers as views (like Django does)
* Use helpers to slim down templates
* Pseudo-presenter layer
* Avoid abstraction

!SLIDE
# Treat controllers as views

!SLIDE
# Before

    @@@ruby
	class BooksController < ApplicationController
	  def index
	    @books = Post.where(:available => true).all
		respond_with(@books)
	  end
	end
	
!SLIDE
# After

    @@@ruby
	class Book < ActiveRecord::Base
	  def self.available
	    where(:available => true)
	  end
	end
	
	class BooksController < ApplicationController
	  def index
	    @books = Post.available.all
	  end
	end

!SLIDE
# Helpers to slim down templates

!SLIDE
# Before

    @@@html
    <% @books.each do |book| %>
	  <h1><%= link_to book.title, book, :id => "show_book_#{book.id}" %></h1>
	  <p><%= book.summary %></p>
	<% end %>
	
# After

    @@@html
	<% @books.each do |book| %>
	  <h1><%= link_to_book book %></h1>
	  <p><%= book.summary %></p>
	<% end %>

	@@@ruby
	module BooksHelper
	  def link_to_book(book, options={})
	    link_to book.title, book, { :id => "show_book_#{book.id} }.merge(options)
	  end
	end

!SLIDE
.notes Yes, i'm very big hater of HAML and reason of it is very ordinary. Simply, my applications are styled by external design studios or freelancers, and most of them have no idea about existing of those abstract markups.  
# Avoid abstraction

* HAML
* Slim
* ...

!SLIDE
# Btw, Django templates rock!
