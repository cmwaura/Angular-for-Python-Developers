ANGULAR FACTORY, SERVICE AND DEPENDENCY INJECTION.

Dependency injection.
---------------------

What is Dependecy injection?
----------------------------

Software design patterns that implements, inversion of control for resolving dependencies

- Dependency: an object that can be used
- Injection: passing of a dependency to a dependent object so that it can use it. The clien does not need to build the object


Dependency

Three ways for a component to get hold of its dependencies:

	- create dependency using new operator
	- lookup dependency using a global
	- have dependency passed to it where
	needed.
Third option is the most flexible.

Dependency Injection
--------------------
DI involves four roles:

	- The service
	- The client
	- The interfaces
	- The injector

Angular and DI
---------------
- Separation of business logic and dep construction

- The dependency is passed to the object consuming it where it is needed
- Angular injector subsystem is responsible for

	- creating componenets
	- resolving their dependencies and
	-providing them to other components


Angular Factory and Service.
============================

1) Angular services
--------------------

- substitutable objects wired together using DI
- Allows organizing and sharing code across app
- Lazy instantiation
- singletons

2) Angular Built in services
-----------------------------

- Built in services start with $
	ie $http, $scope etc
	- inject via DI

3) Create your own services
---------------------------

Five functions that declare services:

	-service()
	-factory()
	-provider()
	-constant()
	-value()

ANGULAR TEMPLATES
=================

angular templates are written in HTML

	- contains Angular specific elements and attribs
		- Directives
		- Markup:{{}}
		- Filter
		- Form Control


The ngInclude Directive
-----------------------

Enables to fetch compile and include an external HTML fragment

usage:
	<div ng-include="menu.html"></div>
	<ng-include src="menu.html"></ng-include>

creates a new scope


SINGLE PAGE APPLICATIONS
========================

Traditional Websites
--------------------
when you request for index.html:

Browser ---> Request index.html ----> Server
Browser <--- Send index.html <------- Server

This pattern continues for each page that you request. Its a full round trip.

Single Page Application:
------------------------

We have a single page master app which is a single download for alot of resources.

hence:

1) initially:

Browser ------> Request web App -----> Server
Browser <------- Send Web App and Assets <--Server

2) when a user clicks for some sort of data:

Browser -------> user clicks on link, new Request ----> Server
Browser <---- Respond with JSON data <---- Server

What is a Single Page Application
---------------------------------

Web application or website that fits into a single page

Angular ngRoute and SPAs
------------------------


Data binding: one-way and two-way
mvc framework support
views --> templates + controller + model
location and routing.

Role of Client and Server in SPA
---------------------------------

Server:
	- serves up data using REST API
	- supplies the static HTML pages, Angular templates and resources

Rendering of view is completely on the client-side
	- Templating and routing

Deep Linking
------------

Deep linking: hyperlink that specifies a link to a searchable or indexed piece of web content

Example:
	http:// www.confusion.food/index.html#/menu/0

anything beyond the hash does not cause the page to reload. So for instance if the hash wat to be changed to /menu/1, the page would not reload but it would think that its in the same page.

The $location Service
---------------------
- Exposes the current URL in the browser add bar
	- watch and observe the URL
	- Change the URL
- Synchronizes the URL with the browser when the user:
	- changes the add bar
	- click the back/forward button
	- click on a link
- Allows you to manipulate the hash potion of a URL
	- url(): get/set the URL
	- path(): get/set the path
	- search(): get/set the search path
	- hash()

Routing
-------

Mapping the path portion of a URL to a handler for that particular route

	- Route is the hash portion of the URL in the context of SPAs
	- Example:
		http://www.confusion.food/index.html#/menu/0

Angular ngRoute Module
----------------------

- installing the module:
	bower install angular-route-S
- manages the interaction between the $location service and the rendered view
- Dependency injection into the module:
	angular.module('confusionApp', ['ngRoute'])

The $routeProvider
------------------
- Angular provider
- Enables mapping from the routes to handlers
- Handlers are an object that defines:
	- template URL
	- Controller

The ngView Directive
--------------------

Directive that works together with the $route service to include the rendered template of the current route into the main layout

usage:
	<ng-view></ng-view>
	<div ng-view></div>

The Angular UI-Router for SPAs
==============================

Limitatons of ngRoute
---------------------

- only one view is allowed per page
	- no support for multiple views
	- no support for nested views
- Application views tied to route URL

Angular UI Router
-----------------

views based on state of the applicatin
	- change parts of your site using the routing even if the URL does not change
multiple views
nested views

Installing:
	bower install angular-ui-router-S

It takes a state machine route and uses states to track the machines.

uiView Directive
----------------

Indicates where to include the views
<div ui-view="header"></div>
<div ui-view="content"></div>

ui-sref
-------

use ui-sref="state"to indicate which state to move to when clicked.
<a ui-sref="app"></a>

$stateParams
------------
- menu.html
	<a ui-sref="app.dishdetails({id:dish._id})"</a>
DishDetailController
