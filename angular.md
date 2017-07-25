# Angular Tutorial

## 4. Directory and File Organization
Refactoring codebases and moving files around. 
*Goal:* To make the app more easily expandable, and mantainable
**So far we know how to make it modular and testable**
 
 ### Steps:
 1. Put each entity in its pwn file
 2. Organize code by **feature area**, instead of by *function*
 3. Split code into modules that other modules can depend on.

## One feature per file:
Traditional approach: To put all controllers in one file, all components in another and all views in another, and so on.

**Disadvantage**
As we add more and more features, our files will get bigger and bigger and it will be difficult to navigate and find the code we are looking for.

**Solution**
Let's have each feature(entity) in its own file.

However, there may arise a case where logically related files will not be grouped together; it will be really difficult to locate all files related to a specific section of the application and make a change or fix a bug.

## Organizing by feature.
We are going to group our files into directories by feature.
\e.g Since we have a section that lists phones, we will put all the related files into a phone-list/ folder under app/. 
For feactures which are used across the different parts of the app, we put them under app/core/. {or shared, common, ..}

app/
    phone-list/
        phone-list.component.js
        phone-list.component.spec.js
    app.js

# Using Modules
A modular architecture promotes code reuse, both inside and across applications. 
To make our code reuse easy:
Each feature or section should declare its own module and all related entities should register themselves on that module.
Example: 
app/
  phone-list/
    phone-list.module.js
    phone-list.component.js
    phone-list.component.spec.js
  app.module.js

*app/phone-list/phone-list.module.js:*
We define the `phoneList` module
angular.module('phoneList', []);

*app/phone-list/phone-list.component.js:*
// Register the `phoneList` component on the `phoneList` module,
angular.
  module('phoneList').
  component('phoneList', {...});


app/app.module.js:
(since app/app.js now only contains the main module declaration, we gave it a .module suffix)
// Define the `phonecatApp` module
angular.module('phonecatApp', [
  // ...which depends on the `phoneList` module
  'phoneList'
]);

## NB
Note that files defining a module (i.e. .module.js) need to be included before other files that add features (e.g. components, controllers, services, filters) to that module. 