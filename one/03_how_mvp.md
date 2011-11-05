!SLIDE bullets incremental with-title
.notes What is MVP and how it works? Actually it's very similar to MVC, take a look:
.notes The most important difference is that you can't access models from the view layer.
# How does it work?

* Model 
    - nothing changes, business logic
* Presenter 
    - tie between model and view
* View 
    - only presentation layer, no access to model

!SLIDE full
.notes Ok my friends, for sure you want to see it in action, so I prepared some snippets whith possible implementation.
# Example...

!SLIDE small with-title
.notes What I have here is very, very simple user model, just name and age. 
# Model

    @@@ruby
	class User < Struct(:name, :age)
	  # snip...
	end
	
!SLIDE small with-title
.notes Also very simple presentrer.
# Presenter

    @@@ruby
	class UserInfoPresenter
	  def initialize(attrs={})
	    @user = User.new(attrs[:name], attrs[:age])
	  end
	  
	  def name
	    @user.name
	  end
	  
	  def age
	    @user.age
	  end
	end

!SLIDE small with-title
.notes And finally, one possible view. 
# View

    @@@ruby
	class UserInfoView
	  def initialize(params={})
	    @p = UserInfoPresenter(params)
	  end
	  
	  def render
	    "My name is %s and I'm %d years old" % [
		  @p.name, @p.age ]
	  end
	end

!SLIDE small with-title
.notes Now we can use this views in our application. 
# Usage?...

    @@@ruby
	require 'sinatra'
	
	get '/user-info' do
	  view = UserInfoView.new(params[:name], params[:age])
	  view.render
	end

!SLIDE with-title bullets incremental
.notes As you noticed, I totaly separated my application from the web requests layer. Thanks to this my implementation is very clean, and easy to test without slow and complicated integration tests.
.notes Also, by using separated request handler I made it totally independent from the web. I can use the same code in console application with no fuss.  
# MVP strengths

* Clean
* Testable
* Independent

!SLIDE with-title bullets incremental
.notes And this insight, pushes us to more deductions. 
# What does the web need?

* Model
* View
* Event (Request) handler
* Presenter or Controller
* Templating

!SLIDE with-title bullets good
# What does the web need?

* Model
* View
* Event (Request) handler
* Presenter or Controller
* Templating

!SLIDE main good full
# MVHPT?

!SLIDE main good full
# MVCHT?

!SLIDE main good full
# MVCPHT?

!SLIDE full
# AAAAAAA

!SLIDE small full
# American Association Against Acronym and Abbreviation Abuse
