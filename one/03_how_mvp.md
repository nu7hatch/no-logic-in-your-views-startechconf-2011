!SLIDE
.notes What is MVP and how it works? Actually it's very similar to MVC, take a look:
.notes The most important difference is that you can't access models from the view layer.
# How it works?

* Model - nothing changes, business logic
* Presenter - tie between model and view
* View - only presentation layer, no access to model

!SLIDE
.notes Ok my friends, for sure you want to see it in action, so I  prepared some snippets which possible implementation.
# Example...

!SLIDE small
.notes What I have here is very, very simple user model, just name and age. 
# Model

    @@@python
	class User(object):
	    def __init__(self, name, age):
	        self.name = name
		    self.age = age

!SLIDE small
.notes Also very simple presentrer.
# Presenter

    @@@python
	class UserInfoPresenter(object):
        def __init__(self, **kw):
            self.__user = User(kw['name'], kw['age'])
			self.user_name = self.__user.name
			self.user_age = self.__user.age
			
!SLIDE small
.notes And finally, one possible view. 
# View	

    @@@python
	class UserInfoView(object):
	    def __init__(self, **kw):
	        self.p = UserInfoPresenter(**kw)
	  
	    def render(self):
	        return "My name is %s and I'm %d years old" % (
			    self.p.user_name,
				self.p.user_age)

!SLIDE small
.notes Now we can use this views in our application. 
# Usage?...

    @@@python
	import tornado.web
	
	class UserInfoHandler(tornado.web.RequestHandler):
	    def get(self, name, age):
		    view = UserInfoView(name, age)
			self.write(view.render())

!SLIDE
.notes As you noticed, I totaly separated my application from the web requests layer. Thanks to this my implementation is very clean, and easy to test without slow and complicated integration tests.
.notes Also, by using separated request handler I made it totally independent from the web. I can use the same code in console application with no fuss.  
# MVP strenthgs

* Clean
* Testable
* Independent

!SLIDE
# Controller !== Event handler

!SLIDE
.notes And this insight, pushes us to more deductions. 
# What does web really need?

* Model
* View
* Event (Request) handler
* Presenter or Controller
* Templating

!SLIDE
# MVHPT

!SLIDE
# MVCHT

!SLIDE
# MVCPHT

!SLIDE
# AAAAAAA

!SLIDE
# American Association Against Acronym and Abbreviation Abuse
