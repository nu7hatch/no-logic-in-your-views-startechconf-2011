!SLIDE full
.notes And now my friends, you may say, WTF? Some guy with crappy hairstyle is showing up here, saying that everything we've done so far is wrong and we should rewrite our Rails or Django apps with some MVCHPT pattern? 
.notes Of course not. I obviously hope that some new, nicely implemented MVP or MVC framework will become Rails-killer. But so far we have to deal with this. And we can do it by applying sort of good practices. 
# Cleaning up Rails' mess

!SLIDE small full
# Treat controllers as views

!SLIDE small with-title
# Before

    @@@ruby
	# app/controllers/posts_controller.rb
	class BooksController < ApplicationController
	  respond_to :html
	  
	  def index
	    @books = Books.where(:read => false).all
		respond_with(@books)
	  end
	end
	
!SLIDE small with-title
# After

    @@@ruby
	# app/models/book.rb
	class Book < ActiveRecord::Base
	  def self.unread
	    where(:read => false)
	  end
	end

!SLIDE small with-title
# After

    @@@ruby	
	# app/controllers/posts_controller.rb
	class BooksController < ApplicationController
	  respond_to :html
	  
	  def index
	    @books = Book.unread.all
		respond_with(@books)
	  end
	end

!SLIDE smaller full
# Use helpers to slim down templates

!SLIDE small with-title
# Before

    @@@html
	<!-- app/views/books/index.html.erb -->
    <% @books.each do |book| %>
	  <h1><%= link_to book.title, book, 
		              :id => "show_book_#{book.id}" %></h1>
	  <p><%= book.summary %></p>
	<% end %>

!SLIDE small with-title
# After

	@@@ruby
	# app/helpers/books_helper.rb
	module BooksHelper
	  def link_to_book(book, options={})
	    defaults = { :id => dom_id(book, :show) }
	    link_to book.title, book, defaults.merge(options)
	  end
	end

!SLIDE small with-title
# After

    @@@html
	<!-- app/views/books/index.html.erb -->
	<% @books.each do |book| %>
	  <h1><%= link_to_book(book) %></h1>
	  <p><%= book.summary %></p>
	<% end %>

!SLIDE full
# Use cells

<footer>
  <h2><small>http://www.github.com/apotonick/cells</small></h2>
</footer>

!SLIDE small with-title
# Before

    @@@ruby
	# app/controllers/posts_controller.rb
	class PostsController < ApplicationController
	  respond_to :html
	  
	  def show
	    @post = Post.find(params[:post])
		@comments = @post.comments
		respond_with(@post)
	  end
	end

!SLIDE smaller with-title
# Before

    @@@html
	<!-- posts/show.html.erb -->
	<h1><%= @post.title %></h1>
	<p><%= @post.content %></p>
	<ul class="comments">
	  <% @comments.each do |comment| %>
	    <%= content_tag_for :li, comment do %><article>
		  <p><%= comment.content %></p>
		  <footer>
		    posted at 
			<time><%= comment.created_at.to_s(:short) %></time>
		  </footer>
		</article><% end %>
	  <% end %>
	</ul>

!SLIDE smaller with-title
# Before

    @@@html	
	<!-- shared/comments.html.erb -->
	<ul class="comments">
	  <% @comments.each do |comment| %>
	    <%= content_tag_for :li, comment do %><article>
		  <p><%= comment.content %></p>
		  <footer>
		    posted at 
			<time><%= comment.created_at.to_s(:short) %></time>
		  </footer>
		</article><% end %>
	  <% end %>
	</ul>

!SLIDE smaller with-title
# Before

    @@@html
	<!-- posts/show.html.erb -->
	<h1><%= @post.title %></h1>
	<p><%= @post.content %></p>
	<%= render :partial => "shared/comments" %>

!SLIDE small with-title
# After

    @@@ruby
	# app/cells/comments/listing.rb
	class Comments::ListingCell < Cell::Rails
	  def show
		@commentable = options[:commentable]
		@comments = @commentable.comments
		render
	  end
	end

!SLIDE smaller with-title
# After

    @@@html	
	<!-- app/cells/comments/listing/show.html.erb -->
	<ul class="comments">
	  <% @comments.each do |comment| %>
	    <%= content_tag_for :li, comment do %><article>
		  <p><%= comment.content %></p>
		  <footer>
		    posted at 
			<time><%= comment.created_at.to_s(:short) %></time>
		  </footer>
		</article><% end %>
	  <% end %>
	</ul>

!SLIDE small with-title
# After

    @@@html
	<!-- posts/show.html.erb -->
	<h1><%= @post.title %></h1>
	<p><%= @post.content %></p>
	<%= render_cell 'comments/listing', :show, 
	                :commentable => @post %>
	

!SLIDE with-title bullets incremental
.notes Yes, i'm very big hater of HAML and reason of it is very ordinary. Simply, my applications are styled by external design studios or freelancers, and most of them have no idea about existing of those abstract markups.  
# Avoid HTML magic

* HAML
* Slim
* ...

!SLIDE full
.notes Ok my friends, but finally we have to talk about the backbone of our views. About the templates.
.notes When i submitted proposal for this conference few months ago i was just starting my experiment with logic-less templating systems. To be honest i expected that i will come here to sell my templating language as the best solution of your problems.
# Logicless templating

!SLIDE bullets incremental with-title
.notes Please, take a look at my Shaven templates compared to well known Mustache.
# Logicless templating...

* Shaven?
* Mustache?

!SLIDE small with-title
# Mustache

    @@@ruby
	class MoviesPresenter < Mustache
	  def movies
	    @movie ||= {
		  :title => "Back to the future",
		  :director => "Steven Spielberg"
		}
	  end
	end

!SLIDE small with-title
# Mustache

    @@@html
	{{#movie}}
	  <h1>{{ title }}</h1>
	  <p>directed by {{ director }}</p>
	{{/#movie}}

!SLIDE full
# Shaven

<footer>
  <h2><small>http://github.com/nu7hatch/shaven</small></h2>
</footer>

!SLIDE small with-title
# Shaven

    @@@ruby
	class MoviesPresenter < Shaven::Presenter
	  def movies
	    @movie ||= {
		  :title => "Back to the future",
		  :director => "Steven Spielberg"
		}
	  end
	end

!SLIDE smaller with-title
# Shaven

    @@@html
	<div data-fill="movie">
	  <h1 data-fill="title">Movie title here</h1>
	  <p>directed by <span data-fill="director">Joe Schmoe</span></p>
	</div>

!SLIDE smaller with-title
# Shaven

    @@@html
	<ul data-fill="movies">
	  <li data-fill="movie">
	    <span data-fill="title">Some movie</span> 
		directed by <span data-fill="director">Joe Schmoe</span>
	  </li>
	  <li data-dummy="true">
	    Other movie by Joe Schmoe
	  </li>
	</ul>

!SLIDE smaller with-title
# Shaven

    @@@html
    <ul data-fill="movies" data-if="movies?">
	  *snip*
	</ul>
	<div class="no-movies" data-unless="movies?">
	  Sorry bro, no movies to show here...
	</div>

!SLIDE full
.notes As i said, 2 months ago i expected to present Shaven as the best solution. But as you see in that presentation, problem is not laying down in the templates but in the way of how our application is built.
# The winner is...

!SLIDE full
# The winner is...

<footer>
  <h2>Just pick up your favorite!</h2>
</footer>

!SLIDE with-title bullets incremental
# Once again

* Treat controllers as views
* Use helpers to slim down templates
* Use cells
* Avoid magic
* Use logicless templates

!SLIDE with-title bullets good
# Once again

* Treat controllers as views
* Use helpers to slim down templates
* Use cells
* Avoid magic
* Use logicless templates

!SLIDE full
# And remember...

!SLIDE small main full wrong
# NO LOGIC IN YOUR VIEWS!
