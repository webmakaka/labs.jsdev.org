---
layout: page
title: Learning Full-Stack JavaScript Development MongoDB, Node and React
permalink: /server/nodejs/2016/learning-full-stack-javascript-development/routing-on-client-and-server/
---

# Learning Full-Stack JavaScript Development: MongoDB, Node and React

<br/>

## 6. Routing on Client and Server

<br/>

### 023 Handling the contest click event

<br/>

**App.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import axios from 'axios';
import Header from './Header';
import ContestList from './ContestList';

class App extends React.Component {
  
 constructor(props){
super(props);
  
 this.state = {
pageHeader: 'Naming Contests',
contests: this.props.initialContests
};
}
  
 componentDidMount() {

    }

    componentWillUnmount() {

    }

    render() {

        return (
            <h2 className="App">
                <Header message= {this.state.pageHeader} />
                <ContestList contests={this.state.contests} />
            </h2>
        );
    }

};

export default App;

{% endhighlight %}

<br/>

**ContestList.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import ContestPreview from './ContestPreview';
import PropTypes from 'prop-types';

const ContestList = ({ contests }) => (
<div className="ContestList">  
 {contests.map(contest =>  
 <ContestPreview key={contest.id} {...contest} />
)}
</div>
);

ContestList.propTypes = {
contests: PropTypes.array
}

export default ContestList;

{% endhighlight %}

<br/>

**ContestPreview.js**

<br/>

{% highlight javascript linenos %}

import React, { Component } from 'react';
import PropTypes from 'prop-types';

class ContestPreview extends Component {
  
 constructor(props){
super(props);
this.handleClick = this.handleClick.bind(this);
}

    handleClick(){
        console.log(this.props.id);
    };

    render() {
        return (
            <div className="link ContestPreview" onClick={this.handleClick}>
                <div className="category-name">
                    {this.props.categoryName}
                </div>
                <div className="contest-name">
                    <div>{this.props.contestName}</div>
                </div>
            </div>
        );
    }

}

ContestPreview.propTypes = {
categoryName: PropTypes.string.isRequired,
contestName: PropTypes.string.isRequired
}

export default ContestPreview;

{% endhighlight %}

<br/>

### 024 Navigating to a contest

<br/>

**App.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import axios from 'axios';
import Header from './Header';
import ContestList from './ContestList';

const pushState = (obj, url) => window.history.pushState(obj, '', url);

class App extends React.Component {
  
 constructor(props){
super(props);
  
 this.state = {
pageHeader: 'Naming Contests',
contests: this.props.initialContests
};
}
  
 componentDidMount() {

    }

    componentWillUnmount() {

    }

    fetchContest(contestId){
        pushState(
            { currentContestId: contestId },
            `/contest/${contestId}`
        )
    };

    render() {

        return (
            <h2 className="App">
                <Header message= {this.state.pageHeader} />
                <ContestList
                    onContestClick={this.fetchContest}
                    contests={this.state.contests} />
            </h2>
        );
    }

};

export default App;

{% endhighlight %}

<br/>

**ContestList.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import ContestPreview from './ContestPreview';
import PropTypes from 'prop-types';

const ContestList = ({ contests, onContestClick }) => (
<div className="ContestList">  
 {contests.map(contest =>  
 <ContestPreview
key={contest.id}
onClick={ onContestClick }
{...contest} />
)}
</div>
);

ContestList.propTypes = {
contests: PropTypes.array,
onContestClick: PropTypes.func.isRequired
}

export default ContestList;

{% endhighlight %}

<br/>

**ContestPreview.js**

<br/>

{% highlight javascript linenos %}

import React, { Component } from 'react';
import PropTypes from 'prop-types';

class ContestPreview extends Component {
  
 constructor(props){
super(props);
this.handleClick = this.handleClick.bind(this);
}

    handleClick(){
        // console.log(this.props.id);
        this.props.onClick(this.props.id);
    };

    render() {
        return (
            <div className="link ContestPreview" onClick={this.handleClick}>
                <div className="category-name">
                    {this.props.categoryName}
                </div>
                <div className="contest-name">
                    <div>{this.props.contestName}</div>
                </div>
            </div>
        );
    }

}

ContestPreview.propTypes = {
id: PropTypes.number.isRequired,
categoryName: PropTypes.string.isRequired,
contestName: PropTypes.string.isRequired,
onClick: PropTypes.func.isRequired
}

export default ContestPreview;

{% endhighlight %}

<br/>

### 025 Looking up the contest on route change

<br/>

**App.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import axios from 'axios';
import Header from './Header';
import ContestList from './ContestList';
import Contest from './Contest';

const pushState = (obj, url) => window.history.pushState(obj, '', url);

class App extends React.Component {
  
 constructor(props){
super(props);
this.fetchContest = this.fetchContest.bind(this);
this.currentContent = this.currentContent.bind(this);
  
 this.state = {
pageHeader: 'Naming Contests',
contests: this.props.initialContests
};
}
  
 componentDidMount() {

    }

    componentWillUnmount() {

    }

    fetchContest(contestId){

        pushState(
            { currentContestId: contestId },
            `/contest/${contestId}`
        );

        this.setState({
            pageHeader: this.state.contests[contestId].contestName,
            currentContestId: contestId
        });
    };

    currentContent() {
        if (this.state.currentContestId) {
            return <Contest {...this.state.contests[this.state.currentContestId]} />;
        }

        return <ContestList
            onContestClick={this.fetchContest}
            contests={this.state.contests} />;
    }

    render() {

        return (
            <h2 className="App">
                <Header message= {this.state.pageHeader} />
                {this.currentContent()}
            </h2>
        );
    }

};

export default App;

{% endhighlight %}

<br/>

**Contest.js**

<br/>

{% highlight javascript linenos %}

import React, { Component} from 'react';
import PropTypes from 'prop-types';

class Contest extends React.Component {
render() {
return (
<div className="Contest">
{this.props.id}
</div>
);
  
 }
}

Contest.propTypes = {
id: PropTypes.number.isRequired
}

export default Contest;

{% endhighlight %}

<br/>

**ContestList.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import ContestPreview from './ContestPreview';
import PropTypes from 'prop-types';

const ContestList = ({ contests, onContestClick }) => (
<div className="ContestList">  
 {Object.keys(contests).map(contestId =>  
 <ContestPreview
key={contestId}
onClick={ onContestClick }
{...contests[contestId]} />
)}
</div>
);

ContestList.propTypes = {
contests: PropTypes.object,
onContestClick: PropTypes.func.isRequired
}

export default ContestList;

{% endhighlight %}

<br/>

### 026 Fetching contest information from the API

<br/>

**api/index.js**

<br/>

{% highlight javascript linenos %}

import express from 'express';
import data from '../src/testData';

const router = express.Router();

const contests = data.contests.reduce((obj, contest) => {
obj[contest.id] = contest;
return obj;
}, {});

router.get('/contests', (req, res) => {
res.send({ contests: contests });
});

router.get('/contests/:contestId', (req, res) => {
let contest = contests[req.params.contestId];
contest.description = 'Any Text';
res.send({ contest });
});

export default router;

{% endhighlight %}

<br/>

**api.js**

<br/>

{% highlight javascript linenos %}

import axios from 'axios';

export const fetchContest = contestId => {
return axios.get(`/api/contests/${contestId}`)
.then( resp => resp.data.contest )
};

{% endhighlight %}

<br/>

**Contest.js**

<br/>

{% highlight javascript linenos %}

import React, { Component} from 'react';
import PropTypes from 'prop-types';

class Contest extends React.Component {
  
 render() {
  
 return (
<div className="Contest">
{this.props.description}
</div>
);
}
}

Contest.propTypes = {
description: PropTypes.string.isRequired
}

export default Contest;

{% endhighlight %}

<br/>

**App.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import axios from 'axios';
import Header from './Header';
import ContestList from './ContestList';
import Contest from './Contest';
import \* as api from '../api';

const pushState = (obj, url) => window.history.pushState(obj, '', url);

class App extends React.Component {
  
 constructor(props){
  
 super(props);
  
 this.fetchContest = this.fetchContest.bind(this);
this.currentContent = this.currentContent.bind(this);
  
 this.state = {
pageHeader: 'Naming Contests',
contests: this.props.initialContests,
};
}
  
 componentDidMount() {

    }

    componentWillUnmount() {

    }

    fetchContest(contestId){

        pushState(
            { currentContestId: contestId },
            `/contest/${contestId}`
        );


        api.fetchContest(contestId).then(contest => {

            this.setState({
                pageHeader: contest.contestName,
                currentContestId: contest.id,
                contests: {
                    [contest.id]: contest
                }
            });
        });
    };

    currentContent() {

        if (this.state.currentContestId) {
            return <Contest {...this.state.contests[this.state.currentContestId]} />;
        }

        return <ContestList
            onContestClick={this.fetchContest}
            contests={this.state.contests} />;
    }

    render() {

        return (
            <h2 className="App">
                <Header message= {this.state.pageHeader} />
                {this.currentContent()}
            </h2>
        );
    }

};

export default App;

{% endhighlight %}

http://localhost/api/contests/4

<br/>

### 027 A bit of refactoring

<br/>

**App.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import axios from 'axios';
import Header from './Header';
import ContestList from './ContestList';
import Contest from './Contest';
import \* as api from '../api';
import PropTypes from 'prop-types';

const pushState = (obj, url) => window.history.pushState(obj, '', url);

class App extends React.Component {
  
 constructor(props){
  
 super(props);
  
 this.fetchContest = this.fetchContest.bind(this);
this.currentContent = this.currentContent.bind(this);
  
 // static propTypes = {
// initialData: PropTypes.object.isRequired
// }

        this.state = this.props.initialData;
    }

    componentDidMount() {

    }

    componentWillUnmount() {

    }

    fetchContest(contestId){

        pushState(
            { currentContestId: contestId },
            `/contest/${contestId}`
        );


        api.fetchContest(contestId).then(contest => {

            this.setState({
                currentContestId: contest.id,
                contests: {
                    [contest.id]: contest
                }
            });
        });
    };


    currentContest(){
        return this.state.contests[this.state.currentContestId]
    }

    pageHeader() {
        if(this.state.currentContestId){
            return this.currentContest().contestName;
        }

        return 'Naming Contests';

    }

    currentContent() {

        if (this.state.currentContestId) {
            return <Contest {...this.currentContest()} />;
        }

        return <ContestList
            onContestClick={this.fetchContest}
            contests={this.state.contests} />;
    }

    render() {

        return (
            <h2 className="App">
                <Header message= {this.pageHeader()} />
                {this.currentContent()}
            </h2>
        );
    }

};

export default App;

{% endhighlight %}

<br/>

**index.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import ReactDOM from 'react-dom';

import App from './components/App';

ReactDOM.render(
<App initialData={window.initialData} />,
document.getElementById('root')
);

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
<App initialData={resp.data} />
),
initialData: resp.data
};
});

export default serverRender;

{% endhighlight %}

<br/>

### 028 Server-side routing for a contest

<br/>

<br/>

**server.js**

<br/>

{% highlight javascript linenos %}

import config from './config';
import apiRouter from './api';
import sassMiddleware from 'node-sass-middleware';
import path from 'path';
import serverRender from './serverRender';

import express from 'express';
const server = express();

server.use(sassMiddleware({
src: path.join(**dirname, 'sass'),
dest: path.join(**dirname, 'public')
}));

server.set('view engine', 'ejs');

server.get(['/', '/contest/:contestId'], (req, res) => {  
 serverRender(req.params.contestId)
.then(( {initialMarkup, initialData}) => {
res.render('index', {
initialMarkup,
initialData
});
})
.catch(console.error);
});

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

const getApiUrl = contestId => {
  
 console.log('contestId1');
console.log(contestId);
  
 if (contestId) {
return `${config.serverUrl}/api/contests/${contestId}`;
}
return `${config.serverUrl}/api/contests`;
}

const getInitialData = (contestId, apiData) => {  
 if (contestId){
return {
currentContestId: apiData.contest.id,
contests: {
[apiData.contest.id]: apiData.contest
}
};
}
  
 return {
contests: apiData.contests
}
};

const serverRender = (contestId) =>
axios.get(getApiUrl(contestId))
.then(resp => {

            const initialData = getInitialData(contestId, resp.data);

            return {
                initialMarkup: ReactDOMServer.renderToString(
                <App initialData={initialData} />
                ),
                initialData
            };
        });

export default serverRender;

{% endhighlight %}

<br/>

### 029 Navigating to a list of contests

<br/>

**api.js**

<br/>

{% highlight javascript linenos %}

import axios from 'axios';

export const fetchContest = contestId => {
return axios.get(`/api/contests/${contestId}`)
.then( resp => resp.data.contest )
};

export const fetchContestList = () => {
return axios.get(`/api/contests`)
.then( resp => resp.data.contests )
};

{% endhighlight %}

<br/>

**Contest.js**

<br/>

{% highlight javascript linenos %}

import React, { Component} from 'react';
import PropTypes from 'prop-types';

class Contest extends React.Component {
  
 render() {
  
 return (
<div className="Contest">
<div className="contest-description">
{this.props.description}
</div>
<div className="home-link link"
                    onClick={this.props.contestListClick}
                    >
Contest List
</div>
</div>
);
}
}

Contest.propTypes = {
description: PropTypes.string.isRequired,
contestListClick: PropTypes.func.isRequired
}

export default Contest;

{% endhighlight %}

<br/>

**App.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import axios from 'axios';
import Header from './Header';
import ContestList from './ContestList';
import Contest from './Contest';
import \* as api from '../api';
import PropTypes from 'prop-types';

const pushState = (obj, url) => window.history.pushState(obj, '', url);

class App extends React.Component {
  
 constructor(props){
  
 super(props);
  
 this.fetchContest = this.fetchContest.bind(this);
this.fetchContestList = this.fetchContestList.bind(this);
this.currentContent = this.currentContent.bind(this);
  
 // static propTypes = {
// initialData: PropTypes.object.isRequired
// }

        this.state = this.props.initialData;
    }

    componentDidMount() {

    }

    componentWillUnmount() {

    }

    fetchContest(contestId) {

        pushState(
            { currentContestId: contestId },
            `/contest/${contestId}`
        );


        api.fetchContest(contestId).then(contest => {

            this.setState({
                currentContestId: contest.id,
                contests: {
                    [contest.id]: contest
                }
            });
        });
    };


    fetchContestList() {

        pushState(
            { currentContestId: null },
            `/`
        );

        api.fetchContestList().then(contests => {

            this.setState({
                currentContestId: null,
                contests
            });
        });
    };


    currentContest(){
        return this.state.contests[this.state.currentContestId]
    }

    pageHeader() {
        if(this.state.currentContestId){
            return this.currentContest().contestName;
        }

        return 'Naming Contests';

    }

    currentContent() {

        if (this.state.currentContestId) {
            return <Contest
                contestListClick={this.fetchContestList}
                {...this.currentContest()} />;
        }

        return <ContestList
            onContestClick={this.fetchContest}
            contests={this.state.contests} />;
    }

    render() {

        return (
            <h2 className="App">
                <Header message= {this.pageHeader()} />
                {this.currentContent()}
            </h2>
        );
    }

};

export default App;

{% endhighlight %}

<br/>

### 030 Handling the browser's back button

<br/>

**App.js**

<br/>

{% highlight javascript linenos %}

import React from 'react';
import axios from 'axios';
import Header from './Header';
import ContestList from './ContestList';
import Contest from './Contest';
import \* as api from '../api';
import PropTypes from 'prop-types';

const pushState = (obj, url) => window.history.pushState(obj, '', url);

const onPopState = handler => {
window.onpopstate = handler;
}

class App extends React.Component {
  
 constructor(props){
  
 super(props);
  
 this.fetchContest = this.fetchContest.bind(this);
this.fetchContestList = this.fetchContestList.bind(this);
this.currentContent = this.currentContent.bind(this);
  
 this.state = this.props.initialData;
}
  
 componentDidMount() {
onPopState((event) => {
this.setState({
currentContestId: (event.state || {}).currentContestId
})
});
}
  
 componentWillUnmount() {
onPopState(null);
}
  
 fetchContest(contestId) {
  
 pushState(
{ currentContestId: contestId },
`/contest/${contestId}`
);
  
  
 api.fetchContest(contestId).then(contest => {
  
 this.setState({
currentContestId: contest.id,
contests: {
[contest.id]: contest
}
});  
 });
};
  
  
 fetchContestList() {
  
 pushState(
{ currentContestId: null },
`/`
);
  
 api.fetchContestList().then(contests => {
  
 this.setState({
currentContestId: null,
contests
});  
 });
};
  
  
 currentContest(){
return this.state.contests[this.state.currentContestId]
}
  
 pageHeader() {
if(this.state.currentContestId){
return this.currentContest().contestName;
}
  
 return 'Naming Contests';

    }

    currentContent() {

        if (this.state.currentContestId) {
            return <Contest
                contestListClick={this.fetchContestList}
                {...this.currentContest()} />;
        }

        return <ContestList
            onContestClick={this.fetchContest}
            contests={this.state.contests} />;
    }

    render() {

        return (
            <h2 className="App">
                <Header message= {this.pageHeader()} />
                {this.currentContent()}
            </h2>
        );
    }

};

export default App;

{% endhighlight %}
