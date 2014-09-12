angular.lazyLoad
================

lazyLoad module for angularjs

In order to add dynamic loading of modules for angularjs, then Ba is necessary to:
1. to find the line:
  ==============================================
  forEach(loadModules(modulesToLoad), function(fn) { instanceInjector.invoke(fn || noop); });
  ==============================================
2. replace it with:
  ==============================================
  instanceInjector.injectModules = function (_modulesToLoad){
    forEach(loadModules(_modulesToLoad), function(fn) { instanceInjector.invoke(fn || noop); });
  };

  instanceInjector.injectModules(modulesToLoad);
  ==============================================
3. upload files with the modules in any way possible (eg requirejs) and call a method injectModules in service $injector
