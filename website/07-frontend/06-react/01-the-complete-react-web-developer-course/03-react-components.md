---
layout: page
title: React.js - The Complete React Web Developer Course (2nd Edition)
permalink: /frontend/react/the-complete-react-web-developer-course-2nd-edition/react-components/
---

# The Complete React Web Developer Course (2nd Edition)

<br/>

## 04 React Components

<br/>
    
### 026 Creating a React Component


<br/>
    
    $ vi src/app.js
    
<br/>


{% highlight javascript linenos %}

class Header extends React.Component {
    render() {
        return  (
            <div>
              <h1>Indecision</h1>
              <h2>Put your life in the hand of a computer</h2>
            </div>  
          );
    }
}

class Action extends React.Component {
    render() {
        return (
          <div>
            <button>What should i do?</button>
          </div>  
        );
    }
}

class Options extends React.Component {
    render() {
        return (
          <div>
            Options component here
          </div>  
        );
    }
}

class AddOption extends React.Component {
    render() {
        return (
          <div>
            AddOption component here
          </div>  
        );
    }
}


const jsx = (
    <div>
        <Header />
        <Action />
        <Options />
        <AddOption />
    </div>
);

ReactDOM.render(jsx, document.getElementById('app'));

{% endhighlight %}



<br/>

### 027 Nesting Components

{% highlight javascript linenos %}

class IndecisionApp extends React.Component {
    render() {
        return  (
            <div>
              <Header />
              <Action />
              <Options />
              <AddOption />
            </div>  
          );
    }
}


class Header extends React.Component {
    render() {
        return  (
            <div>
              <h1>Indecision</h1>
              <h2>Put your life in the hand of a computer</h2>
            </div>  
          );
    }
}

class Action extends React.Component {
    render() {
        return (
          <div>
            <button>What should i do?</button>
          </div>  
        );
    }
}

class Options extends React.Component {
    render() {
        return (
          <div>
            Options component here
            <Option />
          </div>  
        );
    }
}

class Option extends React.Component {
    render() {
        return (
          <div>
            Option component here
          </div>  
        );
    }
}

class AddOption extends React.Component {
    render() {
        return (
          <div>
            AddOption component here
          </div>  
        );
    }
}


const jsx = (
    <div>
        <IndecisionApp />
    </div>
);

ReactDOM.render(jsx, document.getElementById('app'));

{% endhighlight %}


<br/>

### 028 Component Props



{% highlight javascript linenos %}

class IndecisionApp extends React.Component {
    render() {

        const title = 'Indecision';
        const subtitle = 'Put your life in the hand of a computer';
        const options = ['Thing one', 'Thing two', 'Thing four'];

        return  (
            <div>
              <Header title={title} subtitle={subtitle} />
              <Action />
              <Options options={options} />
              <AddOption />
            </div>  
          );
    }
}


class Header extends React.Component {
    render() {
        return  (
            <div>
              <h1>{this.props.title}</h1>
              <h2>{this.props.subtitle}</h2>
            </div>  
          );
    }
}

class Action extends React.Component {
    render() {
        return (
          <div>
            <button>What should i do?</button>
          </div>  
        );
    }
}

class Options extends React.Component {
    render() {
        return (
          <div>
          {
            this.props.options.map((option) => <Option key={option} optionText={option} />)
          }
          </div>  
        );
    }
}

class Option extends React.Component {
    render() {
        return (
          <div>
            Option: {this.props.optionText}
          </div>  
        );
    }
}

class AddOption extends React.Component {
    render() {
        return (
          <div>
            AddOption component here
          </div>  
        );
    }
}


const jsx = (
    <div>
        <IndecisionApp />
    </div>
);

ReactDOM.render(jsx, document.getElementById('app'));

{% endhighlight %}



<br/>

### 029 Events Methods, 030 Method Binding, 031 What Is Component State, 032 Adding State to Counter App Part I, 033 Adding State to Counter App Part II, 035 Build It Adding State to VisibilityToggle, 036 Indecision State Part I, 037 Indecision State Part II


{% highlight javascript linenos %}


class IndecisionApp extends React.Component {

    constructor(props){
        super(props);
        this.handleDeleteOptions = this.handleDeleteOptions.bind(this);
        this.handlePick = this.handlePick.bind(this);
        this.handleAddOption = this.handleAddOption.bind(this);
        


        this.state = {
            options: ['Thing one', 'Thing two', 'Thing three']
        }
    }

    handleDeleteOptions(){
        this.setState(() => {
            return {
                options: []
            };
        });
    }

    handlePick(){
       const randomNum = Math.floor(Math.random() * this.state.options.length);
       const option = this.state.options[randomNum];
       alert(option);
    }

    handleAddOption(option){

        if (!option) {
            return 'Enter valid value to add item';
        } else if (this.state.options.indexOf(option) > -1) {
            return 'This option already exists';
        }

        this.setState((prevState) => {
            return {
                options: prevState.options.concat(option)
            }
        });
    }


    render() {

        const title = 'Indecision';
        const subtitle = 'Put your life in the hand of a computer';

        return  (
            <div>
              <Header title={title} subtitle={subtitle} />
                <Action 
                    hasOptions={this.state.options.length > 0}
                    handlePick={this.handlePick}
                />
                <Options 
                    options={this.state.options} 
                    handleDeleteOptions={this.handleDeleteOptions}
                />
              <AddOption 
                handleAddOption={this.handleAddOption}
              />
            </div>  
          );
    }
}


class Header extends React.Component {
    render() {
        return  (
            <div>
              <h1>{this.props.title}</h1>
              <h2>{this.props.subtitle}</h2>
            </div>  
          );
    }
}

class Action extends React.Component {
    render() {
        return (
          <div>
            <button 
                onClick={this.props.handlePick} 
                disabled={!this.props.hasOptions}
             >
                What should i do?
            </button>
          </div>  
        );
    }
}

class Options extends React.Component {

    render() {
        return (
          <div>
            <button onClick={this.props.handleDeleteOptions} >Remove All</button>
          {
            this.props.options.map((option) => <Option key={option} optionText={option} />)
          }
          </div>  
        );
    }
}

class Option extends React.Component {
    render() {
        return (
          <div>
            Option: {this.props.optionText}
          </div>  
        );
    }
}

class AddOption extends React.Component {

    constructor(props) {
        super(props);
        this.handleAddOption = this.handleAddOption.bind(this);
        this.state = {
            error: undefined
        };
    }

    handleAddOption(e) {
       e.preventDefault();
       
       const option = e.target.elements.option.value.trim();
       const error = this.props.handleAddOption(option);

       this.setState(() => {
           return { error };
       });

    }

    render() {
        return (
          <div>
          {this.state.error && <p>{this.state.error}</p>}
            <form onSubmit={this.handleAddOption} >
                <input type="text" name="option" />
                <button>Add Option</button>
            </form>
          </div>  
        );
    }
}


const jsx = (
    <div>
        <IndecisionApp />
    </div>
);

ReactDOM.render(jsx, document.getElementById('app'));

{% endhighlight %}
