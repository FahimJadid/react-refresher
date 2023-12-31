### React Episode Eight Notes

# React Food Ordering Application :

# Q&A:

- # Q: why we use super(props) in class based component in react?

- Ans:
  In a class-based React component, `super(props)` is used in the constructor to call the constructor of the parent class, which is `React.Component`. Here's why we use `super(props)`:

1. **Inheritance**: In JavaScript, `super` refers to the parent class constructor¹. In the context of a React component, this means `React.Component`. By calling `super(props)`, you're calling the constructor of `React.Component`, effectively initializing the parent class with the `props` parameter⁴.

2. **Accessing `this.props` in the constructor**: If you intend on using `this.props` inside the constructor, you have to call `super(props)`. This ensures `this.props` is set even before the constructor exits¹. If `super(props)` is not called, `this.props` would be `undefined` in the constructor².

3. **Preventing Future Errors**: Even if `this.props` is not used in the constructor, it's recommended to always pass `props` to `super` to avoid inconsistencies and misleading behaviors³. This helps in situations where you might call a method in the constructor and then decide to use `props` in it at some point in the future¹.

Here's an example of how it's used:

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      /* initial state */
    };
  }
  // ...
}
```

In this example, `super(props)` is called to ensure that `this.props` is available in the constructor, and that the parent class (`React.Component`) is properly initialized.

- # Q: What is the use of componentDidMount?

  - Ans: The `componentDidMount()` method is used to fetch data from a server or an API. In the functional components, we use the `useEffect()` hook to fetch data from an API. But in the class-based components, we use the `componentDidMount()` method to fetch data from an API.

- # Q: Why fetch data in the componentDidMount?

  - Ans:
    `Loads => Render => componentDidMount(API call) => Re-render`
    we are familiar with this flow in react. So, when the component is rendered for the first time with basic data the componentDidMount method is called. And we can fetch data from an API in the componentDidMount method. And when the data is fetched from the API then the component will re-render with new fetched data. And the data will be displayed in the component. We do this for fast rendering. Because if we fetch data from an API in the render method then the component will re-render multiple times. And it will slow down the rendering process. And that's why we fetch data from an API in the componentDidMount method.

- # Q: What are differences between componentDidMount vs componentWillUnMount vs componentDidUpdate?

  - Ans:

    - `componentDidMount` is called after the component is mounted and has a DOM representation. This is often a place where you would attach generic DOM events. It is also the only place where you can call `setState` synchronously without causing an extra render. This is because it is called after the initial render, but before the browser updates the screen. Any calls to `setState` in this method will be batched together with the initial render, and therefore will only cause a single re-render.

    - `componentWillUnmount` is called before the component is unmounted and destroyed. This is often a place where you would clean up any DOM events that were attached in `componentDidMount`.

    - `componentDidUpdate` is called after the component is updated and has a DOM representation. This is often a place where you would attach generic DOM events. It is also the only place where you can call `setState` synchronously without causing an extra render. This is because it is called after the initial render, but before the browser updates the screen. Any calls to `setState` in this method will be batched together with the initial render, and therefore will only cause a single re-render.

## 1. Introduction to Class based Components:

- Let's experiment with class based components. Because from the first episode we have been using functional components. But in the industry often we have to work on legacy code and most of them were built with class based components. But when the react team introduced hooks, they said that hooks are the future of react. So, we will be using hooks in this course. But we will also learn class based components. Because we have to work with them in the industry. And for interview purpose we have to know about class based components. So, let's get started.

- Let's start by working on the About component. So, go to the About.js file. And change the functional component to a class based component.
- In the about we want to implement Github API to fetch the data. And We will display that data in our about section.
- To understand class components better we are going to use functional components first in the about section. And then we will convert it to class based component. That way we will understand the difference between functional and class based components.

- To help in this process let's create an User component using functional components. Then we will import this User component in the About component. And we will display the User data in the About component.

- Now make class component called UserClass.js. And copy the code from User.js and paste it in the UserClass.js file. And change the functional component to a class based component.

```js
import React from "react";
class UserClass extends React.Component {
  render() {
    return (
      <div className="user-card">
        <h2>Name: Jadid</h2>
        <h3>Location: Dhaka</h3>
        <h4>Contact: @fahimaljadid</h4>
      </div>
    );
  }
}
```

- Let's explain what is extends and React.component does. So, React is a library. And it has a class called component. And we are extending that component class. So, we are inheriting all the properties of the component class. And render is a method of the component class. So, we are overriding the render method. And we are returning the jsx code. And we are using the UserClass component in the About component.

- Now we are going to see how to send props in class based components. We are sending props from the About component to the UserClass component. Sending props is almost same as functional components. But there is a difference. In functional components we use props as a parameter. But in class based components we use this.props. Let's see how it works. And to receive props in UserClass component we have to use constructor. And we have to pass props as a parameter in the constructor. And we have to call super(props) inside the constructor. And we have to use this.props to receive props. Let's see how it works.

```js
<UserClass name={"Fahim"} location={"Dhaka"} contact={"@myname"} />
      <UserClass name={"Moon"} location={"BD"} contact={"@myname"} />

```

- ```js
  import React from "react";

  class UserClass extends React.Component {
    constructor(props) {
      super(props);
      console.log(props);
    }
    render() {
      return (
        <div className="user-card">
          <h2>Name: {this.props.name}</h2>
          <h3>Location: {this.props.location}</h3>
          <h4>Contact: {this.props.contact}</h4>
        </div>
      );
    }
  }

  export default UserClass;
  ```

- Now we are going to see how to use state in class based components. When we say that we are loading a class based component on our web page that means we are creating an instance of that class. So basically that means we are creating a new instance of that class and giving it some props. And whenever instance is created the constructor is called and this is the best place to receive props and create state variables. So if you want to create a state variable for your class based components you need to create it inside the constructor. And you need to use this.state. And you need to pass an object inside the this.state. And you can create as many state variables as you want. And you can use those state variables inside the render method. And you can also use those state variables inside the jsx code. Let's see how it works.

```js
this.state = {
  count: 0,
};
```

- We created the count state variable. And we are using it inside the render method. Before using the state variables let's just destructure the props to clean the code a little bit. And also destructuring the state variables.

```js
class UserClass extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }
  render() {
    const { name, location } = this.props;
    const { count } = this.state;
    return (
      <div className="user-card">
        <h1>Count: {count}</h1>
        <h2>Name: {name}</h2>
        <h3>Location: {location}</h3>
        <h4>Contact: {contact}</h4>
      </div>
    );
  }
}
```

- Now if we had to create 2 state variables then we would have to write inside the constructor. Because this.state is an object. And we can create as many state variables as we want inside the object. we can use it the same way we used it before. Let's see how it works.

```js
this.state = {
  count: 0,
  age: 20,
};
```

- Now we will ses how to update these state variables. We will create a button and when we click on the button the count state variable will be updated. And we will see how to update the state variables. And we will see how to use the setState method. Let's see how it works.

- "Modifying a state variable directly is not a good practice. We should use the setState method to update the state variables. Let's see how it works."

  ` this.state.count = this.state.count + 1;` // Not a good practice; bad practice

```js
        <h1>Count: {count}</h1>
        <button
          onClick={() => {
            this.setState({ count: this.state.count + 1 });
          }}
        >
          Click
        </button>
```

- So we are using setState method to update the state variables. And we are passing an object inside the setState method and updating the count state variable.

- Let's discuss how our class based component is working behind the scenes. In our app About is our parent component. so whenever About Component is rendered or mounted in to the web page it basically starts rendering the JSX and while rendering whenever it finds the UserClass component it starts to load UserClass component. And goes to the UserClass and it creates an instance of the UserClass component and when the class is instantiated the constructor is called an once the constructor is called then the render is called. first constructor and then render.

- Now it get's slightly complex when we also make the parent component a class based component. So, let's make the About.js a class based component. And let's see how the lifecycle works.

```js
// import User from "./User";
import React from "react";
import UserClass from "./UserClass";

class About extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>About</h1>
        <h2>This is a about section</h2>
        <UserClass name={"Fahim"} location={"Dhaka"} contact={"@myname"} />
      </div>
    );
  }
}

export default About;
```

- Now let's see how constructor and render function is called between these two class based components.
- Lifecycle flow of class based components:

  - 1. About constructor : Parent constructor
  - 2. About render : Parent render
  - 3. UserClass constructor : Child constructor
  - 4. UserClass render : Child render

- It looks easy but let's make it a little bit complex. Let's add another method called componentDidMount in the UserClass component. And Now the flow follows:

  - 1. When the component is loaded the constructor is called first.
  - 2. Then the render method is called.
  - 3. Once this component is mounted into the DOM
  - 4. Then the componentDidMount method is called. This will be called when the component is already mounted in the DOM and we can do some side effects here. Like we can fetch data from an API.
  - 1. Child constructor
  - 2. Child render
  - 3. Child componentDidMount

- But if the componentDidMount also exists in the parent components then what will happen and what will be the lifecycle flow.

  - 1. parent constructor
  - 2. parent render
  - 3. child constructor
  - 4. child render
  - 5. Child component Did mount
  - 6. parent component Did mount

  - You might have a question that why the parent component Did mount is called after the child component Did mount. Because the parent component is already mounted in the DOM. The reason is that the parent component is also a child component of the App component. So, the parent component is also mounted in the DOM. And that's why the parent component Did mount is called after the child component Did mount.

- Let's understand this parent & child relational concept in depth because it's really important for interview purpose. So, we have two class based components, one is the parent: About component and other is the child: UserClass component.
  So when the `parent: About is loaded`, at first the `constructor will be called` then `parent: About render will be called` and when the component is rendering it will render the About component and when it finds the `child: UserClass` component it will start loading the UserClass component. But The mounting of the About component is not finished yet. So, the `parent: About componentDidMount` will not be called yet. That's why it is go to the child: UserClass component and it will trigger child's lifecycle method

  And now the `child: UserClass` component is loaded it will call the `constructor` and then it will call the `render` method. And when the `child: UserClass` component is mounted in the DOM then the `child: UserClass componentDidMount` will be called. And when the `child: UserClass` component is mounted in the DOM and once the children mounting is completed then the `parent: About componentDidMount` will be called. And that's why the `parent: About componentDidMount` is called after the `child: UserClass componentDidMount`.

- Right Now we have only one children component. But what if we have multiple children components. Let's see how it effects the lifecycle. Now we have two instances of the same UserClass.

```js
<UserClass name={"Fahim"} location={"Dhaka"} contact={"@myname"} />
        <UserClass name={"Jadid"} location={"DhK"} contact={"@myname"} />
```

- Now the flow should be;

  - 1. parent constructor
  - 2. parent render
    - 3. child 1 constructor
    - 4. child 1 render
    - 5. child 2 constructor
    - 6. child 2 render
    - 7. Child 1 component Did mount
    - 8. Child 2 component Did mount
  - 9. parent component Did mount

- Let's discuss what just happened!
  ![Alt text](image-4.png)

  React lifecycle Diagram

# In react the component is mounted in two phases.

- `Phase: 1:` Render Phase: When the component is mounting; first of all the constructor is called. Then the render is called. This combination of constructor and render is the render phase. Then react updates the DOM.

- `Phase: 2:` Commit Phase: When the DOM is updated then the componentDidMount is called. And this is the second phase of mounting.

- let's visualize with our application's About and UserClass component for better understanding.
  About component will be mounted:

  - 1. parent constructor(About)
  - 2. parent render(About)
       Starts the lifecycle of first child of UserClass component:
    - 3. first child constructor(UserClass)
    - 4. first child render(UserClass)
         Now because there are two children of UserClass component, so that componentDidMount of the first child will not be called yet. Instead it will batch the render phase for the children of UserClass component. So, it will go to the second child of UserClass component for rendering.
    - 5. second child constructor(UserClass)
    - 6. second child render(UserClass)
         Now the render phase is completed for the children of UserClass component. So, it will batch the commit phase together. And it will call the componentDidMount of the first child & second child of UserClass component.
    - 7. first Child component Did mount(UserClass)
    - 8. second Child component Did mount(UserClass)
  - 9. parent component Did mount(About)

- `So, why we use batching because it's faster. Because the DOM manipulation or updationg is expensive. So, react tries to batch up all children in the render and also the componentDidMount. And that's why it's faster. So react is first of all batching the render phase for both children and then batching the commit phase for both the children.`

# Time for how to make an API call:

- we are using github API to fetch data. And we are going to use the componentDidMount method to fetch data from the API. we are going to use the async await method to fetch data from the API. And we are going to use the setState method to update the state variab

```js

  async componentDidMount() {
    // Api call

    const data = await fetch("https://api.github.com/users/FahimJadid");

    const json = data.json();
    console.log(json);
  }
```

```js
import React from "react";

class UserClass extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInfo: {
        name: "default name",
        location: "default location",
      },
    };
  }

  async componentDidMount() {
    // Api call

    const data = await fetch("https://api.github.com/users/FahimJadid");

    const json = await data.json();

    this.setState({
      userInfo: json,
    });

    console.log(json);
  }

  render() {
    const { name, location, avatar_url } = this.state.userInfo;
    return (
      <div className="user-card">
        <img src={avatar_url} />
        <h2>Name: {name}</h2>
        <h3>Location: {location}</h3>
      </div>
    );
  }
}

export default UserClass;
```

- So the flow for UserClass goes like this:
  `Mounting phase:`
  - 1. constructor
  - 2. renders happend
  - 3. react updated the DOM with dummy data
  - 4. componentDidMount called the API
  - 5. API call finished & setState called
  - 6. setState updates the state variable with new data
  - 7. setState finished & react updated the DOM with new data (Mounting phase is finished)

`Updating phase:`

- 8. (render happens)When the state variable is updated then react triggers render again
- 9. react update the DOM with new data(visible to the user)
- 10. Now componentDidUpdate called

- `Summary:`
  `Mounting phase:`
  - 1. constructor(dummy)
  - 2. render(dummy)
    - <HTML dummy>
  - 3. componentDidMount called - <API call> - <this.setState> => State variable updated
       `Updating phase:`
  - 4. render(API data)
    - <HTML new updated API data>
  - 5. componentDidUpdate called
  - 6. componentWillUnmount called only when we move to another page and the component is unmounted.

```js
import React from "react";

class UserClass extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInfo: {
        name: "default name",
        location: "default location",
      },
    };
  }

  async componentDidMount() {
    // Api call

    const data = await fetch("https://api.github.com/users/FahimJadid");

    const json = await data.json();

    this.setState({
      userInfo: json,
    });

    console.log(json);
  }

  componentDidUpdate() {
    console.log("componentDidUpdate called");
  }

  componentWillUnmount() {
    console.log("componentWillUnmount called");
  }

  render() {
    const { name, location, avatar_url } = this.state.userInfo;
    return (
      <div className="user-card">
        <img src={avatar_url} />
        <h2>Name: {name}</h2>
        <h3>Location: {location}</h3>
      </div>
    );
  }
}

export default UserClass;
```

# Let's talk about clean up:

- When we are using class based components we have to clean up the component. Because if we don't clean up the component then it will cause memory leak. Suppose if we leave the component without cleaning up then the setInterval method will keep running in the background. And it will cause memory leak. Far worse is if we get back to the component again then the setInterval method will run again. And it will cause multiple setInterval method running in the background. And it will cause memory leak. Beacuse our app is not reloading it just changing or switching the components. And that's why we have to clean up the component. And we have to use componentWillUnmount method to clean up the component. Let's see how it works.

```js

componentDidMount() {
  this.timer = setInterval(() => {
    console.log("setInterval called");
  }, 1000);
  }

componentWillUnmount() {
  console.log("componentWillUnmount called");
}
```

- So, we are using setInterval method to call a function every 1 second. And we will use componentWillUnmount method to clean up the setInterval method. And we will use clearInterval method to clean up the setInterval method. Let's see how it works.

```js
componentWillUnmount() {
  clearInterval(this.timer);
  console.log("componentWillUnmount called");
}

```

- Now let's see the same thing in funtional component with UseEffect hook. And we will see how to clean up the component in functional component. And we will see how to use UseEffect hook to clean up the component. Let's see how it works.

```js
useEffect(() => {
  const timer = setInterval(() => {
    console.log("setInterval called");
  }, 1000);

  return () => {
    clearInterval(timer);
    console.log("clean up");
  };
}, []);
```

- So, we are using setInterval method to call a function every 1 second. And we will use return function to clean up the setInterval method. And we will use clearInterval method to clean up the setInterval method.
