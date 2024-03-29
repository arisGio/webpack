# webpack

Introduction to webpack

## Intro

webpack 5 (bit more configuration), snowpack, parcel, vite
introduction to bundling in general
tools like CRA
use JS modules
transpile code with BABEL
compile SASS
create source maps
use TypeScript
make environment as simple or as advanced you want

module with dependencies --> static assets (for deployment)

loaders, plugins etc
webpackconfig.js

building an environment that you can use for multiple projects

## Initial Files (src/dist)

src is where all our source code goes, all the code that we write
dist: where all of our static assets are built to
eg if you have experience with ReactJS and you write eg npm build --> and it builds out your static assets --> into a folder called build..
that's basically the same thing we are doing here, although we are not using ReactJS, we coul if we wanted tol but we are not

for now let's create the index.html and later on we are going to install an html plugin --> so that we don't have to actually edit the html file in the dist folder --> will have a template in our src folder that we can edit, but just for now just add a boilerplate

later on we will see how we can install the webpack dev server plugin --> so we won't actually need live server later

## Creating Modules

focus on the environment that we are building, not the app
error: cannot use import statement outside a module --> there is a way we can do this by adding type module to our package.json and all but...
webpack is going to take care of this for us...

## Webpack Install & Building
<code>npm init -y</code> --> skip the questions, creates the package.json file

<code>npm i -D webpack webpack-cli</code> --> install webpack & webpack-cli as dev dependencies, creates the package-lock.json file, in package.json you should see under dev dependecies the newly installed packages

to run webpack we need to create a script
we have not set the mode yet so we use production mode for now, then run...

<code>npm run build</code> --> in the dist folder we have main.js now, basically it looked at our source code here and it saw that in our generateJoke function we are returning something and we are console logging it etc...

## Using NPM Modules

now we can import and export our own JS modules
--> we can also use npm modules
--> let's see an example even though we don't need this module for our initial purposes
<code>npm i uuid</code> --> let's install UUID which will just generate a uuid number, if we just reload, it is not going to work, we have to rebuild it

<code>npm run build</code> --> to rebuild it, so main.js now get's updated with the new code we previously wrote, and we can see this in the console too
--> you can install any npm modules you want and use them
--> now main.js is more complicated because we have that uuid code that's being compiled

<code>npm remove uuid</code> --> we do not need this module so we remove it

## Webpack Config File

rebuild code
it's going to be in common JS syntax
config object
set mode development and remove mode production
set the entry & the output
--> by default, is looking at <code>index.js</code> & outputting to <code>dist</code> a main.js... but we can change all that around if you want to rename stuff
<code>\_\_dirname</code>: take me to the current directory

--> let's delete main.js & npm run build --> created a bundle.js file & we have to update in the index.html --> now it works properly as before

--> you could have multiple if you wanted to do some code splitting

--> [name].js going to be bundle.js as you can see from the entry property

--> since we are in development mode we have all this unnecessary lines of comments in bundle.js, in production mode is going to be much less code

## Loaders & Sass Compiling

loaders will make it so you can load images right into your JS or CSS or SASS
--> in this example we want to have sass files here, and have webpack compile our SASS or have the loader do it

<code>npm i -D sass style-loader css-loader sass-loader</code> --> you can use node sass, but probably is deprecated now, maybe it's DART SASS

before we add our loaders --> create a sass file
& bring that into index.js

if I do npm run buind it will show an error --> no loaders are configured to process this file
--> rules array with an object for each loader or each file type
--> in general I could create more css files, import them or use them

## HTML Webpack Plugin

plugins are a little more powerful than loaders, can be used for many things

--> we don't want to have to edit index.html, but just be able to delete dist folder and be able to npm run build & have it rebuilt

<code>npm i -D html-webpack-plugin</code>
--> whenever we have a plugin then we go under the module

if we delete the dist folder & then npm run build again it will rebuild the dist folder

## HTML Template

--> if we type in some html and rebuild it will get rid of it

after rebuild it updates the index.html with the code template.html has
--> in dist folder index.html includes bundle.js & html of template.html

## Caching & Hash Setup

google: caching webpack --> https://webpack.js.org/guides/caching/

--> we can make it so instead of just being bundle.js, it's going to be bundle.hash (bunch of letters & numbers), you might have seen this if you've used react and there's other front-end frameworks that do this as well
--> when they generate the assets --> they have some kind of hash --> and basically what happens is this will change every time the file changes --> which helps with caching

delete dist folder and rebuild

## Webpack Dev Server

we can set up the webpack dev server
we can make it auto reload as well which is nice

--> add dev script to package.json
--> <code>npm run dev</code> --> it will ask us if we want to install the webpack dev server --> y for YES

--> default port: 8080, but we can change that
--> stop server: <code>CTRL + C</code>

now we want to add options to the dev server
--> we used to contentBase but now we use static
--> open: true --> it will open the browser automatically
compress true --> will enable gzip compression

<code>npm run dev</code> --. now the browser will open at 3000

--> stop Live Server, no need to use it now

we are not focusing on the functionality, but just showing the different things you can add to your environment

## Cleaning Up Hash Files

in dist folder the files with hash filenames can add up, as we saw previously if you recall
eg if we make a change to the code in index.js
if we save that & run npm run build again it will add a new file

clean: true --> will keep only one file and not 2 or more bundlehash1 bundlehash2 etc

--> when you run the server, it's not running directly from the files in dist --> it's actually running it from memory

change code in index.js & npm run build --> does not create additional bundle files

## Source Maps

this is one more option we can add
source maps are good for debugging because a lot of times you are going to get a message with a line number that does not show you where the actual problem is in your source code

--> source maps provide a map for of from your dist or production code to your source code

--> to enable source maps is easy..

tweek webpack.config.js & npm run build to see the result
--> we get a js.map source file --> which you can use in the browser in SOURCES and help you debbug

## Babel Loader

we want to add some other loaders
--> if you want your code to be BACKWARDS COMPATIBLE with older browsers and so on --> use BABEL or the Babel Loader

<code>npm i -D babel-loader @babel/core @babel/preset-env</code> --> they should have been added to package.json

then go to webpack.config.js and add one more rule about js files excluding files in the node_modules folder

<code>npm run build</code> to make sure that after saving there are no errors

## Asset Resource Loader

you might also want to load images
eg you have a logo or something eg an svg you want to load in js file
--> we want to be able to bring that by importing it
after importing it if you rebuild it you will get an error --> because we do not have a loader for this
--> there is nothing we even have to install
--> webpack comes with this asset resource loader --> so we just have to add, eg after the babel loader...
--> we want it to stay as laughing.svg otherwise it wiil be renamed to something weird

after rebuilding --> we have laughing svg in dist folder

## Finish The Joke App

stop dev server
install axios --> <code>npm i axios</code>

you now have this environment, that you could use for anything that you want to build
you can now use npm modules
your own JS modules
you can import sass files
you can import svgs
it's going to use babel
you have a server with live reload
you have source maps
there are a lot of things that we used here

## Webpack Bundle Analyzer

this is a plugin which actually shows you like a screen of all of what your applications is built from
what takes up the most space and all that

<code>npm i -D webpack-bundle-analyzer</code>

after tweeking webpack.config.js then we rebuild again --> it will open up a new page as a visual representation of our application
