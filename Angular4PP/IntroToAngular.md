Angular Built in Directives
----------------------------

1) HTML custom Attributes:
- data- * attributes
-Angular: ng-* attrib
2) Examples: ng-app, ng-bnd etc
- also use camelCase so ngApp
- Dash-delimited attrib since HTML is case insensitive
3) Declarative programming in Action:
- Declaratively call JS fns.

The ng-app Directive.
---------------------
Applied to the HTML tag to specify the root of the app:
- applying to <html> tag means the entire page is an angular app.

The ng-init Directive
---------------------
used to evaluate and expression
initializes a javascript var
Example:
<p ng-init="index=1"><p>
<div class="row row-content"ng-init="dish={name:'uthapizza',..}"></div>

Angular Expressions
--------------------
Simple JS Expr.
- Evaluated against an Angular Scope
- No conditionals, loops, or exceptions
- Expressions enclosed in {{expressions}}

Example
<p> 6+5={{6+5}}</p>

<div class="media-body">
	<h2 class="media-heading">{{dish.name}}</h2>
	<p> {{dish.description}}</p>
</div>

The ng-model Directive
----------------------

bind an input value to a variable within the scope
-two way data binding
<div class="media-body">
	<p> {{dish.description}}</p>
	<p> Comment: {{dish.comment}}</p
	<p>
		<input type="text" ng-model="dish.comment">
	</p>
</div>

The ng-repeat Directive:
------------------------

looping construct
-loops over items in a collection
- instantiate a template for each item
Example:
<ul class="media-list">
	<li class="media" ng-repeat="dish in dishes">
		...
	</li>
</ul>

THE MVC FRAMEWORK:
------------------

1) Design Patterns


well documented solution to a recurring problem.
- architectural pattern.

Software Design pattern:

The model-view-controller Framework:

Software engineeringm architecure pattern
-isolation of domain logic from user interface
-permits independent testing, development, and maintenance.

I) Model:

- manages the behavior and data of the app domain
- responds to requests for information about its state(usually from the view)
- responds to instructions to change state(controller)
- in event-driven systems, the model notifies observers(views) when the information changes so the can react.

II) View:

- renders the model into a form suitable for interaction, typicallu a user interface element.
- has a 1-1 correnspondence with a display surface and knows how to render it.

III) Controller:

- receive info from users and initiates a response by making calls on a model object.

- accepts input from the user and instructs the model and viewport to perform actions based on that input.


Angular Modules and Controllers.
----------------------------------

Angular is built with MVC in mind

Angular modules:
----------------
- Collection of:
	1) controllers
	2) Directives
	3) services
	4) filters etc..

<html ngApp="confusionApp">
...
<body>
<script
>
var app = angular.module('confusionApp',[]);
</script>
</body>
</html>

Angular Controller.
Controller defined using a ng-controller directive on a html element
Example:
<div class="row row-content"
ng-controller="menuController as menuCtrl">
</div>

ad the controller code:
<script>
var app  = angular.module('confusionApp',[]);
app.controller('menuController', function(){

});
</script>

Angular Filters
---------------

- A filter allows us to format the value of an expression for display to the end user.
	- The do not modify the underlying data

- Filters can be used in view templates, controllers or services
- Angular comes with built in filters
- We can create our own though


Example:

price = {{dish.price | currency}} **currency in this case becomes a filter.

