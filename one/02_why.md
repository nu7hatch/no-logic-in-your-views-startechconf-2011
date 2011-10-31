!SLIDE
.notes Answer for the first question is very short and simple. Our application becomes very hard to test, and business logic becomes view-dependent, which is fucking wrong! 
# Why logic in views is so bad?

* features are hard to test
* application becomes view-dependent

!SLIDE
.notes But there is one more important question we have to ask before we move forward. Why on the earth people are putting logic in the views? And again, simple answer. 
# Why people have logic in views?

* Because they can...
* Because tools allow that

!SLIDE
.notes Yes, but speaking of tools. What tools are you guys using to build your web applications?
# Speaking of tools

* Ruby on Rails
* Django
* Pylons/Pyramid
* Zope

!SLIDE
.notes Exactly, you are using MVC/MVT frameworks.
# Speaking of tools...

* MVC frameworks (Ruby on Rails, Pyramid)
* MVT frameworks (Django)

!SLIDE
.notes Now let me tell you something my friends. MVC for the web is a marketing bullshit. So far I know, there is no agile web framework matching the definition of MVC.
# MVC for web is a myth!

!SLIDE
.notes Just take a look at this short comparison...
.notes Controller should handle user actions and be sort of a tie between model and view layers.

# MVC pattern

* Model - contains business logic
* Controller - handles user events via registered handler
* View - produces response for the user

!SLIDE
.notes Now, let's compare it with reality. For example, with the most popular web framework, Ruby on Rails.
# Web vs. MVC

## Ruby on Rails
.notes Controller handles request, produces response, interacts with models, deals with http layer, hmm it does almost everything... Too bad that it doesn't clean my house.
.notes And my favorite part. Views in Rails? Can someone explain me who invented to call templates as views?

* Model - business logic (OK)
* Controller - handles web request, produces response (Um?)
* View - um... isn't it a template?

!SLIDE
# Remember folks...

* <strong>View !== Template</strong>
* MVC for the web <strong>is a myth</strong>

!SLIDE
.notes Ok, but let's turn off "Hater mode" for a while, and figure out how to make the world better by looking some alternatives... 
# Alternatives?

!SLIDE
.notes The only thing coming to my mind is MVP.
# MVP

!SLIDE
# Bitches likes MVP
