
---
Pluralsight - 201305 Intermediate - AngularJS Fundamentals

1. Intro

2. Controllers and Markup

3. Services

- 02 Custom server [.factory](http://docs.angularjs.org/guide/dev_guide.services.creating_services)

- $anchorScroll

4. Routing
	
- 04 [$routeProvider](http://docs.angularjs.org/api/ngRoute.$routeProvider)  for configuring routes.

	Example: http://docs.angularjs.org/api/ngRoute.$route
	
- 07 [$routeParams](http://docs.angularjs.org/api/ngRoute.$routeParams) to retrieve the current set of route parameters.

- 08 [$route](http://docs.angularjs.org/api/ngRoute.$route)

	Access route parameters
	
	$route.reload() without need to reload the entire App.

- 09 [$localProvider](http://docs.angularjs.org/api/ng.$locationProvider).html5Mode(true); to get rid of the hash sign.

	*Note* : Back end(server-side) support is needed.
	
- 10 Template and Resolve Properties

	resolve, delay a loading view until you have finished a task such as loading a data.

- 11 [$location](http://docs.angularjs.org/api/ng.$location)

5. Custom Directives

- [.directive](http://docs.angularjs.org/guide/directive)

6. Testing

	
---