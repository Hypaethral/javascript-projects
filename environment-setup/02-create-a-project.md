# Putting it Together:  Making a new project
Okay, so we've covered a ton of things and haven't even started talking about JavaScript.  Don't worry though, let's take a second to put all of this into action by creating a simple frontend project using what we know now -- we can add the extra stuff incrementally after we complete this step, but actually implementing the simple version is more important than the bells and whistles that are on the way.

#### Create a project folder
VSCode specifically is directory-based like sublime rather than project-based like intelliJ, so this may be as simple as creating a folder someplace with the name of your project in mind.  Open your empty project or folder with your preferred IDE.

#### Generate a package file
Most javascript projects could be registered in the package registry just like their dependencies are -- it's a standard for keeping track of dependencies and storing project metadata.  Complying with this standard is super simple, as one command (`npm init` or `yarn init`) is all we need.

To do this in VSCode, open the `View -> Integrated Terminal` or use the keyboard shortcut (`Alt + F12` by default).  If you're not using VSCode and don't have an IDE with an integrated shell, just open your preferred command line tool on the side.

After running `yarn init`, you'll answer a few prompts to create your example project (press enter a bunch of times if the defaults look good).  The resulting file is where dependencies will be stored in the future when you use commands like `yarn add <package-name> --save`.  The `--save` portion is something I learned when using NPM, but it doesn't appear to be necessary with yarn.  Yay!!  It used to be required in order to adds the library information to your list of dependencies in `package.json`, which could be a real headache if you ever forgot.

*If you Windows users are frustrated that VSCode is using 32-bit cmd.exe, search your settings for `terminal.integrated` to find relevant settings.* 

#### Adding a dependency
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

#### Configuring Webpack
Create a new file called exactly `webpack.config.js`, as this is the filename that webpack looks for by default for its configuration settings.

Remembering the [5 principles of Webpack](https://webpack.js.org/concepts/), let's focus on `entry` and `output` first.

The configuration file is set up like in a json structure like so:

```js
//webpack.config.js

var config = {
  entry: 'index.js', //look for a file called index.js to start building the module tree
  output: {
    path: './dist/', //put the result in a folder called dist
    filename: 'bundle.js' //and call it bundle.js
}

```

Since we made our entry point `index.js`, we should probably create a file called `index.js` as well!


```js
//index.js

document.write('hello world');
```
