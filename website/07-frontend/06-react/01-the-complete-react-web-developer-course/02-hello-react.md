---
layout: page
title: React.js - The Complete React Web Developer Course (2nd Edition)
permalink: /frontend/react/the-complete-react-web-developer-course-2nd-edition/hello-react/
---

# The Complete React Web Developer Course (2nd Edition)

<br/>

## 03 Hello React
    
    
<br/>

### 007 Setting up a Web Server


    # npm install -g live-server
    # su ${username}
    
    $ cd /project/
    
    
    $ mkdir -p INDECISION-APP/public
    

<br/>
    
    $ vi INDECISION-APP/public/index.html
    
<br/>

    <html>
    <head>
        <meta charset="UTF-8">
        <title>Indecision App</title>
    </head>
    <body>
        This is my HTML file!
    </body>
    </html>


<br/>
    
    
    # live-server INDECISION-APP/public


<br/>

host:

http://localhost/

All ok



<br/>

### 008 Hello React



<br/>
    
    $ vi INDECISION-APP/public/index.html
    
<br/>

    <html>
    <head>
        <meta charset="UTF-8">
        <title>Indecision App</title>
    </head>
    <body>
        <div id="app"></div>
        <script src="https://unpkg.com/react@16.0.0/umd/react.development.js"></script>
        <script src="https://unpkg.com/react-dom@16.0.0/umd/react-dom.development.js"></script>
        <script src="/scripts/app.js"></script>
    </body>
    </html>


<br/>
    
    $ vi INDECISION-APP/public/scripts/app.js
    
<br/>


{% highlight js linenos %}

console.log('App.js is running!');

// JSX - JavaScript XML

var template = React.createElement(
    "h1",
    {id: "someid"},
    "This is JSX from app.js"
  );

var appRoot = document.getElementById('app');

ReactDOM.render(template, appRoot);

{% endhighlight %}


<br/>

### 009 Setting up Babel

http://babeljs.io/docs/plugins/preset-react/

<br/>

    # npm install -g babel-cli


    $ cd INDECISION-APP/


<br/>
    
    $ vi src/app.js
    
<br/>

{% highlight js linenos %}

console.log('App.js is running!');

// JSX - JavaScript XML

var template = <h1>This is JSX from app.js</h1>;

var appRoot = document.getElementById('app');

ReactDOM.render(template, appRoot);

{% endhighlight %}

<br/>


    $ npm init -y
    $ npm install --save-dev babel-preset-react babel-preset-env
    
    $ babel src/app.js --out-file=public/scripts/app.js --presets=env,react
    $ babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch

    
