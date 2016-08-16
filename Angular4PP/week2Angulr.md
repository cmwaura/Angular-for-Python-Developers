Web Tools: Grunt
-----------------

- Grunt: Task runner based in configuration of tasks
-installing Grunt
	npm install -g grunt-cli
installing grunt locally

Configuring Grunt
-----------------

configuration in Gruntfile.js
	
	module.exports = function(grunt){
		//do requires here
		require('jit-grunt')(grunt);

		// do grunt tasks config here
		grunt.initConfig({

			});
			// register tasks here
			grunt.registerTask('built',['jshint']);
			grunt.registerTask('default', ['build']);
	}

File Globbing Patterns
-----------------------

Grunt uses filename expansion(globbing):

- * matches any number of char but not /
- ? matches a single char but not /
- ** mathes any char including / as long as it's the only thing in a path part
- {} allows for comma-separated list of "or" exp
- ! negation 

Creating a Distribution Folder
==============================

Your project contains many files so you may need to generate a distrib folder that:

- contains only essential files to server up your website
-compacted and minified files.

Copying and Cleaning up
Create a distrib folder and clean up the distrib folder:
	
	npm install grunt-contrib-copy --save-dev
	npm install grunt-contrib-clean --save-dev

Config:
	copy:{
		dist:{
		cwd:'app'
		src:["**",'!**/*.css','!**/*.js'],
		dest:'dist',
		expand:true

		}
	}
for cleaning the dist folder
	clean {
		build:{
			src['dist/']
		}
	}
register a task to perform the clean then jshint and finally copy

	grunt.registerTask('build', ['clean', jshint', 'copy']);

Preparing the Distrib folder
----------------------------

Grunt modules:

	npm install grunt-contrib-concat --save-dev
	npm install grunt-contrib-cssmin --save-dev
	npm install grunt-contrib-uglify --save-dev
	npm install grunt-filerev --save-dev
	npm install grunt-usemin --save-dev

Grunt-usemin:

- umbrella task that configures and completes most of the css and js minification and uglification tasks

UseminPrepare
-------------

- look for block config in an html file
<!-- build:css styles/main.css -->
<!--endbuild -->

- config:
	useminPrepare:{
		
		html:'app/menu.html',
		options:{dest:'dist'}
		
		}

- will automatically generate config info for concat, cssmin and uglify tasks

Filerev
-------

Revision your files:adds a revision tag to the name of the file
	eg: main.css --> main.2343433235.css

config:
	filerev:{
		option:{
			encoding:'utf-8', algorithm, 'md5', length:20

	}
}


Gulp.
-----

Gulp : Task runner based on code over configuration approach.

- uses node.js streams to build complex pipelines, avoiding creation of intermediate files
- plugins are simple and do one thing well
- Tasks are executed with max concurrency possible

1) Installing gulp.
- CLI
	
	npm install -g gulp

-Locally
	
	npm install gulp --save-dev

2) Install gulp plugins:
	
	npm install jshint gulp-jshint jshint-stylish gulp-imagemin gulp-concat gulp-uglify gulp-minify-css gulp-usemin gulp-cache gulp-changed gulp-rev gulp-rename gulp-notify  browser-sync del --save-dev

3) load the plugins
	
	var gulp = require('gulp'),
	    minifycss = require('gulp-minify-css'),
	    jshint = require('gulp-jshint'),
	    stylish = require('jshint-stylish'),
	    uglify = require('gulp-uglify'),
	    usemin = require('gulp-usemin'),
	    imagemin = require('gulp-imagemin'),
	    rename = require('gulp-rename'),
	    concat = require('gulp-concat'),
	    notify = require('gulp-notify'),
	    cache = require('gulp-cache'),
	    changed = require('gulp-changed'),
	    rev = require('gulp-rev'),
	    browserSync = require('browser-sync'),
	    del = require('del')

Gulp streams
------------

- gulp.src() function takes the file globs and creates a stream of objects that rep files
- pipe(): allows the stream to be piped through a function
- gulp.dest(): specifies the destination of the changed files

JsHint
------
Defining the jshint task:

	gulp.task('jshint', function(){
		gulp.src('app/scripts/**/*.js')
			.pipe(jshint())
			.pipe(jshint.reporter(stylish));
	});

Imagemin
--------
image minification task
	
	gulp.task('imagemin', function(){
			gulp.src('app/images/**/*')
				.pipe(cache(imagemin({optimizationLevel:3,
				progressive:true, interlaced:true})))
				.pipe(gulp.dest('dist/images'))
				.pipe(notify({message:'Images task complete'}));
		});'

Cleaning Up
------------
makes use of the node module del
	
	gulp.task('clean', function(){
		return del(['dist']);
	});

Usemin
------

	gulp.task('usemin'['jshint'], function(){
		return gulp.src('.app/menu.html')
		.pipe(usemin({
			css:[minifycss(), rev()],
			js:[uglify(), rev()]}))
		.pipe(gulp.dest('dist/'))
		
	});

	
BrowserSync
-----------

default task does the building.

	gulp.task('browser-sync', ['default'], function () {
		var files = [
	      'app/**/*.html',
	      'app/styles/**/*.css',
	      'app/images/**/*.png',
	      'app/scripts/**/*.js',
	      'dist/**/*'
	      ];
	    browserSync.init(files, {
      server: {
         baseDir: "dist",
         index: "menu.html"
      }
      });
Watch
-----

	// Watch
	gulp.task('watch', ['browser-sync'], function() {
	  // Watch .js files
	  gulp.watch('{app/scripts/**/*.js,app/styles/**/*.css,app/**/*.html}', ['usemin']);
	   // Watch image files
	  gulp.watch('app/images/**/*', ['imagemin']);
	});

Default Task:
-------------

	// Default task
	gulp.task('default', ['clean'], function() {
	    gulp.start('usemin', 'imagemin','copyfonts');
	});


ANGULAR SCOPE:
==============

- Scope is an object that refers to the app model
- this is at he core od Angular two-way data binding
- the glue btwn the view and the controller

	- the controller can set the properties of the scope
	- the view binds to the properties set by the controller
	- Angular is responsible to keep the two in sync

$rootScope
-----------
- The topmost scope
	-created by Angular when your app starts

Nested Scopes.
--------------

- Everytime Angular creates a new scope, it will create as a child of a parent scope
	-JavaScript prototype
	-Child has access properties in the parents scope
	- a few caveats.


Angular Forms and Form Validation
=================================

- Angular two-way databinding makes it straight forward to work with forms:

	- Define a javascript object on the $scope
		.controller('ContactController', [$scope, function($scope){
			$scope.feedback = {mychannel"", firstName:"",
			lastName:"", agree:false, email""};
			}]);

	- use ng-model directive on form fields
		<input type="text" class="form-control" id="firstname" name="firstname" placeholder="Enter First Name" ng-model= "feedback.firstName" required>

Binding Select
---------------

- Select items can be found by defining javascript objects:
	var channels = [{value:"tel", label:"Tel"},
	{value:"Email", label:"Email"}];

- Then bind using ng-options directive

	<select class="form-control" ng-model="feedback.mychannel" ng-option="channel.value as channel.label for channel in channels"><option>Tel. or Email></option>
	</select>

Angular form Validation
=======================

- Turn off HTML5 Form validation:
	
	<form class="form-horizontal" name="feedbackForm" ng-submit="sendFeedback()" novalidate>
- angular takes over responsibility for validation
- make sure to give the form a name
- ng-submit directive specifies the function to call.

Angular Form Validation Directive
----------------------------------

- angular validates the form fields before copying the value to the scope
- some directives:
	-ng-minlength etc

Field Properties
-----------------
- use Field name and form name


Field properties and CSS
------------------------
- Bootstrap provides alot of css classes to enable display of form validation state and messages.


