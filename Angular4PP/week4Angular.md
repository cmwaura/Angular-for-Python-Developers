CLIENT-SERVER COMMUNICATION
===========================

Networking Essentials
---------------------

- Web applications arent stand alone and many of them have a "cloud" backend.

Browser <------C-S comm-----> The Cloud
					{ Server Backend<--> Database}

The Networking Alphabet Soup
----------------------------

HTTP, URL, JSON, XML, SOAP, REST

Client-Server Communication
---------------------------

- network operations cause unexpected delays
- you need to write applications recognizing the asynchrounous nature of communication

Hypertext Transfer Protocol(HTTP)
---------------------------------

- client server communication protocol
- allows retrieving interlinked text documents


Browser --------GET--------------> Web Server
		<----HTTP/1.1 200 OK------

- Get is requesting for a particular info to be delivered

Http Response
-------------

Server may send back data in specific format:
	- XML
	- JSON

JavaSript Object Notation
-------------------------

- light weight data interchange format
- language independent *
- self-describing and easy to understand
- example:

		{ "promotions":[
			{
				"id":0,
				"name": "weekend Grand Buffet"
				"image":"images/buffet.png"
				"label":"New",
			}
		]
		}

Setting up a Server using json-server
-------------------------------------

1) install via npm:
	
	npm install json-server -g

2) Configuring server Folder:

- Create a folder called json-server and move into the folder
- download db.json file 
- At the command prompt type the following to start the server
	json-server --watch db.json
- check on port 3000 on the machine for a response.

Client-Server Communication using $http
---------------------------------------

- $http: Core Angular service to communicate with servers using HTTP protocol via the browser's 
	-XMLHttpRequest
	-JSONP
- Operation is asynch in nature

Promise
-------

- Angular $q service: run functions asynch and use the return value when they are done processing.

Asych work ----> Promise---> handlers/callbacks
					|		{success error}
					|------>States pending
						{fulfilled rejected}

success -----> fulfilled
error -------> rejected

- if the promise is successful, then the state is fulfilled while if there is an error in the promise then the work is rejected.


The $http Service
-----------------

- the $http service returns a promise:

		$http({method:'GET', url:'/dishes'})
			.then(function(){
			...
			},
			function(){
				...
				});

- shortcut methods:
$http.get()
	.post()
	.put()
	.delete()
	.jsonp()
etc

Example:

	$http.get({baseurl+'/dishes'})
				.then(
					function(response){
				$scope.dishes = response.data;
				scope.showMenu= true;
							},
				function(response){
					scope.mess = "error"+ response.status+ response.statusText;
					});

HTTP Response
-------------
- Response:
	response.data
	response.headers
	response.status: status code
	response.config
	response.statusText: status text of resp


The ngIf Directive
------------------

- its literally like an if but on the DOM. can be used to add/remove a portion of the DOM tree based on an expression.

<div ng-if="!showMenu">
{{message}}
</div>
