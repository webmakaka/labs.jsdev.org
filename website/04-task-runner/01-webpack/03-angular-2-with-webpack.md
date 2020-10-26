---
layout: page
title: Angular 2 with Webpack Project Setup
description: Angular 2 with Webpack Project Setup
keywords: Angular 2 with Webpack Project Setup
permalink: /tasks-runner/webpack/angular-2-with-webpack/
---

# [YouTube] Angular 2 with Webpack Project Setup

https://www.youtube.com/watch?list=PLgGUMhSgtxJyIQ4vI3BzlCzZLHL79Ew6p&v=HTFZPF6iixA

MySRC:  
https://bitbucket.org/marley-angular/angular-2-with-webpack-project-setup/

---

### Angular 2 with Webpack Project Setup - Part 1: NPM Dependencies

<br/>

**package.json**

    {
      "name": "angular_2_webpack",
      "version": "0.0.1"
    }

<br/>

**Dependencies:**

    $ npm install --save \
    @angular/common \
    @angular/compiler \
    @angular/core  \
    @angular/forms  \
    @angular/http  \
    @angular/platform-browser  \
    @angular/platform-browser-dynamic  \
    @angular/router  \
    core-js  \
    reflect-metadata \
    rxjs  \
    zone.js

<br/>

**devDependencies:**

    $ npm install --save-dev \
    typescript \
    typings \
    webpack \
    ts-loader \
    html-webpack-plugin \
    webpack-dev-server \
    raw-loader \
    cross-env

<br/>

### Angular 2 with Webpack Project Setup - Part 2: TypeScript Compiler and Typings

**tsconfig.json**

    {
        "compilerOptions": {
            "target": "es5",
            "experimental": true,
            "emitDecoratorMetadata": true
        }
    }

<br/>

    $ npm bin
    /project/node_modules/.bin

<br/>

    $ $(npm bin)/tsc -v
    Version 2.0.3

<br/>

    $ $(npm bin)/tsc --rootDir src --outDir dist

**Errors:**

    Cannot find name 'Promise'.
    Cannot find name 'Map'
    Cannot find name 'Set'

<br/>

typings

    $ $(npm bin)/typings -v
    1.4.0

<br/>

    s $(npm bin)/typings search core-js
    Viewing 1 of 1

    NAME    SOURCE HOMEPAGE                             DESCRIPTION VERSIONS UPDATED
    core-js dt     https://github.com/zloirock/core-js/             1        2016-09-14T11:45:59.000Z

<br/>

dt - definitely typed

<br/>

    $ $(npm bin)/typings install --global --save dt~core-js

<br/>

    $ $(npm bin)/tsc --rootDir src --outDir dist

no more errors

<br/>

### Angular 2 with Webpack Project Setup - Part 3 NPM Scripts

package.json has been updated

    $ npm install

<br/>

    $ npm run build

<br/>

browser -> run index.html from src folder.

<br/>

    ReferenceError: require is not defined

<br/>

### Angular 2 with Webpack Project Setup - Part 4 Webpack

    $ npm install --save-dev \
    webpack \
    ts-loader

<br/>

    $ $(npm bin)/webpack --progress

<br/>

browser -> run index.html from src folder.

<br/>

reflect-metadata shim is required when using class decorators

    $ npm run build

<br/>

### Angular 2 with Webpack Project Setup - Part 5 Webpack Dev Server

    $ npm install --save-dev html-webpack-plugin

<br/>

    $ npm run build:prod

<br/>

    $ npm install --save-dev webpack-dev-server

<br/>

    $ npm run serve
