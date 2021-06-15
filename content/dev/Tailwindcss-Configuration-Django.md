---
title: "Tailwindcss Configuration for Django"
date: 2021-06-11T11:19:45+09:00
draft: false
---

> This post will includes a tutorial on how to configure tailwind for Django using gulp. Most of the references come from: [Nomadcoders](https://nomadcoders.com)
---

## 1. Node.js & gulp installation
Have the node.js and gulp installed
*Dependencies used in this tutorial are: 12.13.0 LTS && gulp 12.0.3 version*

<br>

#### 1-1. npm init & package 

> `npm init`  

After initialization, a file named 'package.json' is created.  
Delete **"main", "script", "author", "license"** because we are not going to be using node.js for our project's backend

<br>

#### 1-2. install gulp  

<br>

install gulp and its dependencies.  
> `npm i gulp gulp-postcss gulp-sass gulp-csso node-sass autoprefixer -D`

<br>

#### 1-3. install tailwind & initiate

<br>

install tailwind: 
> `npm i tailwindcss -D`

initiate tailwind: 
> `npx tailwind init`

<br>

#### 1-4. add node_modules to .gitignore
In your project folder, there should be the `.gitignore` file.  
Add "node_modules/" in it so the whole tailwind library doesn't get uploaded there.

<br>
<br>
<br>

## 2. Setting up a gulpfile & custom scss
*setting up a gulpfile to automate collecting & converting tailwind css.*

<br>
<br>

#### 2-1. custom scss configuration
Create a "assets" folder in the main directory & Create another "scss" folder and a "styles.scss" file in it.  
**So, the directory of the "styles.scss" should be: "assets/scss/styles.scss"**

<br>

Then modify the "styles.scss" file by importing tailwind in it.  

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

<br>

#### 2-2. gulpfile configuration
Create a "gulpfile.js" In the main directory and write below code in it:  

```
const gulp = require("gulp");

const css = () => {
const postCSS = require("gulp-postcss");
const sass = require("gulp-sass");
const minify = require("gulp-csso");
sass.compiler = require("node-sass");
return gulp
    .src("assets/scss/styles.scss")
    .pipe(sass().on("error", sass.logError))
    .pipe(postCSS([require("tailwindcss"), require("autoprefixer")]))
    .pipe(minify())
    .pipe(gulp.dest("static/css"));
};

exports.default = css;
```
<br>
<br>
<br>

## 3. Execute!
We are all set. Execute it.
And make sure to ONLY modify custom scss file when you need to apply class-based custom styles.  

> npm run css

<br>
<br>