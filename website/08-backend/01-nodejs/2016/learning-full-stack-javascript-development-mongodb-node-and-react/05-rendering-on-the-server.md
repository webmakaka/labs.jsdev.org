---
layout: page
title: Learning Full-Stack JavaScript Development MongoDB, Node and React
permalink: /backend/nodejs/2016/learning-full-stack-javascript-development/rendering-on-the-server/
---

# Learning Full-Stack JavaScript Development: MongoDB, Node and React

<br/>

## 5. Rendering on the Server

<br/>

### 019 Fetching data from a remote API


    $ npm install --save axios

<br/>

**App.js**

{% highlight javascript linenos %}

import React from 'react';
import axios from 'axios';
import Header from './Header';
import ContestPreview from './ContestPreview';

class App extends React.Component {
    
    constructor(props){
        super(props);
        
        this.state = { 
            pageHeader: 'Naming Contests',
            contests: []
        };
    }
        
    componentDidMount() {
        axios.get('/api/contests')
            .then(resp => {
                this.setState({
                    contests: resp.data.contests
                });
                
            })
            .catch(console.error);
    }
    
    componentWillUnmount() {
        
    }

    render() {  
              
        return (
            <h2 className="App">
                <Header message= {this.state.pageHeader} />
                <div>        
                    {this.state.contests.map(contest =>                        
                        <ContestPreview key={contest.id} {...contest} />
                    )}
                </div>
            </h2>
        );
    }
};

export default App;


{% endhighlight %}


http://localhost/api/contests/



<br/>

### 020 Fetching data from the server side


**serverRender.js**

{% highlight javascript linenos %}

import config from './config';
import axios from 'axios';

axios.get(`${config.serverUrl}/api/contests`)
    .then(resp => {
        console.log(resp.data);
    });


{% endhighlight %}



<br/>

### 021 Server rendering with ReactDOMServer


<br/>

**serverRender.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import ReactDOMServer from 'react-dom/server';

import App from './src/components/App';

import config from './config';
import axios from 'axios';

const serverRender = () =>
    axios.get(`${config.serverUrl}/api/contests`)
        .then(resp => {
            // console.log(resp.data);
            return ReactDOMServer.renderToString(
                <App initialContests={resp.data.contests} />
            );
        });

export default serverRender;


{% endhighlight %}



<br/>

**server.js**

<br/>

{% highlight javascript linenos %}

import config from './config';
import apiRouter from './api';
import sassMiddleware from 'node-sass-middleware';
import path from 'path';

import express from 'express';
const server = express();

server.use(sassMiddleware({
    src: path.join(__dirname, 'sass'),
    dest: path.join(__dirname, 'public')
}));

server.set('view engine', 'ejs');

server.get('/', (req, res) => {
    
    serverRender()
        .then(content => {
            res.render('index', {
                content
            });
        })
        .catch(console.error);
});

import serverRender from './serverRender';

server.get('/about.html', (req, res) => {
    res.send('The about page');
});


server.use('/api', apiRouter);
server.use(express.static('public'));

server.listen(config.port, config.host, () => {
    console.info('Express listening on port ', config.port);
});

{% endhighlight %}



<br/>

### 022 Fix the checksum problem

<br/>

**index.ejs**

<br/>

{% highlight javascript linenos %}

<script type="text/javascript">
    window.initialData = <%- JSON.stringify(initialData) -%>
</script>

<%- include('header') -%>
    <div id="root"><%- initialMarkup -%></div>
<%- include('footer') -%>

{% endhighlight %}




<br/>

**index.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import ReactDOM from 'react-dom';

import App from './components/App';

ReactDOM.render(
    <App initialContests={window.initialData.contests} />,
    document.getElementById('root')
);

{% endhighlight %}



<br/>

**server.js**

<br/>

{% highlight javascript linenos %}

import config from './config';
import apiRouter from './api';
import sassMiddleware from 'node-sass-middleware';
import path from 'path';

import express from 'express';
const server = express();

server.use(sassMiddleware({
    src: path.join(__dirname, 'sass'),
    dest: path.join(__dirname, 'public')
}));

server.set('view engine', 'ejs');

server.get('/', (req, res) => {
    
    serverRender()
        .then(( {initialMarkup, initialData}) => {
            res.render('index', {
                initialMarkup,
                initialData
            });
        })
        .catch(console.error);
});

import serverRender from './serverRender';

server.get('/about.html', (req, res) => {
    res.send('The about page');
});


server.use('/api', apiRouter);
server.use(express.static('public'));

server.listen(config.port, config.host, () => {
    console.info('Express listening on port ', config.port);
});


{% endhighlight %}



<br/>

**serverRender.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import ReactDOMServer from 'react-dom/server';

import App from './src/components/App';

import config from './config';
import axios from 'axios';

const serverRender = () =>
    axios.get(`${config.serverUrl}/api/contests`)
        .then(resp => {
            return {
                initialMarkup: ReactDOMServer.renderToString(
                <App initialContests={resp.data.contests} />
                ),
                initialData: resp.data
            };
        });

export default serverRender;

{% endhighlight %}
