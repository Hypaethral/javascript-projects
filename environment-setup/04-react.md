*[read part three first](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/03-typescript.md)*

# UNDER CONSTRUCTION

# React

React is a [super slick UI library by Facebook](https://facebook.github.io/react/). Keeping your components compartmentalized and defined based on inputs is functional, reuseable, and easy to reason about/test.  Let's add it to our typescript project!

### Installation

`yarn add react --save`

`yarn add react-dom --save`

##### Hey, what's up with that second package?

The react-dom package was separated from react's main package starting in version `0.14`.  This separation, [from my understanding](https://facebook.github.io/react/blog/2015/09/10/react-v0.14-rc1.html), was to allow exposure of React's methodologies without necessarily exposing the rendering logic.  Modularity++ or something. Humorously, in deprecating React's internal rendering code, Facebook created an alarming variable name to deter developers of the code:

![unable to load pic](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/images/secret_internals.png "oh jeez, I guess these guys don't f*** around")

### TypeScript Support

### JSX

# Reflux
React is usually accompanied by a style of data control referred to as Flux, which you can think of as a plan for how data moves around your app.  MVC is another style.  MVC -- or Model View Controller -- is one way of managing data in your applications, which involves setting up bindings between a controller, the brain of your component, and the view, or the code that controls what the user sees.  These bindings can function in a pattern called "two-way" binding, where if the user updates the view, the controller updates the model.  Similarly, if the controller updates the model, the view shown to the user changes.  This pattern is tried and true, and still frequently used today.

Flux, in contrast to MVC, attempts to simplify this two-way data binding by forcing the data to travel in a single flow, a defined path from "store" to listening components.  If a component needs to make a decision to change the store or render or anything like that, it requests to do so through an "action" which can influence a related store in a well-defined way.  Once the store updates as the result of an action, listening components are, again, rerendered and updated to match.  If you read a bit ahead about React, you know that part of its power lies in intelligently deciding what should render and what shouldn't.  By defining listeners for your stores as specifically as possible, you can achieve a unidirectional flow of data that causes rerenders in very specific places, which can also improve performance.  

*[continued in part five](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/05-additional-stuff.md)*
