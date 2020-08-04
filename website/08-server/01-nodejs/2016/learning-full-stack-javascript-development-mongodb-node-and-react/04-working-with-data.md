---
layout: page
title: Learning Full-Stack JavaScript Development MongoDB, Node and React
permalink: /server/nodejs/2016/learning-full-stack-javascript-development/working-with-data/
---

# Learning Full-Stack JavaScript Development: MongoDB, Node and React

<br/>

## 4. Working with Data

<br/>

### 015 Loading the test data

    $ npm install --save json-loader


    <br/>

**webpack.config.js**

{% highlight javascript linenos %}

const path = require('path');

module.exports = {
entry: './src/index.js',
output: {
path: path.join(\_\_dirname, 'public'),
filename: 'bundle.js'
},
module: {
loaders: [
{
loader: 'json-loader',
test: /\.json$/
},
{
loader: 'babel-loader',
test: /\.js$/,
exclude: /node_modules/
}
]
},
devtool: 'cheap-module-eval-source-map'
};

{% endhighlight %}

<br/>

### 016 Displaying a list of objects

<br/>

**index.js**

{% highlight javascript linenos %}

import React from 'react';
import ReactDOM from 'react-dom';

import data from './testData';
import App from './components/App';

ReactDOM.render(
<App contests={data.contests} />,
document.getElementById('root')
);

{% endhighlight %}

<br/>

**App.js**

{% highlight javascript linenos %}

import React from 'react';
import Header from './Header';
import ContestPreview from './ContestPreview';

class App extends React.Component {
  
 constructor(props){
super(props);
this.pageHeader = 'Naming Contests';
this.state = { test: 42 };
}
  
 componentDidMount() {
  
 }
  
 componentWillUnmount() {
  
 }

    render() {
        return (
            <h2 className="App">
                <Header message= {this.pageHeader} />
                <div>
                    {this.props.contests.map(contest =>
                        <ContestPreview {...contest} />
                    )}
                </div>
            </h2>
        );
    }

};

export default App;

{% endhighlight %}

<br/>

### 017 Using Sass with Node

    $ npm install --save node-sass-middleware

<br/>

**server.js**

{% highlight javascript linenos %}

import config from './config';
import apiRouter from './api';
import sassMiddleware from 'node-sass-middleware';
import path from 'path';

import express from 'express';
const server = express();

server.use(sassMiddleware({
src: path.join(**dirname, 'sass'),
dest: path.join(**dirname, 'public')
}));

server.set('view engine', 'ejs');

server.get('/', (req, res) => {
res.render('index', {
content: 'Hello Express and <em>EJS!</em>'
});
});

server.get('/about.html', (req, res) => {
res.send('The about page');
});

server.use('/api', apiRouter);
server.use(express.static('public'));

server.listen(config.port, () => {
console.info('Express listening on port ', config.port);
});

{% endhighlight %}

<br/>

### 018 Reading from the state

<br/>

**index.js**

{% highlight javascript linenos %}

import React from 'react';
import ReactDOM from 'react-dom';

import App from './components/App';

ReactDOM.render(
<App />,
document.getElementById('root')
);

{% endhighlight %}

<br/>

**App.js**

{% highlight javascript linenos %}

import React from 'react';
import Header from './Header';
import ContestPreview from './ContestPreview';
import data from '../testData';

class App extends React.Component {
  
 constructor(props){
super(props);
this.pageHeader = 'Naming Contests';
this.state = { test: 42 };
this.contests = data.contests;
}
  
 componentDidMount() {
// this.contests = data.contests;
}
  
 componentWillUnmount() {
  
 }

    render() {

        return (
            <h2 className="App">
                <Header message= {this.pageHeader} />
                <div>
                    {this.contests.map(contest =>
                        <ContestPreview key={contest.id} {...contest} />
                    )}
                </div>
            </h2>
        );
    }

};

export default App;

{% endhighlight %}
