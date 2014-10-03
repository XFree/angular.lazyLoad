angular.lazyLoad
================
  
[https://github.com/XFree/angular.js/commit/3f22596bc342abd856d7300380969b7cfe8f9c61](https://github.com/XFree/angular.js/commit/3f22596bc342abd856d7300380969b7cfe8f9c61 "lazyLoad Commit")


lazyLoad module for angularjs  
In order to add dynamic loading of modules for angularjs, then you need to:   

1. to find the line:  
  `forEach(loadModules(modulesToLoad), function(fn) { instanceInjector.invoke(fn || noop); });`
2. replace it with:  
  `instanceInjector.injectModules = function (_modulesToLoad){
    forEach(loadModules(_modulesToLoad), function(fn) { instanceInjector.invoke(fn || noop); });
  };`  
  `instanceInjector.injectModules(modulesToLoad);`  
3. upload files with the modules in any way possible (eg requirejs) and call a method injectModules in service $injector

If you add this code:  
 `//angular patch fro get modules.
     ensure(angular, 'modules', function(){
        return modules;
     });`  
in:       
 `return ensure(angular, 'module', function() {  
 /** @type {Object.<string, angular.Module>} */  
    var modules = {};`  
        
You can write modules to add to the current application:  
 example code:  
 `var _aBeforeInject = angular.extend({}, angular.modules),  
     _aInjectModules = [];  
 //...                      
 //You load modules code   
 //...  
 angular.forEach(angular.modules, function(value, key){  
    if (!_aBeforeInject.hasOwnProperty(key)){          
      _aInjectModules.push(key);  
    }  
 });  
 //inject new modules  
 $injector.injectModules(_aInjectModules);`  
 
enjoy.  =)  


