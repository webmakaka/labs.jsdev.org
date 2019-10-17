---
layout: page
title: React.js - The Complete React Web Developer Course (2nd Edition)
permalink: /frontend/react/the-complete-react-web-developer-course-2nd-edition/webpack/
---

# The Complete React Web Developer Course (2nd Edition)

<br/>

## 06 Webpack


    # npm -g remove babel-cli live-server
    $ npm install --save babel-cli live-server


<br/>
    
    $ vi package.json
    
<br/>
    
{% highlight javascript linenos %}

{
  "name": "INDECISION-APP",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "serve": "live-server public/",
    "build": "babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-preset-env": "^1.6.0",
    "babel-preset-react": "^6.24.1"
  },
  "dependencies": {
    "babel-cli": "^6.26.0",
    "live-server": "^1.2.0"
  }
}


{% endhighlight %}

    $ npm run serve
    $ npm run build

<br/>

### 050 Installing Configuring Webpack

    $ npm install --save webpack@3.1

<br/>

index.html

<br/>
    
{% highlight html linenos %}


<html>
<head>
    <meta charset="UTF-8">
    <title>Indecision App</title>
</head>
<body>
    <div id="app"></div>
    <script src="/bundle.js"></script>
</body>
</html>

{% endhighlight %}


<br/>

package.json

<br/>

{% highlight json linenos %}

{
  "name": "INDECISION-APP",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "serve": "live-server public/",
    "build": "webpack --watch",
    "build-babel": "babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-preset-env": "^1.6.0",
    "babel-preset-react": "^6.24.1"
  },
  "dependencies": {
    "babel-cli": "^6.26.0",
    "live-server": "^1.2.0",
    "webpack": "^3.1.0"
  }
}

{% endhighlight %}


<br/>

webpack.config.js

<br/>
    
{% highlight javascript linenos %}


const path = require('path');

module.exports = {
    entry: './src/app.js',
    output: {
        path: path.join(__dirname, 'public'),
        filename: 'bundle.js'
    }
};


{% endhighlight %}


<br/>

### 053 Importing npm Modules


**example**

<br/>

    $ npm install --save validator@8.0.0

<br/>

<br/>
    
    $ vi src/app.js
    
<br/>


{% highlight javascript linenos %}

    import validator from 'validator';

    validator.isEmail('test@gmail.com');

{% endhighlight %}
    
<br/>
    
    $ npm install --save react@16.0.0 react-dom@16.0.0


<br/>
    
    $ vi src/app.js
    
<br/>


{% highlight javascript linenos %}

    import React from 'react';
    import ReactDOM from 'react-dom';

    const template = React.createElement('p', {}, 'testing 123');
    ReactDOM.render(template, document.getElementById('app'));
    
{% endhighlight %}


<br/>

### 054 Setting up Babel with Webpack

    $ npm install --save babel-core@6.25.0 babel-loader@7.1.1
    
<br/>

webpack.config.js

<br/>

{% highlight javascript linenos %}

    const path = require('path');

    module.exports = {
        entry: './src/app.js',
        output: {
            path: path.join(__dirname, 'public'),
            filename: 'bundle.js'
        },
        module: {
            rules: [{
                loader: 'babel-loader',
                test: /\.js$/,
                exclude: /node_modules/
            }]
        }
    };

{% endhighlight %}

<br/>


.babelrc

<br/>

{% highlight json linenos %}

{
    "presets": ["env", "react"]
}

{% endhighlight %}

<br/>

{% highlight javascript linenos %}

import React from 'react';
import ReactDOM from 'react-dom';

const template = <p>This is JSX from WebPack</p>;
ReactDOM.render(template, document.getElementById('app'));

{% endhighlight %}

<br/>

### 055 One Component per File, 056 Source Maps with Webpack

webpack.config.js


<br/>

{% highlight javascript linenos %}

const path = require('path');

module.exports = {
    entry: './src/app.js',
    output: {
        path: path.join(__dirname, 'public'),
        filename: 'bundle.js'
    },
    module: {
        rules: [{
            loader: 'babel-loader',
            test: /\.js$/
        }]
    },
    devtool: 'cheap-module-eval-source-map'
};

{% endhighlight %}

<br/>

### 057 Webpack Dev Server
 
    $ npm install --save webpack-dev-server@2.5.1

<br/>

package.json

<br/>

{% highlight json linenos %}

    {
      "name": "INDECISION-APP",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "serve": "live-server public/",
        "build": "webpack",
        "dev-server": "webpack-dev-server"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "babel-preset-env": "^1.6.0",
        "babel-preset-react": "^6.24.1"
      },
      "dependencies": {
        "babel-cli": "^6.26.0",
        "babel-core": "^6.25.0",
        "babel-loader": "^7.1.1",
        "live-server": "^1.2.0",
        "react": "^16.0.0",
        "react-dom": "^16.0.0",
        "validator": "^8.0.0",
        "webpack": "^3.1.0",
        "webpack-dev-server": "^2.5.1"
      }
    }

{% endhighlight %}


<br/>

webpack.config.js

<br/>

{% highlight javascript linenos %}

const path = require('path');

module.exports = {
    entry: './src/app.js',
    output: {
        path: path.join(__dirname, 'public'),
        filename: 'bundle.js'
    },
    module: {
        rules: [{
            loader: 'babel-loader',
            test: /\.js$/
        }]
    },
    devtool: 'cheap-module-eval-source-map',
    devServer: {
        host: '0.0.0.0',
        port: 8080,
        contentBase: path.join(__dirname, 'public')
    }
};

{% endhighlight %}

<br/>

    $ npm run dev-server
