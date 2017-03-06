*[read part one first](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/01-acquire-the-tools.md)*

# Part Two:  Making a new project
Okay, so we've covered a ton of things and haven't even started talking about JavaScript.  Don't worry though, let's take a second to put all of this into action by creating a simple frontend project using what we know now -- we can add the extra stuff incrementally after we complete this step, but actually implementing the simple version is more important than the bells and whistles that are on the way.

## Create a project folder
VSCode specifically is directory-based like sublime rather than project-based like intelliJ, so this may be as simple as creating a folder someplace with the name of your project in mind.  Open your empty project or folder with your preferred IDE.

## Generate a package file
Most javascript projects could be registered in the package registry just like their dependencies are -- it's a standard for keeping track of dependencies and storing project metadata.  Complying with this standard is super simple, as one command (`npm init` or `yarn init`) is all we need.

To do this in VSCode, open the `View -> Integrated Terminal` or use the keyboard shortcut (`Alt + F12` by default).  If you're not using VSCode and don't have an IDE with an integrated shell, just open your preferred command line tool on the side.

After running `yarn init`, you'll answer a few prompts to create your example project (press enter a bunch of times if the defaults look good).  The resulting file is where dependencies will be stored in the future when you use commands like `yarn add <package-name> --save`.  The `--save` portion is something I learned when using NPM, but it doesn't appear to be necessary with yarn.  Yay!!  It used to be required in order to save library information to your list of dependencies in `package.json`, which could be a real headache if you ever forgot.

*If you Windows users are frustrated that VSCode is using 32-bit cmd.exe, search your settings for `terminal.integrated` to find relevant settings.* 

## Adding a dependency
Since our transpilation process is going to depend on webpack, let's add it as a dependency!

`yarn add webpack`

It might take a minute or so to complete.  This command seems to create two things: a `node_modules/` folder, for housing your project's libraries, and a `yarn.lock` file, mentioned earlier as a means of locking down version dependencies and being awesome.

However, remember the analogy of package managers to atoms of grocery items?  Do yourself a quick peek into the node_modules folder, I'll wait.

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


...Yeah.  Dependencies are *insane*.  Praise package management, because screw that.  And ensuring that the packages you use are kept track of in a `package.json` file (or similar, remember that package management is not exclusive to javascript environments) ensures that package managers will know how to help you and anyone with whom you share your code.  Don't forget it!

## Configuring Webpack by Exploration - Entry and Output
To begin setting up our super cool transpilation process, we'll start by telling webpack where to look for our input (fancy-featured javascript files galore) and where to put the output (boring, transpiled browser es5).

Create a new file called exactly `webpack.config.js`, as this is the filename that webpack looks for by default for its configuration settings.

Remembering the [5 principles of Webpack](https://webpack.js.org/concepts/), let's focus on `entry` and `output` first.

Webpack wants a json data structure for its configuration like so:

```json
// webpack.config.js, json structure

{
  "entry": "index.js",
  "output": {
    "path": "dist/",
    "filename": "bundle.js"
  }
}

```

but doesn't expect a raw json file as the format.  So, after a quick variable-izing for javascript:

```js
// webpack.config.js, this time valid javascript syntax

var config = {
  entry: 'index.js', // look for a file called index.js to start building the module tree
  output: {
    path: 'dist/', // put the result in a folder called dist
    filename: 'bundle.js' // and call it bundle.js
  }
}

module.exports = config;
```
Exporting a piece of javascript just means other files know how to import and use it. It's another dependency/modularization thing.  You can "require" them later using the syntax `var Thing = require("thing");`, which we'll get to in a while.

*Not to send you down a rabbit hole: that particular style of importing and exporting is called CommonJS, but
there are many others.*


Since we told webpack to expect `index.js` as our entry point, we should probably create a file called `index.js` as well!


```js
// index.js

document.write('hello world');
```


### Testing The First Configuration Attempt
So we have our entry and output defined in our webpack config, and our entry point exists at index.js.  Its only function right now is to write "hello world" so we know everything is working.

Let's run `webpack` in our project directory (again, it looks for `webpack.config.js` by default) and observe what happens.
```
  ERROR in Entry module not found: Error: Can't resolve 'index.js'
```

Hey what gives?  I made my `index.js` file and my config entry says `'index.js'`, why isn't this 'resolving'?

Update your entry to use a relative directory syntax like so:

`entry: './index.js'`

and try running `webpack` again.

Weird it worked, why didn't the `dist/` folder have the same problem?  To avoid this issue, there's a [commonly-used module in node called `path`](https://nodejs.org/api/path.html).  Using `path` in our config would look something like this:

```js
// webpack.config.js, optional (standard) solution for path resolution using the path module

// import the path module using CommonJS import style
// we declare it as a constant (read-only) because we won't be changing our library anytime soon
const path = require("path");

var config = {
  entry: path.resolve(__dirname, 'index.js'), //__dirname is a node built-in function to get the relative current directory.  Check out the node docs for more info!
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js' // this is just a filename, not a path, so no worries there
  }
}

module.exports = config;
```

Great!  So, running `webpack` worked, and now we have a `dist/` folder with a file called `bundle.js` inside.  Poking around inside that generated `bundle.js` file is giving me a headache, but rest assured it's saving us way more headaches than we realize.

## Uhhh... Now what?
Okay so we have this dist folder now with another javascript file in it that we had no part in writing.  What do we do with it?

This is our javascript payload that we can use wherever we wish.  Create a new file `index.html` like so:

```html
<body>
  <p>did it work?</p>
  <script src="dist/bundle.js" type="text/javascript"></script>
</body>
```
and open it with your browser of choice...

![unable to load pic](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/images/noice.png "God I love it when things work")

This is a trivial example because we have *one* Javascript file right now, but the point of webpack is that we could have a mountain of files and the entire project can be contained in a single javascript file (transpiled, minified, and all the rest!) automagically.  Woohoo!


*[continued in part three](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/03-additional-stuff.md)*
