---
layout: dark-post
title: "How React Component LifeCycle method works"
description: "Understanding React Component LifeCycle Methods"
tags: [react.js]
comments: true
image:
    feature: react-logo.png
categories: [React.js]
share: true
---

# Life Cycle Phases in React Components

There are three life cycle phases in React Components


### Phase 1: Mounting

This phase only occurs once.In this phase component  `props` and `state` are defined
and configured.


 1. Initialize / Construction
 2. MyComponent.defaultProps
 3. `this.state= ...`
 4. `componentWillMount()`
 5. `render()
 6. Children initialization & life cycle kickoff
 7. `componentDidMount()`


### Phase 2: Update

In this phase we get new `props`, change `state`, handle
user interactions and communicate with component hierarchy.


1. `componentWillReceiveProps()`
2. `shouldComponentUpdate()`
3. `componentWillUpdate()`
4. `render()`
5. Child Life Cycle methods
6. `componentDidUpdate()`



### Phase 3: Unmount

This phase occurs when a component instance is unmounted from the Native UI.
This can occur when the user navigates away


1. `componentWillUnmount()`
2.  Children Life Cycle methods
3.  Instance destroyed for Grabage Collection



### componentWillMount

*When it is called ?*


1. Called only one time before initial rendering
2. Called before `render()`

*What can we do in this method ?*

- In this method props and initial state are defined

<br/>


#### Example



```js

import React from 'react';

class CustomerPage extends React.Component {
  constructor(props) {
    super(props);
    this.state = { customer : { type: '',age:0 ,name:''} } ;
  }

  componentWillMount() {

    let customer = {};

    if (this.props.customer.age > 70) {

      customer.type = 'regular';
      customer.name ='Haider';
      customer.age = this.props.customer.age;

    } else if (this.props.customer.age < 18) {

       customer.type = 'young';
       customer.name ='Malik';
       customer.age = this.props.customer.age;

    } else {

      customer.type = 'lower';
      customer.name = 'Salik';
      customer.age = this.props.customer.age;
    }
    this.setState({ customer });  
  }
render() {
    return (

      <div>
        { this.state.customer.name } (age: { this.state.customer.age })
      </div>

    );
  }
}

export default CustomerPage;

```

<br/>

### componentDidMount

 *When it is Called?*


 - Called once all our children elements and Component instances
 are mounted onto Native UI

*What can we do in this method ?*

- You can integrate external library in this method Can do Ajax Call

<br/>

#### Example


```javascript

import React from 'react';
import ReactDOM from 'react-dom';
import c3 from 'c3';

export default class Chart extends React.Component {

  componentDidMount() {
    this.chart = c3.generate({
      bindto: ReactDOM.findDOMNode(this.refs.chart),
      data: {
        columns: [
          ['data1', 30, 200, 100, 400, 150, 250],
          ['data2', 50, 20, 10, 40, 15, 25]
        ]
      }
    });
  }

  render() {
    return (
      <div ref="chart"></div>
    );
  }
}
```
<br/>

### componentWillReceiveProps

*When it is Called ?*

- This method is called when props are passed to the Component instance.

*Why it is Called ?*

- React has no way of knowing that the data did not change.
Therefore React needs to call `componentWillReceiveProps`,because
the component needs to be notified of the new props.

- `componentWillReceiveProps` allows us to check and see if new
props are coming in and we can make choices based on data.

<br/>

#### Example


```javascript
class SignInForm extends React.Component {

  constructor(props){
    super(props);
  }
handleChange(event) {
   this.setState({ name: event.currentTarget.value });
 }

 render() {
   return (
     <div>
      <input type="text" onChange={ this.handleChange } />
       <Person name={ this.state.name } />
     </div>
   );
 }
 }

class  Person extends React.Component {
  constructor(props) {
    super(props);

  }

  componentWillReceiveProps(newProps){
    if(this.props != newProps){
      console.log(newProps);
    }
  }
}

```


When user typed in the  `<input />`. we invoke a setState() method.
This will trigger update phase for both SignInForm and Person Component.Person Component will receive newProps .

<br/>

### shouldComponentUpdate

*When it is Called ?*

- This method invoked whenever the component receives new props
or a change in state occurs.

- By default, shouldComponentUpdate returns a true value. If you
override it and return false, the component will never be updated
despite receiving updated props or a new state.

*What can you do in this method ?*

- If you create a component that should only be updated if certain
conditions are met.

<br/>

#### Example

```javascript

class CounterButton extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: 1};
  }

  shouldComponentUpdate(nextProps, nextState) {
    if (this.props.color !== nextProps.color) {
      return true;
    }
    if (this.state.count !== nextState.count) {
      return true;
    }
    return false;
  }

  render() {
    return (
      <button
        color={this.props.color}
        onClick={() => this.setState(state => ({count: state.count + 1}))}>
        Count: {this.state.count}
      </button>
    );
  }
}

```

If the only way your component ever changes is when the `props.color` or the `state.count` variable changes

<br/>

### componentWillUpdate

*When it is Called ?*

- Just like `componentWillMount()` this method is called before
`render()`.  

- The method `componentWillUpdate()` is similar to `componentWillMount()`. The difference being that `componentWillUpdate()` called every time re-render is required,
such as when this.state() is called.

*What can we do in this method ?*

- The `componentWillUpdate()` is a chance for us to handle configuration changes and prepare for the next render.

<br/>


#### Example

```javascript

componentWillUpdate(nextProps, nextState) {
  if (nextState.open == true && this.state.open == false) {
    this.props.onWillOpen();
  }
}
```

<br/>


### componentDidUpdate

*When it is Called ?*

- Just like `componentDidMount()`, the `componentDidUpdate()` is called after all of the children are updated.

*What can we do in this method ?*

- The most common uses of componentDidUpdate() is managing 3rd party UI elements and interacting with the Native UI. When using 3rd Party libraries, like our Chart example, we need to update the UI library with new data.

<br/>

#### Example

```javascript

componentDidUpdate(prevProps, prevState) {
  // only update chart if the data has changed
  if (prevProps.data !== this.props.data) {
    this.chart = c3.load({
      data: this.props.data
    });
  }
}
```

<br/>


### componentWillUnmount

*When it is Called?*

- This is invoked just before the component is unmounted
from the DOM.


*What can we do in this method?*

- If you need to clean up the memory or invalidate timers,
this is the place to do it.
<br/>
<br/>

 {% include disqus.html %}
