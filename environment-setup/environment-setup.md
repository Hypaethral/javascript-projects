# Set Up A Brofessional Javascript Dev Environment (UNDER CONSTRUCTION)

*Check out the ["why this matters" document](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/why-does-this-matter.md) before starting!*

*As far as projects go, this is definitely more of a tutorial. It's just a helpful thing in case you don't already have a javascript development environment or in case you run into an issue with a technology listed below.*

*Speaking of, I'll be using VSCode for parts that specify an IDE.  If you get lost or run into issues using your preferred editor, at least get it set up in VSCode by following the specific parts for this project!  Personally I had to abandon my preferred IDE, IntelliJ IDEA, because things just weren't working correctly for some reason.  It happens.*

#### A preamble for Windows users
Windows Power Shell / Git Bash will save you a ton of headaches when we do commandline stuff. Personally, I also use ConEmu to improve the UX (look'n'feel) of these shells.

If you try to follow along with `cmd`, gosh rest your puppers.

# The IDE
[Download VSCode](https://code.visualstudio.com/Download) (or don't if you already have an IDE you like for JavaScript or wanna try something else.)

If the IDE you're using is new to you, get comfy! Try the walkthrough.  You can fiddle with color themes and keybindings from your favorite editors.

# Node.js ([Download](https://nodejs.org/en/))
Unfortunately I could make three repositories worth of tutorials on Node alone.  For now, just think of nodeJS as another language entirely run on servers instead of in the browser, which is a means to sweet advanced javascript features on the frontend (confusing, I realize).  It also comes bundled with a package manager, NPM, which we'll use to keep track of all of these things.  More on that later.

There are installation guides all over the place for Node if you get stuck.  Verify that you can run
`node -v` and `npm -v` successfully in your shell of choice before moving on.


# Webpack
So remember how we installed Node and I was all, "yo this server-side language is going to give you language features on the frontend" and you were all "dude that doesn't make any sense"?  Well, prepare for some tiny fragments of sense!  Enter webpack [(outsourcing the explanation!)](https://webpack.js.org/concepts/).

You can install webpack globally by running

`npm i -g webpack`

We'll worry about configuring this later.

# Yarn
So we installed and ran an npm command, but what exactly *is* npm?

NPM stands for ~~nyarlathotep propagates mythos~~ node package manager, and it's used to manage libraries of code and those libraries' libraries and those libraries' libraries and...  All right, here's a picture to get us started:

![unable to load pic](https://github.com/Hypaethral/javascript-projects/blob/master/environment-setup/images/package_managers.png "Worst analogy ever...")

Think of it like a program that manages a shopping list for code libraries. Instead of sharing the code groceries, we share and update the shopping list, because our needs are very, very specific, and certain groceries depend on other factors that we don't have to worry about. The package manager manages these dependencies and specifications based on what our shopping list tells it (in a file called `package.json` for us). 

So why is this section about package managers called Yarn instead of NPM?  Yarn is a cool alternative to NPM which locks down versions for you so you never have to worry about production environments installing the wrong version of a package or its dependencies.

In this way, the grocery analogy only got us so far... It may be more helpful to think of managing all the atoms in each grocery item: the task is more complex than what it seems, because each package (a grocery item) is comprised of many smaller pieces (atoms vs dependencies).


Install yarn with

`npm i -g yarn`

and have a look at these resource links if you'd like:
* [Good write-up on yarn](https://code.facebook.com/posts/1840075619545360) by Facebook devs.
* [yarn docs](https://yarnpkg.com/lang/en/docs/)


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


## Typescript

## React

## Reflux

# Other Stuff

### Linting

### Testing

### Version Control
* Never commit the node_modules folder -- that's like giving your neighbor your entire fridge of food instead of a recipe for making a sheet of cookies. 

* stub: starting in a project that already exists

### Debugging

### Continuous Integration
