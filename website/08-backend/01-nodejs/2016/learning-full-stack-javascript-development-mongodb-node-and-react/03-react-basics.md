---
layout: page
title: Learning Full-Stack JavaScript Development MongoDB, Node and React
permalink: /backend/nodejs/2016/learning-full-stack-javascript-development/react-basics/
---

# Learning Full-Stack JavaScript Development: MongoDB, Node and React

<br/>

## 3. React Basics


<br/>

### 010 React components


    $ npm install --save prop-types
    
<br/>

{% highlight javascript linenos %}

import React from 'react';
import ReactDOM from 'react-dom';
import PropTypes from 'prop-types';

const App = (props) => {
    return (
        <h2 className="text-center">
            {props.headerMessage}
        </h2>
    );
};

App.propTypes = {
    headerMessage: PropTypes.string.isRequired
};

App.defaultProps = {
    headerMessage: 'Hello!'
}


ReactDOM.render(
    <App />,
    document.getElementById('root')
);


// ReactDOM.render(
//     <App headerMessage="Hello props"/>,
//     document.getElementById('root')
// );

{% endhighlight %}

<br/>

    $ npm run dev
    $ npm start


<br/>

### 011 Component composability

<br/>

{% highlight javascript linenos %}


import React from 'react';
import ReactDOM from 'react-dom';
import PropTypes from 'prop-types';


const Header = ({ message }) => {
    return (
        <h2 className="Header text-center">
            { message }
        </h2>
    );
};

Header.propTypes = {
    message: PropTypes.string.isRequired
};

const App = () => {
    return (
        <h2 className="App">
            <Header message="Naming Contests" />
            <div>
                ...
            </div>
        </h2>
    );
};

ReactDOM.render(
    <App />,
    document.getElementById('root')
);


{% endhighlight %}


<br/>

### 012 Components with modules

<br/>

**App.js**


{% highlight javascript linenos %}

import React from 'react';
import Header from './Header';

const App = () => {
    return (
        <h2 className="App">
            <Header message="Naming Contests" />
            <div>
                ...
            </div>
        </h2>
    );
};


export default App;

{% endhighlight %}



<br/>

**Header.js**


{% highlight javascript linenos %}

import React from 'react';
import PropTypes from 'prop-types';

const Header = ({ message }) => {
    return (
        <h2 className="Header text-center">
            { message }
        </h2>
    );
};

Header.propTypes = {
    message: PropTypes.string.isRequired
};


export default Header;


{% endhighlight %}



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

### 013 Component state

<br/>

**App.js**

{% highlight javascript linenos %}

import React from 'react';
import Header from './Header';

class App extends React.Component {
    
    constructor(props){
        super(props);
        this.pageHeader = 'Naming Contests';
        this.state = { test: 42 };
    }

    render() {
        return (
            <h2 className="App">
                <Header message= {this.pageHeader} />
                <div>
                    {this.state.test}
                </div>
            </h2>
        );
    }
};

export default App;

{% endhighlight %}


<br/>

### 014 Component life cycle


    componentDidMount() {
        
    }

    componentWillUnmount() {
        
    }
    
    
