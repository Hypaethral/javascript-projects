*[read part two first](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/02-create-a-project.md)*

# Additional Development Goodies (UNDER CONSTRUCTION)

## Typescript
Let's add Typescript to our previous configuration, because type-safe, refactorable javascript is juicy productivity gold when working on larger projects!  In other words, if you're taking the time to set up a robust editing environment, odds are you want to be using something like this to help with code completion and maintainability.

### Wait, but what exactly is it?
Remember that our node features were made possible by transpiling a superset of javascript with extra language features (es6) to the dumb old browser es5.  Typescript works exactly the same way -- it's a language designed on top of Javascript which can be transpiled to plain old browser JavaScript.  In that sense, JavaScript that's already in your project is *already* valid TypeScript, with no additional coding required.  This means we can introduce TypeScript slowly to an existing project over time, which is super handy when you want to start using it on a project in progress.

### How does it work?
Awesome resource for answering your [technical questions](https://github.com/Microsoft/TypeScript/wiki/FAQ)

### Installation
`yarn add typescript --dev` does everything we need to install

### Transpilation Process
Remember that TypeScript is a language superset of JavaScript, so it needs to be transpiled to es5 before it'll work in the browser. To do this, we have a few options (such as the TypeScript compiler command line tool), but we'd prefer to automate this through Webpack instead so our build process can be as straightforward as possible.

In our first dealing with Webpack, we discussed two important principles of the tool: entry and output.  To add Typescript into the mix, we'll learn a third principle of Webpack: Loaders.

#### Installing your [Loaders](https://webpack.js.org/concepts/#loaders)
Loaders are just plugins for Webpack that run a process on certain types of files before they're put in our giant bundle files.  What kind of process do we want to run?  Transpilation!  When do we want it?  By the time we're done reading this section!

There are several options for your Typescript loader, feel free to research them or pick the one your team is using.  For demonstration, we'll be using the Awesome TypeScript loader, because it's *awesome* or something.

`yarn add awesome-typescript-loader --dev`

#### Add the Loader to Webpack
```js
//  ...
//  },
    module: {
        loaders: [
            { test: /\.ts$/, loader: "awesome-typescript-loader" }
        ]
    }
};
```
The `test` property defines a regex that will determine which files should be sent through the process defined in the `loader` property.

#### Add Some TypeScript!
Add a new `cat.ts` file to your project, in a new directory called src:

```
src/
   +- cat.ts
```

```js
//updated index.js file
import Cat from './src/cat.ts';

var kitty = new Cat();

document.write('hello world: ' + kitty.meowAt('George'));
```

```js
//new src/cat.ts file
class Cat {
    name: string;
    age: number;

    public constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    meow(): string {
        return `I'm ${this.age} and my name is ${this.name}`;
    }

    meowAt(target: string): string {
        return `Hi ${target}, ${this.meow()}`;
    }
}

export default Cat;
```


#### Try it!
Currently we have a single index.js file and an index.html file still, and we have webpack configured, and we're using a fancy new es6 class defined using typescript.  So, let's try building the project and see what happens:

Hmm, so everything works!  But something's fishy.. Why didn't typescript complain about the lack of parameters when we tried to instantiate a cat?

`var kitty = new Cat();`

Shouldn't this be raising red flags, given we defined a cat's constructor as required a string and an integer?  Why did it work and allow `undefined` to show up on my page?

#### The Sad Truth about Complicated Transpilation Processes
**It's easy to miss stuff.**

We defined a loader for `*.ts` files through our loader:

`{ test: /\.ts$/, loader: "awesome-typescript-loader" }`

but, our entry file isn't actually a TypeScript file at all, it's still a JavaScript file!

#### Rename index.js to index.ts
After renaming `index.js` to `index.ts`, our IDE will recognize the file as typescript and will begin warning us of TypeScript-related errors.  If this isn't working for you, edit a few lines and save your document again, or in extreme cases, you may need to restart your IDE.

The first thing you should notice is the import statement `import Cat from './src/cat.ts';` is failing to work.  Fix your IDE's problem with this file if necessary by removing the `.ts`.

The goal at this point is to have your statement `var kitty = new Cat();` highlighted with a syntax error -- inspecting the error, you should see something to the effect of `supplied parameters do not match any signature of call target`.

Supply the missing parameters age and name and run webpack again.

`Can't resolve 'C:\Users\Ty3\IdeaProjects\environment-setup\index.js'`  Oops!

We need to rename our webpack entry point to `index.ts`, since we changed the filename in the project.

`Can't resolve './src/cat'` Oops!

Okay so here's where things get a little fucky.  Our typescript transpiler demands that , but our module loader (webpack) doesn't recognize the import statement without the suffix.  To remedy this, we can add a custom resolver to our webpack configuration object.  To my knowledge, this is a required step in order to get Webpack's and TypeScript's loading mechanisms to play nicely together:

```js
{
    //snip
    module: {
        //snip
    },
    resolve: {
        extensions: [".ts"]
    }
};
```

`webpack` should run correctly now!  Refresh your page, and your Cat's name and age should appear on the screen.  Woohoo!
