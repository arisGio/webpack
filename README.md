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
