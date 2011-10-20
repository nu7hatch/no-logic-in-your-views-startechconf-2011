!SLIDE
# MVP Pattern

* Model - nothing changes, business data
* View - only presentation layer, no access to model
* Presenter - tie between model and view

!SLIDE
# MVP vs. Web development

!SLIDE
# MVP strengths

* Clean
* Testable

!SLIDE
# MVP weaknesses == HTTP

* Actually, impossible to implement (as well as MVC :D)

!SLIDE
# What do we really need?

* Model
* View (remember, view != template)
* Extra layer for handling web requests and responses
* Presenter

!SLIDE
# MVCP? Or rather MVHP!

* Model
* View
* Handler
* Presenter

!SLIDE
# And finally, templating!

* Mustache?
* or Shaven?

!SLIDE
# Mustache

... word about mustache

!SLIDE
# Shaven

... word about shaven

!SLIDE
# The winner is...

Just pick up your favorite,
but remember one thing...

!SLIDE
# NO LOGIC IN YOUR VIEWS!

!SLIDE
# AND NO LOGIC IN YOU TEMPLATES!

!SLIDE
# Logicless views with Rails and ERB?

* how to avoid logic in views
* how to use helpers as presenter layer...
