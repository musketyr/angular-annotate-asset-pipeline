AngularJs Annotate Asset-Pipeline
================================
[ ![Codeship Status for craigburke/angular-annotate-asset-pipeline](https://codeship.com/projects/63e0e280-8c81-0132-c100-6e5f8c02ac8f/status?branch=master)](https://codeship.com/projects/60472)

The `angular-annotate-asset-pipeline` is an [Asset Pipeline](http://www.github.com/bertramdev/asset-pipeline) module that provides annotations for dependecy injection to allow angular JavaScript or CofeeScript files to be minified in Gradle and Grails projects.

## Getting started

### Gradle
```groovy
buildscript {
    dependencies {
        classpath "com.bertramlabs.plugins:asset-pipeline-gradle:2.0.20"
        classpath "com.craigburke.angular:angular-annotate-asset-pipeline:2.0.3"
    }
}

dependencies {
	compile "com.craigburke.angular:angular-annotate-asset-pipeline:2.0.3"
}
```
Make sure the dependency is specified in both the buildscript and dependencies blocks.

### Grails 
Add the plugin to your **BuildConfig.groovy**::
```groovy
plugins {
	runtime ":angular-annotate-asset-pipeline:2.0.3"
}
```

## How it works

Since the parameter names are significant for AngularJS to do dependency injection and most minifiers rename parameters,
you have to use inline annotations. See [A Note on Minification](https://docs.angularjs.org/tutorial/step_05)

This plugin uses [ng-annotate v0.15.4](https://github.com/olov/ng-annotate) to add those inline annotations and make your angular files safe to minify.

For example this 
```javascript
myApp.controller('IndexController', function($scope) {
	$scope.message = "Hello world";
});
```

Will be automatically annotated like so:
```javascript
myApp.controller('IndexController', ['$scope', function($scope) {
	$scope.message = "Hello world";
}]);
```
