---
title:  "Collected Thoughts on React"
date:   2017-05-23 22:00:42 -0800
---

Recently I have picked up a course from Udemy on React & Redux. I currently am working on making components similar to YouTube's app. It is a YouTube video search app.

This project can be found here:
[React YouTube Project](https://github.com/WarrenU/ReduxSimpleStarterClone)

This involves 5 components, 2 Functional React components, and 3 Class based components. This app pulls videos from YouTube using their API. There is a search bar component that will update a state and call the YouTube search api to look for videos matching the search criteria. To set that up I am using a node package, youtube-api-search.

By using webpack and babel, we can create a bundled javascript file that includes our React components. This file is named bundle.js.The React components/views are written with JSX. The JSX code gets transpiled in to javascript which gets turned in to HTML. React allows great compartmentalizing techniques which makes it awesome.

React components can be thought of as factories. They are objects written to create objects that they represent. There are 2 types of components I am aware of. Functional components that return code, and Class-Based Components that can keep track of states, and utilize constructors.

to create a class based component you just need to access React.Component.
example:
{{<highlight javascript>}}
import React, {Component} from 'react';

class ExampleComponent extends Component{
  render(){
    return <div>Example!</div>;
  }
}

export default ExampleComponent

{{</highlight>}}

When you create a class based component you at minimum need to have a render function. At the end of your component you can export it so that you can then import it in your app/index.js (as an example), where your application is 'sewn' together.

States are react-tant to user events. When a component state is changed (on a user event for example), render gets called. In order to create a state within a class, you need to initialize it in the constructor.

{{<highlight html>}}
class MyReactComponent extends Component{
  constructor(props){
    super(props);
    this.state = {term: ''};
  }

  render(){
    return(
      <input onChange={(event) => this.setState(term: event.target.value)} />;

      <div>Value of input: {this.state.term}</div>
    );
  }
}
{{</highlight>}}


You absolutely should use self closing tags with JSX: <MyComponent />. You can even pass parameters into these components: <MyComponent item={myitem} />.

To implement your componetns, you basically just attach it to a class, or id etc via a selector.:

{{<highlight html>}}
ReactDOM.render(<AppComponent1 />, document.querySelector('.container'));
{{</highlight>}}

The above code is creating an instance of the AppComponent1 and is attaching it to a class called container.

These are my initial collection of thoughts. I am still learning React, but think it is very clean and fun to use.
