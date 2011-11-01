!SLIDE bullets incremental with-title
.notes Answer for the first question is very short and simple. Our application becomes very hard to test, and business logic becomes view-dependent, which is fucking wrong! 
# Why it is so bad?

* hard to test
* logic becomes view-dependent

!SLIDE bullets incremental with-title
.notes But there is one more important question we have to ask before we move forward. Why on the earth people are putting logic in the views? And again, simple answer. 
# Why people do it?

* because they can...
* because tools allow that

!SLIDE bullets incremental with-title
.notes Yes, but speaking of tools. What tools are you guys using to build your web applications?
# Speaking of tools

* Ruby on Rails
* Padrino
* Django
* Pylons/Pyramid

!SLIDE bullets incremental with-title
.notes Exactly, you are using MVC/MVT frameworks.
# Speaking of tools...

* MVC frameworks (Rails, Pyramid)
* MVT frameworks (Django)

!SLIDE main
.notes Now let me tell you something my friends. MVC for the web is a marketing bullshit. So far I know, there is no agile web framework matching the definition of MVC.
# MVC for web is a myth!

!SLIDE bullets incremental with-title
.notes Just take a look at this short comparison...
.notes Controller should handle user actions and be sort of a tie between model and view layers.
# MVC pattern

* Model
    - business logic
* Controller
    - user events via registered handler
* View 
    - response for the user

!SLIDE bullets incremental with-title
.notes Now, let's compare it with reality. For example, with the most popular web framework, Ruby on Rails.
# Web vs. MVC

.notes Controller handles request, produces response, interacts with models, deals with http layer, hmm it does almost everything... Too bad that it doesn't clean my house.
.notes And my favorite part. Views in Rails? Can someone explain me who invented to call templates as views?

* Model 
    - business logic
* Controller 
    - handles web request, produces response...
* View 
    - um... isn't it a template?

!SLIDE bullets with-title wrong
# Web vs. MVC

* Model 
    - business logic
* Controller 
    - handles web request, produces response...
    - <strike>user events (via registered handler)</strike>
* View 
    - um... isn't it a template?
	- <strike>response for the user</strike>

!SLIDE bullets incremental with-title
# Conclusion...

* Templates == Views
* Controllers == View + Event Handler

!SLIDE main
# View !== Template

!SLIDE main small
# Controller !== Event handler

!SLIDE
.notes Ok, but let's turn off "Hater mode" for a while, and figure out how to make the world better by looking some alternatives... 
# Alternatives?

!SLIDE
.notes The only thing coming to my mind is MVP.
# MVP

## <code>Model - View - Presenter</code>
