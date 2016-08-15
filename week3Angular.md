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
