![](http://i.imgur.com/BGrt2QK.png)

## Ionic Framework generator [![Build Status](https://api.travis-ci.org/diegonetto/generator-ionic.png?branch=master)](https://travis-ci.org/diegonetto/generator-ionic) [![Built with Grunt](https://cdn.gruntjs.com/builtwith.png)](http://gruntjs.com/)

> Yeoman generator for Ionic - lets you quickly set up a hybrid mobile app project

**This is currently under active development.**

## Usage
Install `generator-ionicjs`
```
npm install -g generator-ionicjs
```

Make a new directory, and `cd` into it
```
mkdir my-ionic-project && cd $_
```

Run `yo ionicjs`
```
yo ionicjs
```

Spin up a `connect` server with `watch` and `livereload` for developing in your browser
```
grunt serve
```
## Workflow
The included Grunt build system provides sensible defaults to help optimize and automate several aspects of your workflow when developing hybrid-mobile apps using the Ionic Framework.

### Local browser development
Running `grunt serve` enhances your workflow by allowing you to rapidly build Ionic apps without having to constantly re-run your platform simulator. Since we spin up a `connect` server with `watch` and `livereload` tasks, you can freely edit your CSS (or SCSS/SASS files if you chose to use Compass), HTML, and JavaScript files and changes will be quickly reflected in your browser.

### Building assets for Cordova
Once you're ready to test your application in a simulator, `grunt build` will concatenate, obfuscate, and minify your JavaScript, HTML, and CSS files and copy over the resulting assets into your app's `www/` directory so they are ready to be served by Cordova.

### Cordova commands
To make our lives a bit simpler, the `cordova` library has been packaged as a part of this generator and delegated via Grunt tasks. To invoke Cordova, simply run the command you would normally have, but replace `cordova` with `grunt` and `spaces` with `:` (the way Grunt chains task arguments).

For example, lets say you want to add iOS as a platform target for your Ionic app
```
grunt platform:add:ios
```
or emulate a platform target
```
grunt emulate:ios
```

## Initial Walkthrough
To help you hit the ground running, let's walk through an example workflow together. We're assuming you've followed the [usage](https://github.com/diegonetto/generator-ionic#usage) directions and are inside your app's directory.

We'll start by running our app in a browser so we can make a few changes.
```
grunt serve
```
Play around with livereload by changing some of the styles in `app/styles/main.css` or HTML in one of the files in `app/templates/`. When you're ready, lets go ahead and build the assets for Cordova to consume and also spot check that we didn't bork any code during the build process. We can do that with another handy Grunt task that runs the build process and then launches a `connect` server for use to preview the app with our built assets.
```
grunt serve:dist
```
If everything looks good the next step is to add a platform target and then emulate our app. In order for us to launch the iOS simulator from the command line, we'll have to install the `ios-sim` package. (If you forget to do this, Cordova will kindly remind you).
```
npm install -g ios-sim
grunt platform:add:ios
grunt emulate:ios
```
You may have realized that when the Grunt build process is run, it triggers the Cordova build system as well, so you end up with a beautifully packaged mobile app in a single command.

## Testing Your App
To lesson the pain of testing your application, this generator configures your project with a handful of libraries that will hopefully make testing your application, dare I say, more enjoyable.

![Comic](http://dilbert.com/dyn/str_strip/000000000/00000000/0000000/100000/10000/6000/600/116640/116640.strip.gif)

### Unit Tests
The foundation of our testing solution is built using [Karma](http://karma-runner.github.io/) which was created by the AngularJS team and is all around awesome. Inside of your generated `karma.conf.js` file you will find some basic configuration settings. Notice that we're using [Mocha](http://visionmedia.github.io/mocha/) to structure our tests and pulling in [Chai](http://chaijs.com/), a slick assertion library. You can easily drop Chai and replace Mocha with [Jasmine](http://jasmine.github.io/) depending on your preference.

Your generated `Gruntfile.js` also contains a `karma` task that provides further configuration. Any properties specified via this task will override the values inside `karma.conf.js` when run via `grunt`. If you look closely at this task, you'll notice that we're using [PhantomJS](http://phantomjs.org/) for both Karma targets, but you can easily update the `karma:unit` target to run tests inside of real browsers.

Ok, now that you have some context (and links to read up on the bundled testing libraries), go ahead and run `grunt test` and open up one of the included unit tests - `test/spec/controllers.js`. In your editor of choice, change this line - `scope.pets.should.have.length(4);` to any number other than four and watch what happens. Since your test files are being watched for changes, Grunt knows to go ahead and re-run your test suite, which in this cause should have errored out with a failure message being displayed in your terminal.

Undo your modification and ensure that all tests are passing before continuing on.

### End2End Tests
Coming soon!

### Code Coverage
So you've finished writing your tests, why not showoff just how watertight your application has become? Using [Istanbul](http://gotwarlost.github.io/istanbul/) - which was built at Yahoo - we can generate visually engaging code coverage reports that do just that!

Our beloved generator has done all the hard work for you, so go ahead and see these coverage reports in action by running `grunt coverage`.

If this is your first time using Istanbul, take a look around. It will help you spot gaps in your unit tests and lets face it, the more visual gratification we can get during our testing stage, the greater the likelihood of us sitting down and writing these tests to begin with!

## Wrapping it up
If you made it this far then congratulations! You're now up and running with the gorgeous Ionic Framework powered by an intelligent workflow and sophisticated build system - all facilitated by the addition of just a few commands!

## Special Thanks To
* The pioneers behind [Yeoman](http://yeoman.io/) for building an intelligent workflow management solution.
* The [AngularJS Generator](https://github.com/yeoman/generator-angular) and [Ionic Seed Project](https://github.com/driftyco/ionic-angular-cordova-seed) projects for inspiration.
* The visionaries at [Drifty](http://drifty.com) for creating the [Ionic Framework](http://ionicframework.com/).

## TODO
1. ~~building / Emulating doc section~~
2. Better starting app using SideBar and a few other components
3. ~~Workflow doc section~~
4. ~~SCSS prompt options~~
5. ~~Decide if we should use imagemin + svgmin~~
6. ~~Add testing support using Karma and integrate with Grunt~~
7. Consider pulling in generator-angular as a subgenerator
8. Add Mocha generator unit tests
9. Contributing doc section

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)
