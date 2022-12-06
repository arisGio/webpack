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

npm init -y --> skip the questions, creates the package.json file

npm i -D webpack webpack-cli --> install webpack & webpack-cli as dev dependencies, creates the package-lock.json file, in package.json you should see under dev dependecies the newly installed packages

to run webpack we need to create a script
we have not set the mode yet so we use production mode for now, then run...

npm run build --> in the dist folder we have main.js now, basically it looked at our source code here and it saw that in our generateJoke function we are returning something and we are console logging it etc...

## Using NPM Modules

now we can import and export our own JS modules
--> we can also use npm modules
--> let's see an example even though we don't need this module for our initial purposes
npm i uuid --> let's install UUID which will just generate a uuid number, if we just reload, it is not going to work, we have to rebuild it

npm run build --> to rebuild it, so main.js now get's updated with the new code we previously wrote, and we can see this in the console too
--> you can install any npm modules you want and use them
--> now main.js is more complicated because we have that uuid code that's being compiled

npm remove uuid --> we do not need this module so we remove it
