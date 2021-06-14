---
title: "Tailwindcss Configuration for Django"
date: 2021-06-11T11:19:45+09:00
draft: true
---

> This post will includes a tutorial on how to configure tailwind for Django using gulp. Most of the references come from: [Nomadcoders](https://nomadcoders.com)
---


## 1. Node.js & gulp installation
Have the node.js and gulp installed
*Dependencies used in this tutorial are: 12.13.0 LTS && gulp 12.0.3 version*

#### 1-1. npm init & package 
`npm init`
After initialization, a file named 'package.json' is created. 
Delete "main", "script", "author", "license" because we are not going to be using node.js for our project's backend

#### 1-2. install gulp
install gulp and its dependencies.
`npm i gulp gulp-postcss gulp-sass gulp-csso node-sass autoprefixer -D`

#### 1-3. install tailwind & initiate
`npm i tailwindcss -D`
`npx tailwind init`

#### 1-4. add node_modules to .gitignore

## 2. Setting up a gulpfile 
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