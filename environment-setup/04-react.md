*[read part three first](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/03-typescript.md)*

# UNDER CONSTRUCTION

# React

React is a [super slick UI library by Facebook](https://facebook.github.io/react/). Keeping your components compartmentalized and defined based on inputs is functional, reuseable, and easy to reason about/test.  Let's add it to our typescript project!

### Installation

`yarn add react --save`

`yarn add react-dom --save`

##### Hey, what's up with that second package?

The react-dom package was separated from react's main package starting in version `0.14`.  This separation, [from my understanding](https://facebook.github.io/react/blog/2015/09/10/react-v0.14-rc1.html), was to allow exposure of React's methodologies without necessarily exposing the rendering logic.  Modularity++ or something. Humorously, in deprecating React's internal rendering code, Facebook created an alarming variable name to deter developers:

![unable to load pic](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/images/secret_internals.png "oh jeez, I guess these guys don't f*** around")

### TypeScript Support

The next thing we need, since we're introducing React on top of TypeScript, is React Types.  Because of the way TypeScript works, we need a special file for these libraries called a type file to expose React's methods to TypeScript for IDE support.

`yarn add "@types/react" --dev`

`yarn add "@types/react-dom" --dev`

### Updating our TypeScript file to be a React Component

Let's start by redefining our Cat class to "extend" a React component:

```
class Cat extends React.Component {
    render() {
        return <span></span>
    }
}
```

TypeScript asks that we very clearly define the "shape" of the two main defining features of a React component:

#### The Props

"Props" are the external stuff that the component is given from its parents.  If a component's props change, the component is (usually) forced to rerender.  A component's props should *only* change based on an external, parent component.

#### The State

"State" the internal stuff that the component remembers from render to render. A stateful component is said to be "smart", and can make decisions about its own appearance and rendering.  If a component's state changes, the component is (usually) forced to rerender.  A component's state should *only* change based on an internal actor. Remember this for when we explore Stores later.

In general, we try to avoid state where possible because it's confusing and can change at the drop of a hat.  Try to create your components as stateless (or colloquially, "dumb") as possible, and only use state when you absolutely need it.  This will take some practice!


#### Defining React's Props and State with TypeScript

We'll focus on just props for now, because that's all we need.

We'll create an interface to define the property names and their type:

```
interface CatProps {
    age: number;
    name: string;
}
```

By defining our Props in this way, we're defining the scope of how someone using this component can interact with it.  Let's take a look at what that looks like, using a nifty markup syntax called JSX:

### JSX

### Optional "functional" style of defining a React component


# Reflux
React is usually accompanied by a style of data control referred to as Flux, which you can think of as a plan for how data moves around your app.  MVC is another style.  MVC -- or Model View Controller -- is one way of managing data in your applications, which involves setting up bindings between a controller, the brain of your component, and the view, or the code that controls what the user sees.  These bindings can function in a pattern called "two-way" binding, where if the user updates the view, the controller updates the model.  Similarly, if the controller updates the model, the view shown to the user changes.  This pattern is tried and true, and still frequently used today.

Flux, in contrast to MVC, attempts to simplify this two-way data binding by forcing the data to travel in a single flow, a defined path from "store" to listening components.  If a component needs to make a decision to change the store or render or anything like that, it requests to do so through an "action" which can influence a related store in a well-defined way.  Once the store updates as the result of an action, listening components are, again, rerendered and updated to match.  If you read a bit ahead about React, you know that part of its power lies in intelligently deciding what should render and what shouldn't.  By defining listeners for your stores as specifically as possible, you can achieve a unidirectional flow of data that causes rerenders in very specific places, which can also improve performance.  

*[continued in part five](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/05-additional-stuff.md)*
