---
layout: post
title:      "Types of React Components "
date:       2021-03-18 16:55:22 +0000
permalink:  types_of_react_components
---

Components are the life-blood of React. But what is a component? According to w3schools.com, "Components are independent and reusable bits of code." There are two main types of components, class and functional. The syntax and capabilities are different, but the most recent updates to React allow both of these types to do similar things. 

### Class Components
Class componnents can receive props and have state and lifecycle methods. The name of React components must start with an upper case letter and must extend React.Component. This statement allows the component to access  React.Component's functions. Class components must have a a render() method and return HTML or a JSX object.

```
import React from 'react';

class Example extends React.component {

   render(){
	    return <div>Returned HTML</>
		}
		
}

export default Example;
```


Class components can also utilize the ```constructor()``` method to initialize state. 

```
import React from 'react';

class Example extends React.component {
  constructor(){
	  super();
		this.state = {
		  color: "red"
		};
	}
	
   render(){
	    return <div>Returned HTML</>
		}
		
}

export default Example;
```

Now our ```Example``` component has a ```state``` of ```color: "red"``` which can be used and changed as necessary in your app.

### Functional Components
Functional components can do similar things to class components, but with different syntax. These components are mainly used to receive props or return JSX. Initially, it was not possible for functional components to have state, but with the introduction of hooks, functional components can take advantage of lifecycle methods and state just like class components.

```
import React, { useState } from 'react';

const Example = () => {
    const [color, setColor] = useState("red");
		
		return <div>Returned HTML</>
}
	

export default Example;
```

This functional component achieves the same result as the class component above. The ```useState``` hook allows our functional component to set state.



