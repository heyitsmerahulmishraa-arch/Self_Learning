## What is React? Why is it used?
React is a JavaScript library for building user interfaces, particularly single-page applications where you need a fast and interactive user experience. It was developed by Facebook and is widely used in web development due to its efficiency and flexibility. React allows developers to create reusable UI components, which can manage their own state and be composed to build complex user interfaces. It uses a virtual DOM (Document Object Model) to optimize rendering performance, making it faster than traditional methods of updating the DOM. React is also popular for its unidirectional data flow, which helps in managing the state of applications more predictably. Overall, React is used to create dynamic and responsive web applications with ease.

## What is JSX?
JSX stands for JavaScript XML. It is a syntax extension for JavaScript that allows developers to write HTML-like code within their JavaScript files. JSX makes it easier to create and visualize the structure of the user interface in React applications. Instead of using traditional JavaScript functions to create elements, developers can use JSX to write code that closely resembles HTML, which is more intuitive and easier to read. For example, instead of writing `React.createElement('div', null, 'Hello World')`, you can simply write `<div>Hello World</div>` in JSX. JSX is not a requirement for React, but it is widely used because it enhances the developer experience and makes the code more readable.

## What is a component?
A component in React is a reusable piece of code that represents a part of the user interface. Components can be thought of as building blocks for creating complex UIs. They can be defined as either functional components (using functions) or class components (using ES6 classes). Each component can manage its own state and receive data through props (short for properties). Components can be nested within other components, allowing for a hierarchical structure in the UI. This modular approach promotes code reusability and makes it easier to maintain and update the application. For example, you might have a `Button` component that can be reused across different parts of your application, each time with different props to customize its appearance and behavior.

## What is the difference between functional and class components?
Functional components are simpler and are defined as JavaScript functions that return JSX. They do not have their own state or lifecycle methods, but with the introduction of React Hooks, functional components can now manage state and side effects. Class components, on the other hand, are defined using ES6 classes and can have their own state and lifecycle methods. They require more boilerplate code compared to functional components. With the rise of hooks, functional components have become more popular due to their simplicity and ease of use, while class components are still used in older codebases or when specific features that require classes are needed.
1. Functional Component:
```jsx
function MyComponent(props) {
  return <div>{props.message}</div>;
}
```
2. Class Component:
```jsx
class MyComponent extends React.Component {
  render() {
    return <div>{this.props.message}</div>;
  }
}
```
In summary, functional components are generally preferred for their simplicity and ease of use, especially with the introduction of hooks, while class components are still valid and may be necessary in certain situations.

## What are props?
Props, short for properties, are a way to pass data from a parent component to a child component in React. They are read-only and cannot be modified by the child component. Props allow you to customize the behavior and appearance of a component by providing it with different data. For example, if you have a `Button` component, you can pass a `label` prop to specify the text that should appear on the button:
```jsx
function Button(props) {
  return <button>{props.label}</button>;
}
// Usage
<Button label="Click Me" />
```
In this example, the `Button` component receives the `label` prop and renders it inside the button element. Props can also be used to pass functions, allowing child components to communicate back to their parents or trigger certain actions. Overall, props are essential for creating dynamic and reusable components in React.

## What is state in React?
State in React is a built-in object that allows components to manage and track changes in data over time. Unlike props, which are passed from parent to child components and are read-only, state is mutable and can be updated by the component itself. State is typically used to store information that can change in response to user actions or other events, such as form inputs, toggles, or fetched data. When the state of a component changes, React automatically re-renders the component to reflect the new state in the user interface. State can be defined in class components using `this.state` and updated with `this.setState()`, while in functional components, it can be managed using the `useState` hook. Overall, state is crucial for creating interactive and dynamic applications in React.
```jsx
// Example of state in a class component
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}


// Example of state in a functional component using hooks
function Counter() {
  const [count, setCount] = React.useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```
In both examples, the `Counter` component maintains a `count` state that can be incremented when the button is clicked. The component re-renders to display the updated count value whenever the state changes.

## What is the use of useState hook?
The `useState` hook is a function in React that allows functional components to manage state. It provides a way to declare state variables and update them within a functional component. The `useState` hook takes an initial state value as an argument and returns an array containing the current state and a function to update that state. This allows developers to create interactive components that can respond to user input or other events by updating the state and re-rendering the component accordingly. The `useState` hook is essential for managing state in functional components, which do not have access to the traditional `this.state` and `this.setState()` methods used in class components.
```jsx
import React, { useState } from 'react';
function Counter() {
  const [count, setCount] = useState(0); // Declare a state variable 'count' with an initial value of 0

  const increment = () => {
    setCount(count + 1); // Update the state variable 'count' by incrementing its value
  };

  return (
    <div>
      <p>Count: {count}</p> {/* Display the current value of 'count' */}
      <button onClick={increment}>Increment</button> {/* Button to trigger the increment function */}
    </div>
  );
}
```
In this example, the `useState` hook is used to create a state variable called `count` with an initial value of `0`. The `setCount` function is used to update the value of `count` whenever the "Increment" button is clicked. When the state changes, the component re-renders to display the updated count value.

## What is useEffect used for?
The `useEffect` hook in React is used to perform side effects in functional components. Side effects can include tasks such as fetching data from an API, subscribing to events, or manually manipulating the DOM. The `useEffect` hook allows you to run a function after the component has rendered, and it can also be configured to run only when certain dependencies change. This makes it a powerful tool for managing lifecycle events in functional components, similar to the lifecycle methods in class components (like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`). By using `useEffect`, you can ensure that your component behaves correctly in response to changes in state or props, and you can also clean up any resources when the component unmounts.
```jsx
import React, { useState, useEffect } from 'react';
function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    // This function will run after the component mounts
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data))
      .catch(error => console.error('Error fetching data:', error));
    
    // Optional cleanup function
    return () => {
      console.log('Component unmounted, cleanup if necessary');
    };
  }, []); // Empty dependency array means this effect runs only once after the initial render

  return (
    <div>
      {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : 'Loading...'}
    </div>
  );
}
```
In this example, the `useEffect` hook is used to fetch data from an API when the component mounts. The empty dependency array `[]` ensures that the effect runs only once, similar to `componentDidMount` in class components. The fetched data is stored in the state variable `data`, and if there is an error during fetching, it is logged to the console. Additionally, a cleanup function is provided to handle any necessary cleanup when the component unmounts.

## What is conditional rendering?
Conditional rendering in React refers to the ability to render different components or elements based on certain conditions. This is typically achieved using JavaScript's conditional statements (like `if`, `else`, or ternary operators) within the JSX code. Conditional rendering allows developers to create dynamic user interfaces that can change based on user interactions, application state, or other factors. For example, you might want to display a loading spinner while data is being fetched, and then show the actual content once the data is available. By using conditional rendering, you can control what gets displayed to the user and create a more interactive and responsive application.
```jsx
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}
function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}
```
In this example, the `Greeting` component uses conditional rendering to display either a `UserGreeting` or a `GuestGreeting` based on the value of the `isLoggedIn` prop. If `isLoggedIn` is true, it renders the `UserGreeting`; otherwise, it renders the `GuestGreeting`. This allows the UI to adapt based on the user's login status.

## What is the difference between controlled and uncontrolled components?
Controlled components are form elements (like input, textarea, select) that are controlled by React state. In a controlled component, the value of the form element is set by the state of the component, and any changes to the form element are handled through event handlers that update the state. This allows for more predictable behavior and easier management of form data. For example:
```jsx
function ControlledInput() {
  const [value, setValue] = useState('');
  return (
    <input
      type="text"
      value={value}
      onChange={(e) => setValue(e.target.value)}
    />
  );
}
```
In this example, the `ControlledInput` component is a controlled component because the value of the input is determined by the `value` state, and any changes to the input are handled by the `onChange` event handler that updates the state.

Uncontrolled components, on the other hand, are form elements that manage their own state internally. In an uncontrolled component, you can use a ref to access the form element's value directly from the DOM when needed. This approach is less common in React and is generally not recommended for complex forms, as it can lead to less predictable behavior. For example:
```jsx
function UncontrolledInput() {
  const inputRef = useRef(null);
  const handleSubmit = () => {
    alert(`Input value: ${inputRef.current.value}`);
  };
  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}
```
In this example, the `UncontrolledInput` component is an uncontrolled component because the value of the input is not managed by React state. Instead, a ref is used to access the input's value directly from the DOM when the submit button is clicked. This can make it more difficult to manage and validate form data compared to controlled components.

## What is Virtual DOM?
The Virtual DOM is a concept in React that refers to an in-memory representation of the actual DOM (Document Object Model). It is a lightweight copy of the real DOM that React uses to optimize rendering performance. When a component's state or props change, React updates the Virtual DOM first, rather than directly manipulating the real DOM. React then compares the updated Virtual DOM with the previous version using a process called "diffing" to determine what has changed. Based on this comparison, React calculates the most efficient way to update the real DOM, minimizing the number of changes and improving performance. This approach allows React to create fast and responsive user interfaces, as it reduces the overhead associated with direct DOM manipulation.
```jsx
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```
In this example, when the "Increment" button is clicked, the `count` state is updated. React updates the Virtual DOM first, compares it with the previous version, and then efficiently updates the real DOM to reflect the new count value. This process ensures that the application remains fast and responsive even as the UI changes frequently.

## What is reconciliation in React?
Reconciliation in React is the process by which React updates the DOM to match the Virtual DOM. When a component's state or props change, React creates a new Virtual DOM tree and compares it with the previous Virtual DOM tree using a diffing algorithm. This algorithm identifies what has changed between the two trees, such as which components have been added, removed, or updated. Based on this comparison, React determines the most efficient way to update the real DOM to reflect the changes. Reconciliation helps optimize performance by minimizing unnecessary updates to the DOM, ensuring that only the components that have actually changed are re-rendered. This process is crucial for maintaining a fast and responsive user interface in React applications.
```jsx
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```
In this example, when the "Increment" button is clicked, the `count` state is updated. React creates a new Virtual DOM tree with the updated count value and compares it to the previous Virtual DOM tree. The reconciliation process identifies that only the text content of the `<p>` element has changed, so React efficiently updates only that part of the real DOM, rather than re-rendering the entire component. This ensures that the application remains fast and responsive even as the UI changes frequently.

## What is React Fragment?
React Fragment is a component that allows you to group a list of children without adding extra nodes to the DOM. It is useful when you want to return multiple elements from a component without wrapping them in a parent element like a `<div>`. This helps to keep the DOM clean and avoids unnecessary nesting, which can improve performance and make the code more readable. You can use React Fragment by either using the `<React.Fragment>` syntax or the shorthand `<>` syntax.
```jsx
function MyComponent() {
  return (
    <React.Fragment>
      <h1>Title</h1>
      <p>This is a paragraph.</p>
    </React.Fragment>
  );
}
```
or using the shorthand syntax:
```jsx
function MyComponent() {
  return (
    <>
      <h1>Title</h1>
      <p>This is a paragraph.</p>
    </>
  );
}
```
In both examples, the `MyComponent` returns multiple elements (a heading and a paragraph) without adding an extra wrapper element to the DOM. This allows for a cleaner and more efficient structure in the rendered output. React Fragments are particularly useful when you want to return multiple elements from a component without affecting the layout or styling of the page.

## What is lifting state up?
Lifting state up is a common pattern in React where you move the state from a child component to a common parent component. This is done when multiple components need to share and manage the same state. By lifting the state up to the nearest common ancestor, you can ensure that all child components that need access to that state can receive it through props. This approach promotes better organization and makes it easier to manage shared state across components. For example, if you have two sibling components that need to access the same data, you would lift the state up to their parent component and pass it down as props to both siblings.
```jsx
function ParentComponent() {
  const [sharedState, setSharedState] = useState('Hello');

  return (
    <div>
      <ChildComponent1 sharedState={sharedState} />
      <ChildComponent2 sharedState={sharedState} />
    </div>
  );
}
function ChildComponent1(props) {
  return <p>Child 1: {props.sharedState}</p>;
}
function ChildComponent2(props) {
  return <p>Child 2: {props.sharedState}</p>;
}
```
In this example, the `sharedState` is lifted up to the `ParentComponent`, which manages the state and passes it down to both `ChildComponent1` and `ChildComponent2` through props. This allows both child components to access and display the same state without having to manage it individually, promoting better code organization and state management in the application.

## What is prop drilling?
Prop drilling is a term used in React to describe the process of passing data from a parent component down to child components through multiple levels of the component tree. This can become cumbersome and inefficient when you have deeply nested components, as you may need to pass props through several layers of components that do not actually need the data, just to get it to the component that does. Prop drilling can lead to code that is difficult to maintain and understand, as it scatters the data across many components and makes it less clear where the data is coming from. To avoid prop drilling, developers often use state management libraries like Redux or Context API, which allow for more efficient and centralized state management without having to pass props through multiple levels of the component tree.
```jsx
function ParentComponent() {
  const [data, setData] = useState('Hello');

  return (
    <div>
      <ChildComponent1 data={data} />
    </div>
  );
}
function ChildComponent1(props) {
  return <p>Child 1: {props.data}</p>;
}
```
In this example, the `data` is passed from the `ParentComponent` to `ChildComponent1`. If there were more nested components between them, you would have to pass the `data` through each of those components, even if they do not need it, which is an example of prop drilling. This can make the code more complex and harder to maintain as the component tree grows.

## What is React Context API?
The React Context API is a feature in React that allows for the sharing of state and data across components without having to pass props down through every level of the component tree (prop drilling). It provides a way to create global variables that can be accessed by any component in the application, regardless of their position in the component hierarchy. The Context API consists of three main components: `React.createContext()`, which creates a context object; `Provider`, which is used to wrap the part of the component tree that needs access to the context; and `Consumer`, which is used to access the context values in child components. The Context API is particularly useful for managing global state, such as user authentication status or theme settings, and helps to simplify code by reducing the need for prop drilling.
```jsx
const MyContext = React.createContext();
function ParentComponent() {
  const [value, setValue] = useState('Hello');

  return (
    <MyContext.Provider value={value}>
      <ChildComponent />
    </MyContext.Provider>
  );
}
function ChildComponent() {
  return (
    <MyContext.Consumer>
      {value => <p>Value from context: {value}</p>}
    </MyContext.Consumer>
  );
}
```
In this example, the `MyContext` is created using `React.createContext()`. The `ParentComponent` uses the `Provider` to pass the `value` down to any child components that need it. The `ChildComponent` uses the `Consumer` to access the context value and display it. This allows for efficient state management without having to pass props through multiple levels of the component tree, avoiding prop drilling and making the code cleaner and easier to maintain.

## What is React Router?
React Router is a popular library in the React ecosystem that enables developers to implement client-side routing in their applications. It allows you to create single-page applications (SPAs) with multiple views and navigation without requiring a full page reload. React Router provides components such as `BrowserRouter`, `Route`, `Link`, and `Switch` to manage routing and navigation within a React application. With React Router, you can define routes for different components, handle dynamic URL parameters, and create nested routes, making it easier to build complex and interactive web applications with seamless navigation.
```jsx
import { BrowserRouter as Router, Route, Link, Switch } from 'react-router-dom';
function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </Router>
  );
}
function Home() {
  return <h1>Home Page</h1>;
}
function About() {
  return <h1>About Page</h1>;
}
```
In this example, the `App` component uses `BrowserRouter` to enable routing. The `Link` components are used to create navigation links to the "Home" and "About" pages. The `Switch` component is used to render the appropriate component based on the current URL path. When the user clicks on the "Home" link, the `Home` component is rendered, and when they click on the "About" link, the `About` component is rendered. This allows for a seamless navigation experience in a single-page application without requiring full page reloads.

## What is lazy loading in React?
Lazy loading in React is a technique that allows you to load components or resources only when they are needed, rather than loading everything upfront. This can improve the performance of your application by reducing the initial load time and optimizing resource usage. React provides a built-in function called `React.lazy()` that enables lazy loading of components. When a component is wrapped with `React.lazy()`, it will only be loaded when it is rendered for the first time. This is often used in conjunction with `Suspense` to provide a fallback UI while the lazy-loaded component is being fetched.
```jsx
import React, { Suspense } from 'react';
const LazyComponent = React.lazy(() => import('./LazyComponent'));
function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```
In this example, the `LazyComponent` is loaded lazily using `React.lazy()`. The `Suspense` component is used to wrap the lazy-loaded component and provides a fallback UI (in this case, a simple "Loading..." message) while the component is being fetched. This approach helps to improve the performance of the application by only loading components when they are actually needed, rather than loading everything at once.

## What is memoization in React?
Memoization in React is a performance optimization technique that allows you to cache the results of expensive function calls and return the cached result when the same inputs occur again. This can help to avoid unnecessary re-renders and improve the performance of your application. React provides a built-in function called `React.memo()` that can be used to memoize functional components. When a component is wrapped with `React.memo()`, it will only re-render if its props have changed, otherwise it will return the cached result from the previous render.
```jsx
const MyComponent = React.memo(function MyComponent(props) {
  // This component will only re-render if props change
  return <div>{props.value}</div>;
});
```
In this example, the `MyComponent` is wrapped with `React.memo()`, which means that it will only re-render if the `props.value` changes. If the parent component re-renders but the `props.value` remains the same, `MyComponent` will return the cached result from the previous render, improving performance by avoiding unnecessary re-renders. Memoization is particularly useful for components that receive complex props or perform expensive calculations, as it can help to optimize rendering and enhance the user experience.

## What is useMemo and useCallback?
The `useMemo` and `useCallback` hooks in React are used for performance optimization by memoizing values and functions, respectively.
- `useMemo` is used to memoize the result of a function that returns a value. It takes a function and a dependency array as arguments, and it will only recompute the memoized value when one of the dependencies has changed. This can help to avoid expensive calculations on every render.
```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
- `useCallback` is used to memoize a function itself. It takes a function and a dependency array as arguments, and it will return a memoized version of the function that only changes if one of the dependencies has changed. This is useful for preventing unnecessary re-renders of child components that depend on the function.
```jsx
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```
In summary, `useMemo` is used to memoize the result of a function, while `useCallback` is used to memoize the function itself. Both hooks help to optimize performance by preventing unnecessary calculations and re-renders in React applications.

## What is React Fiber?
React Fiber is a reimplementation of the React core algorithm that was introduced in React 16. It is designed to improve the performance and responsiveness of React applications by breaking down the rendering work into smaller units of work, called "fibers". This allows React to prioritize and manage updates more efficiently, enabling features like time-slicing and concurrent rendering. With React Fiber, React can pause and resume work as needed, which helps to keep the user interface responsive even during complex updates. Overall, React Fiber is a significant improvement to the React architecture that enhances the performance and user experience of React applications.


## What is concurrent rendering?
Concurrent rendering is a feature in React that allows the rendering process to be interrupted and resumed, enabling React to work on multiple tasks simultaneously. This means that React can prioritize certain updates over others, allowing for a more responsive user interface. With concurrent rendering, React can pause the rendering of a component if it detects that the user is interacting with the application, and then resume it once the interaction is complete. This helps to prevent the UI from becoming unresponsive during heavy computations or when rendering large components. Concurrent rendering is part of the React Fiber architecture and is designed to improve the performance and user experience of React applications.
```jsx
function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```
In this example, when the "Increment" button is clicked, the `count` state is updated. With concurrent rendering, React can prioritize this update and ensure that the UI remains responsive even if there are other ongoing tasks or updates in the application. This allows for a smoother user experience, as the application can handle multiple updates without becoming unresponsive.

## What is hydration in React?
Hydration in React refers to the process of attaching event listeners and making a server-rendered React application interactive on the client side. When a React application is rendered on the server, it generates HTML that can be sent to the client's browser. However, this HTML is static and does not have any interactivity. Hydration is the step where React takes this server-rendered HTML and "hydrates" it by attaching the necessary event listeners and making it fully functional as a React application on the client side. This allows for faster initial load times since the HTML is already rendered, while still providing a seamless user experience with interactivity once the hydration process is complete.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
ReactDOM.hydrate(<App />, document.getElementById('root'));
```
In this example, the `ReactDOM.hydrate()` method is used to hydrate the server-rendered React application. The `App` component is rendered on the server and sent as HTML to the client's browser. When the client receives this HTML, the `hydrate` method attaches event listeners and makes the application interactive without re-rendering the entire component tree. This allows for a faster initial load time while still providing a responsive user experience. Hydration is an essential part of server-side rendering (SSR) in React applications, enabling them to be both fast and interactive.

## What is server-side rendering (SSR)?
Server-side rendering (SSR) is a technique in React where the initial rendering of a React application is done on the server rather than in the client's browser. This means that when a user requests a page, the server generates the HTML for that page and sends it to the client, allowing for faster initial load times and improved SEO (Search Engine Optimization). SSR can be particularly beneficial for applications that require fast loading times or need to be indexed by search engines, as it allows the content to be rendered and available to users and search engines immediately, without waiting for JavaScript to load and execute on the client side. However, SSR can also add complexity to the development process and may require additional configuration and setup compared to client-side rendering.
```jsx
import React from 'react';
import ReactDOMServer from 'react-dom/server';
import App from './App';
const html = ReactDOMServer.renderToString(<App />);
console.log(html);
```
In this example, the `ReactDOMServer.renderToString()` method is used to render the `App` component to a string of HTML on the server. This HTML can then be sent to the client's browser, allowing for faster initial load times and improved SEO. The client can then use hydration to make the application interactive once it receives the server-rendered HTML. Server-side rendering is a powerful technique for improving performance and SEO in React applications, but it requires additional setup and configuration compared to client-side rendering.

## What is static site generation (SSG)?
Static site generation (SSG) is a technique in React where the HTML for a website is generated at build time rather than on the server or client side. This means that when you build your React application, it generates static HTML files for each page, which can be served directly to users without the need for server-side rendering or client-side rendering. SSG can improve performance and SEO, as the static HTML files can be served quickly and are easily indexed by search engines. It is particularly useful for content-heavy websites or blogs where the content does not change frequently. Popular frameworks like Next.js and Gatsby provide built-in support for static site generation in React applications.
```jsx
import React from 'react';
import { renderToStaticMarkup } from 'react-dom/server';
function App() {
  return <h1>Hello, World!</h1>;
}
const html = renderToStaticMarkup(<App />);
console.log(html);
```
In this example, the `renderToStaticMarkup` method from `react-dom/server` is used to generate a static HTML string for the `App` component. This HTML can be saved as a static file and served directly to users. Static site generation is an effective way to improve performance and SEO for websites that do not require dynamic content, as it allows for fast loading times and easy indexing by search engines.

## What is code splitting?
Code splitting is a technique in React that allows you to split your application into smaller chunks of code that can be loaded on demand. This can improve the performance of your application by reducing the initial load time, as only the necessary code for the current view is loaded, rather than the entire application. React provides a built-in function called `React.lazy()` that enables code splitting for components. When a component is wrapped with `React.lazy()`, it will only be loaded when it is rendered for the first time. This is often used in conjunction with `Suspense` to provide a fallback UI while the lazy-loaded component is being fetched.
```jsx
import React, { Suspense } from 'react';
const LazyComponent = React.lazy(() => import('./LazyComponent'));
function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```
In this example, the `LazyComponent` is loaded lazily using `React.lazy()`. The `Suspense` component is used to wrap the lazy-loaded component and provides a fallback UI (in this case, a simple "Loading..." message) while the component is being fetched. Code splitting helps to improve the performance of the application by only loading components when they are actually needed, rather than loading everything at once. This can lead to faster initial load times and a better user experience, especially for larger applications with many components.

## What are error boundaries?
Error boundaries are a feature in React that allows you to catch JavaScript errors anywhere in the component tree and display a fallback UI instead of crashing the entire application. An error boundary is a React component that implements either the `componentDidCatch` lifecycle method (for class components) or the `getDerivedStateFromError` static method (for functional components). When an error is thrown in a child component, the error boundary will catch it and can render a fallback UI, log the error, or perform any other necessary actions. This helps to improve the user experience by preventing the entire application from crashing due to an error in a specific component.
```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    console.error('Error caught by ErrorBoundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children; 
  }
}
```
In this example, the `ErrorBoundary` component is a class component that implements the `getDerivedStateFromError` method to update its state when an error is caught. The `componentDidCatch` method is used to log the error details. If an error occurs in any child component wrapped by `ErrorBoundary`, it will display a fallback UI with the message "Something went wrong." This allows the application to continue functioning even if a specific component encounters an error, improving the overall user experience.

## What is React Suspense?
React Suspense is a feature in React that allows you to handle asynchronous operations, such as data fetching or code splitting, in a more declarative way. It provides a way to specify a fallback UI that will be displayed while the asynchronous operation is in progress. When the operation is complete, the actual content will be rendered. This helps to improve the user experience by providing feedback during loading states and allowing for smoother transitions between different states of the application. React Suspense can be used in conjunction with features like `React.lazy()` for code splitting or with libraries like `react-query` for data fetching.
```jsx
import React, { Suspense } from 'react';
const LazyComponent = React.lazy(() => import('./LazyComponent'));
function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```
In this example, the `LazyComponent` is loaded lazily using `React.lazy()`. The `Suspense` component is used to wrap the lazy-loaded component and provides a fallback UI (in this case, a simple "Loading..." message) while the component is being fetched. React Suspense allows for a more declarative way to handle asynchronous operations, improving the user experience by providing feedback during loading states and enabling smoother transitions between different states of the application.

## What is forwardRef?
`forwardRef` is a function in React that allows you to pass a ref through a component to one of its child components. This is useful when you want to access the DOM element of a child component from a parent component. By using `forwardRef`, you can create a component that can accept a ref and forward it to the appropriate child component, enabling you to interact with the DOM element directly. This is particularly helpful when working with third-party libraries or when you need to manage focus, measure the size of an element, or perform other operations that require direct access to the DOM.
```jsx
import React, { forwardRef } from 'react';
const MyInput = forwardRef((props, ref) => (
  <input ref={ref} {...props} />
));
function ParentComponent() {
  const inputRef = React.createRef();

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <MyInput ref={inputRef} />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```
In this example, the `MyInput` component is created using `forwardRef`, which allows it to accept a ref and forward it to the underlying `<input>` element. The `ParentComponent` creates a ref called `inputRef` and passes it to the `MyInput` component. When the "Focus Input" button is clicked, the `focusInput` function is called, which uses the ref to focus the input element. This demonstrates how `forwardRef` enables you to access and interact with child components' DOM elements from a parent component.

## What is portal in React?
A portal in React is a way to render a component's children into a DOM node that exists outside the hierarchy of the parent component. This is useful for situations where you want to render content that should visually appear above other elements, such as modals, tooltips, or dropdowns. React provides the `createPortal` function from the `react-dom` package to create portals. When you use `createPortal`, you can specify the content to be rendered and the target DOM node where it should be rendered. This allows you to maintain the logical structure of your components while still rendering them in a different part of the DOM.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
function Modal({ children }) {
  return ReactDOM.createPortal(
    <div className="modal">
      {children}
    </div>,
    document.getElementById('modal-root')
  );
}
function App() {
  return (
    <div>
      <h1>Main Application</h1>
      <Modal>
        <p>This is a modal!</p>
      </Modal>
    </div>
  );
}
```
In this example, the `Modal` component uses `ReactDOM.createPortal` to render its children into a DOM node with the ID of `modal-root`, which is outside the hierarchy of the `App` component. This allows the modal content to visually appear above other elements in the application, while still maintaining a logical structure in the component tree. Portals are particularly useful for creating UI elements that need to break out of their parent container, such as modals, tooltips, or dropdowns, without affecting the overall structure of the application.

## What is Strict Mode in React?
Strict Mode is a feature in React that helps developers identify potential problems in their applications. It is a tool for highlighting issues such as deprecated APIs, unsafe lifecycle methods, and other potential bugs in the code. When you wrap your components in `<React.StrictMode>`, React will run additional checks and warnings during development to help you catch these issues early on. Strict Mode does not affect the production build of your application, and it does not render any visible UI. It is purely a development tool to help improve the quality of your code and ensure that you are following best practices.
```jsx
import React from 'react';
function App() {
  return (
    <React.StrictMode>
      <MyComponent />
    </React.StrictMode>
  );
}
```

## What is controlled vs uncontrolled form handling?
In React, controlled and uncontrolled form handling refer to two different approaches for managing form inputs and their state.
Controlled components are form elements that are controlled by React state. In a controlled component, the value of the form element is determined by the state, and any changes to the form element are handled through event handlers that update the state. This allows for more predictable behavior and easier management of form data. For example:
```jsx
function ControlledInput() {
  const [value, setValue] = useState('');
  return (
    <input
      type="text"
      value={value}
      onChange={(e) => setValue(e.target.value)}
    />
    );
}
```
In this example, the `ControlledInput` component is a controlled component because the value of the input is determined by the `value` state, and any changes to the input are handled through the `onChange` event handler that updates the state.
Uncontrolled components, on the other hand, are form elements that manage their own state internally. In an uncontrolled component, you can access the form element's value directly from the DOM when needed, rather than relying on React state to manage it. This approach is less common in React and is generally not recommended for complex forms, as it can lead to less predictable behavior. For example:
```jsx
function UncontrolledInput() {
  const inputRef = useRef(null);
  const handleSubmit = () => {
    alert(inputRef.current.value);
  };
  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}
```
In this example, the `UncontrolledInput` component is an uncontrolled component because the value of the input is not managed by React state. Instead, it uses a ref to access the input's value directly from the DOM when the submit button is clicked. This can make it more difficult to manage and validate form data compared to controlled components, as you have to rely on direct DOM manipulation rather than React's state management.

## What is React batching?
React batching is a performance optimization technique that allows React to group multiple state updates together and apply them in a single render pass. This means that when multiple state updates occur within the same event loop, React will batch them together and only re-render the component once, rather than re-rendering for each individual update. This can significantly improve the performance of your application by reducing the number of renders and minimizing the amount of work React has to do. Batching is especially beneficial when you have multiple state updates that are triggered by user interactions or asynchronous events, as it helps to ensure that your application remains responsive and efficient.
```jsx
function App() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState('');

  const handleClick = () => {
    setCount(count + 1);
    setText('Button clicked!');
  };

  return (
    <div>
      <p>Count: {count}</p>
      <p>{text}</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}
```
In this example, when the "Click Me" button is clicked, both the `count` and `text` state updates are triggered. React will batch these updates together and only re-render the component once, rather than re-rendering for each individual update. This helps to improve the performance of the application by reducing the number of renders and ensuring that the UI remains responsive even when multiple state updates occur in quick succession.

## What is custom hook? Why do we use it?
A custom hook in React is a reusable function that allows you to extract and share logic between components. Custom hooks are created by defining a function that uses built-in React hooks (like `useState`, `useEffect`, etc.) to encapsulate specific functionality. The main reason for using custom hooks is to promote code reusability and separation of concerns. By creating custom hooks, you can keep your components clean and focused on rendering UI, while the custom hook handles the logic and state management. This makes it easier to maintain and test your code, as well as to share common functionality across different components without duplicating code.
```jsx
import { useState, useEffect } from 'react';
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((response) => response.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      })
      .catch((error) => {
        setError(error);
        setLoading(false);
      });
  }, [url]);

  return { data, loading, error };
}
```
In this example, the `useFetch` custom hook encapsulates the logic for fetching data from a given URL. It manages the state for the fetched data, loading status, and any errors that may occur during the fetch operation. By using this custom hook, you can easily reuse the data fetching logic across multiple components without having to duplicate code, making your application more maintainable and organized. Custom hooks are a powerful way to abstract away complex logic and promote code reuse in React applications.

## What is useLayoutEffect?
`useLayoutEffect` is a React hook that is similar to `useEffect`, but it runs synchronously after all DOM mutations. This means that `useLayoutEffect` is executed immediately after the DOM has been updated, but before the browser has had a chance to paint the changes on the screen. This makes it useful for performing operations that need to happen before the browser paints, such as measuring the layout of elements or making adjustments to the DOM based on the new layout. However, because `useLayoutEffect` runs synchronously, it can block the browser from painting and may lead to performance issues if used excessively. Therefore, it should be used with caution and only when necessary for tasks that require immediate access to the DOM after updates.
```jsx
import { useLayoutEffect, useRef } from 'react';
function MyComponent() {
  const divRef = useRef(null);

  useLayoutEffect(() => {
    const div = divRef.current;
    if (div) {
      // Measure the layout of the div and make adjustments if necessary
      const { width, height } = div.getBoundingClientRect();
      console.log(`Div dimensions: ${width}x${height}`);
    }
  });

  return <div ref={divRef}>Hello, World!</div>;
}
```
In this example, the `useLayoutEffect` hook is used to measure the dimensions of a `div` element immediately after it has been rendered and the DOM has been updated. The `divRef` is created using `useRef` to access the DOM element, and the `getBoundingClientRect()` method is used to retrieve the width and height of the `div`. This allows you to perform any necessary adjustments or calculations based on the layout of the element before the browser paints it on the screen. However, it's important to use `useLayoutEffect` judiciously, as it can lead to performance issues if overused or if it contains heavy computations.

## What is React DevTools?
React DevTools is a browser extension that provides a set of tools for inspecting and debugging React applications. It allows developers to view the component hierarchy, inspect props and state, and analyze the performance of their React applications. With React DevTools, you can easily identify issues in your components, understand how data flows through your application, and optimize performance by analyzing component re-renders. The DevTools also provide features like highlighting updates, showing component render times, and allowing you to edit props and state directly from the browser. Overall, React DevTools is an essential tool for any React developer looking to improve their development workflow and debug their applications effectively.
```jsx
// To use React DevTools, you can install the extension for your browser (available for Chrome and Firefox) and then open the DevTools panel. You will see a new "React" tab where you can inspect your React components, view their props and state, and analyze their performance. You can also use the DevTools to debug issues in your application by setting breakpoints, inspecting component updates, and monitoring the component tree. React DevTools is a powerful tool that can help you understand and optimize your React applications more effectively.
```

## What is key prop and why is it important?
The `key` prop in React is a special attribute that is used to identify elements in a list or collection of components. It is important because it helps React efficiently update and manage the rendering of components when the data changes. When you render a list of components, React uses the `key` prop to determine which items have changed, been added, or been removed. This allows React to optimize the rendering process by only re-rendering the components that have actually changed, rather than re-rendering the entire list. The `key` prop should be a unique identifier for each item in the list, such as an ID or a unique string, to ensure that React can correctly track and manage the components.
```jsx
function ItemList({ items }) {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```
In this example, the `ItemList` component renders a list of items, and each item is given a `key` prop that is set to the unique `id` of the item. This allows React to efficiently update the list when items are added, removed, or changed, as it can use the `key` to identify which components need to be re-rendered. Using a unique `key` is crucial for maintaining performance and ensuring that your React application behaves correctly when rendering lists of components.

## What is React performance profiling?
React performance profiling is the process of analyzing and measuring the performance of a React application to identify bottlenecks and optimize rendering. This can be done using tools like the React DevTools Profiler, which allows you to record and analyze the rendering behavior of your components. The profiler provides insights into how long each component takes to render, how many times it re-renders, and what caused the re-render (such as changes in props or state). By using performance profiling, developers can identify components that are rendering unnecessarily or taking a long time to render, and then optimize those components to improve the overall performance of the application. This can lead to faster load times, smoother interactions, and a better user experience.
```jsx
// To use React performance profiling, you can open the React DevTools in your browser and navigate to the "Profiler" tab. From there, you can start recording a profiling session while interacting with your application. The profiler will capture the rendering behavior of your components and provide a visual representation of the time taken for each component to render, as well as the reasons for re-renders. You can analyze this data to identify performance issues and optimize your components accordingly.
```

## What is Higher Order Component (HOC)?
A Higher Order Component (HOC) in React is a function that takes a component and returns a new component with enhanced functionality. HOCs are used to reuse component logic across multiple components without modifying the original component. They allow you to abstract away common patterns and behaviors, such as authentication, data fetching, or logging, and apply them to different components in a consistent way. An HOC typically wraps the original component and provides additional props or functionality to it. This pattern promotes code reusability and separation of concerns, making it easier to maintain and scale your React applications.
```jsx
function withLogging(WrappedComponent) {
  return function WithLogging(props) {
    useEffect(() => {
      console.log('Component mounted');
      return () => {
        console.log('Component unmounted');
      };
    }, []);
    return <WrappedComponent {...props} />;
  };
}
```
In this example, the `withLogging` function is a Higher Order Component that takes a `WrappedComponent` as an argument and returns a new component called `WithLogging`. The `WithLogging` component uses the `useEffect` hook to log messages when the component mounts and unmounts. By wrapping any component with `withLogging`, you can easily add logging functionality without modifying the original component's code. This demonstrates how HOCs can be used to enhance components with additional behavior in a reusable way.

## What is React testing (Jest + RTL basics)?
React testing involves using tools like Jest and React Testing Library (RTL) to write tests for React components and applications. Jest is a JavaScript testing framework that provides a simple and powerful way to write unit tests, while React Testing Library focuses on testing the behavior of React components from the user's perspective. With Jest, you can create test suites and assertions to verify that your code behaves as expected. React Testing Library allows you to render components in a test environment and interact with them using queries that mimic how users would interact with the application. This combination of tools helps ensure that your React components are functioning correctly and provides confidence in the stability of your application as it evolves.
`Example of a simple React component test using Jest and React Testing Library:`
```javascript
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import '@testing-library/jest-dom/extend-expect';
import MyButton from './MyButton'; // Assume this is a simple button component
test('renders MyButton and handles click event', () => {
  render(<MyButton />);
  const buttonElement = screen.getByRole('button');
  expect(buttonElement).toBeInTheDocument();
  fireEvent.click(buttonElement);
  expect(screen.getByText('Button clicked!')).toBeInTheDocument();
});
```
In this example, we import the necessary modules from React Testing Library and Jest. We render the `MyButton` component and use `screen.getByRole` to find the button element. We then assert that the button is present in the document. Next, we simulate a click event on the button using `fireEvent.click` and assert that a message indicating the button was clicked is displayed in the document. This test verifies that the `MyButton` component renders correctly and responds to user interactions as expected.

## What is reconciliation algorithm in depth?
The reconciliation algorithm is a key concept in React, a popular JavaScript library for building user interfaces. It is the process by which React updates the DOM to reflect changes in the component's state or props. When a component's state or props change, React creates a new virtual DOM tree and compares it to the previous virtual DOM tree. This comparison is done using a diffing algorithm that identifies what has changed between the two trees. Based on this comparison, React determines the minimum number of changes needed to update the actual DOM efficiently. The reconciliation algorithm helps optimize performance by minimizing unnecessary updates and ensuring that only the parts of the DOM that have changed are re-rendered. Understanding how the reconciliation algorithm works can help developers write more efficient React applications and improve their performance.
For example, if you have a list of items rendered in a React component and you add a new item to the list, the reconciliation algorithm will compare the new virtual DOM tree with the previous one. It will identify that a new item has been added and will only update the DOM to include that new item, rather than re-rendering the entire list. This efficient updating process is what makes React applications performant and responsive, even as they grow in complexity.

## What is render props pattern?
The render props pattern is a technique in React for sharing code between components using a prop that is a function. This function, often called a "render prop," allows you to pass a function as a prop to a component, which can then call that function to render content. The render props pattern is useful for creating reusable components that can share logic and state without relying on higher-order components or other patterns. It allows for greater flexibility and composability in your React applications.
```jsx
function DataFetcher({ url, render }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((response) => response.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      })
      .catch((error) => {
        setError(error);
        setLoading(false);
      });
  }, [url]);

  return render({ data, loading, error });
}
```
In this example, the `DataFetcher` component takes a `url` prop to fetch data from and a `render` prop, which is a function that receives the fetched data, loading state, and error state. The `DataFetcher` component manages the logic for fetching data and then calls the `render` function to render the appropriate UI based on the current state. This allows you to reuse the data fetching logic across different components while still providing flexibility in how the UI is rendered. The render props pattern promotes code reuse and separation of concerns, making it easier to maintain and scale your React applications.

## What is React memo?
`React.memo` is a higher-order component that allows you to optimize the performance of your React components by memoizing the rendered output. It is used to prevent unnecessary re-renders of a component when its props have not changed. When you wrap a component with `React.memo`, React will compare the current props with the previous props, and if they are the same, it will skip rendering the component and reuse the previous output. This can improve performance, especially for components that are expensive to render or have complex logic. However, it's important to note that `React.memo` only performs a shallow comparison of props, so if you have complex objects as props, you may need to provide a custom comparison function to ensure that it works correctly.
```jsx
const MyComponent = React.memo(function MyComponent(props) {
  // Component logic and rendering
});
```
In this example, `MyComponent` is wrapped with `React.memo`, which means that it will only re-render if its props change. If the props remain the same between renders, React will skip rendering `MyComponent` and reuse the previous output, improving performance by avoiding unnecessary re-renders. This is particularly useful for components that receive a lot of props or have complex rendering logic, as it can help to reduce the amount of work React has to do when updating the UI.

## What is state normalization?
State normalization is a technique used in React applications to manage and structure the state in a way that makes it easier to access and update. It involves organizing the state in a flat structure, often using objects or arrays, rather than nesting data deeply. This can help to avoid issues with deeply nested state updates and make it easier to manage relationships between different pieces of state. Normalizing state can also improve performance by reducing the amount of data that needs to be updated when changes occur, as well as making it easier to implement features like caching and memoization. Libraries like Redux often encourage state normalization to help manage complex application state more effectively.
```javascript
const normalizedState = {
  users: {
    byId: {
      '1': { id: '1', name: 'Alice' },
      '2': { id: '2', name: 'Bob' },
    },
    allIds: ['1', '2'],
  },
};
```
In this example, the state is normalized by organizing the users into a `byId` object, where each user is stored with their ID as the key. The `allIds` array keeps track of the order of the user IDs. This structure allows for easy access to individual users by their ID and simplifies updates to the state, as you can directly modify the relevant user without having to navigate through nested structures. State normalization helps to improve the maintainability and performance of your React applications by providing a clear and efficient way to manage complex state.

## What is optimistic UI update?
Optimistic UI update is a technique in React where the user interface is updated immediately in response to a user action, before the actual data change has been confirmed by the server. This approach provides a more responsive and fluid user experience, as it allows users to see the results of their actions without waiting for a server response. If the server confirms the change, the UI remains as is; if the server returns an error, the UI can be rolled back to its previous state. Optimistic UI updates are commonly used in scenarios like form submissions, liking a post, or adding items to a cart, where immediate feedback is important for user engagement.
```jsx
function LikeButton() {
  const [liked, setLiked] = useState(false);
  const [error, setError] = useState(null);

  const handleLike = () => {
    // Optimistically update the UI
    setLiked(true);
    
    // Simulate a server request
    fakeApiRequest()
      .then(() => {
        // Server confirms the like, do nothing
      })
      .catch(() => {
        // Server returns an error, roll back the UI
        setLiked(false);
        setError('Failed to like the post. Please try again.');
      });
  };

  return (
    <div>
      <button onClick={handleLike}>{liked ? 'Unlike' : 'Like'}</button>
      {error && <p>{error}</p>}
    </div>
  );
}
```
In this example, the `LikeButton` component uses an optimistic UI update approach. When the user clicks the "Like" button, the `liked` state is immediately set to `true`, giving the user instant feedback. A simulated API request is made to confirm the like action. If the request succeeds, the UI remains unchanged; if it fails, the `liked` state is rolled back to `false`, and an error message is displayed. This technique enhances the user experience by providing immediate feedback while still handling potential errors gracefully.

## What is useTransition?
`useTransition` is a React hook that allows you to manage the state of a transition in your application. It is used to indicate that a certain part of the UI is in a "transitioning" state, which can be useful for showing loading indicators or preventing user interactions during the transition. The `useTransition` hook returns an array with two values: a boolean indicating whether the transition is currently active, and a function to start the transition. When you call the function to start the transition, it will set the transitioning state to `true`, and you can use this state to conditionally render loading indicators or disable buttons until the transition is complete.
```jsx
import { useTransition } from 'react';
function MyComponent() {
  const [isPending, startTransition] = useTransition();

  const handleClick = () => {
    startTransition(() => {
      // Perform some state updates or data fetching here
    });
  };

  return (
    <div>
      <button onClick={handleClick} disabled={isPending}>
        {isPending ? 'Loading...' : 'Click Me'}
      </button>
    </div>
  );
}
```
In this example, the `MyComponent` uses the `useTransition` hook to manage a transition state. When the button is clicked, the `startTransition` function is called, which sets the `isPending` state to `true`. This allows you to conditionally render a loading indicator (in this case, changing the button text to "Loading...") and disable the button while the transition is active. Once the transition is complete, you can set `isPending` back to `false` to re-enable the button and update the UI accordingly. This helps to improve the user experience by providing feedback during asynchronous operations or state updates.

## What is useDeferredValue?
`useDeferredValue` is a React hook that allows you to defer the rendering of a value until the browser has had a chance to paint. This can be useful for improving the performance of your application by preventing expensive computations or rendering from blocking the main thread. When you use `useDeferredValue`, React will delay the update of the value until the next render cycle, allowing the browser to remain responsive and avoid jank. This is particularly beneficial when you have a component that receives a large amount of data or performs complex calculations, as it can help to ensure that the UI remains smooth and responsive even when there are heavy updates happening in the background.
```jsx
import { useDeferredValue } from 'react';
function MyComponent({ value }) {
  const deferredValue = useDeferredValue(value);

  return (
    <div>
      <p>Current Value: {value}</p>
      <p>Deferred Value: {deferredValue}</p>
    </div>
  );
}
```
In this example, the `MyComponent` receives a `value` prop and uses the `useDeferredValue` hook to create a `deferredValue`. The `deferredValue` will only update after the browser has had a chance to paint, allowing the UI to remain responsive even if the `value` prop changes frequently or involves expensive computations. This can help to improve the performance of your application by preventing unnecessary re-renders and ensuring that the user interface remains smooth and responsive.

## What is React Query / TanStack Query?
React Query, now known as TanStack Query, is a powerful data-fetching library for React applications. It provides a simple and efficient way to manage server state, handle caching, and synchronize data between the client and server. With React Query, you can easily fetch, cache, and update data in your React components without having to worry about complex state management or manual caching strategies. It also offers features like automatic refetching, pagination, and optimistic updates, making it a great choice for handling asynchronous data in your React applications. By using React Query, you can improve the performance and user experience of your application by ensuring that data is always up-to-date and efficiently managed.
```jsx
import { useQuery } from 'react-query';
function MyComponent() {
  const { data, error, isLoading } = useQuery('fetchData', () =>
    fetch('/api/data').then((res) => res.json())
  );

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <div>
      <h1>Data:</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}
```
In this example, the `MyComponent` uses the `useQuery` hook from React Query to fetch data from an API endpoint. The `useQuery` hook takes a query key ('fetchData') and a function that returns a promise (the fetch request). It returns an object containing the fetched data, any error that occurred, and a loading state. The component conditionally renders a loading message, an error message, or the fetched data based on the state of the query. This demonstrates how React Query simplifies data fetching and state management in React applications, allowing you to focus on building your UI without worrying about the complexities of asynchronous data handling.

## What is React error handling strategy?
React provides a built-in error handling strategy through the use of Error Boundaries. An Error Boundary is a React component that catches JavaScript errors anywhere in its child component tree, logs those errors, and displays a fallback UI instead of the component tree that crashed. This allows you to gracefully handle errors in your application without crashing the entire app. To create an Error Boundary, you can define a class component that implements the `componentDidCatch` lifecycle method, which is called when an error is thrown in any of its child components. You can also use the `getDerivedStateFromError` static method to update the state and render a fallback UI when an error occurs. By using Error Boundaries, you can improve the user experience by providing a way to handle errors gracefully and prevent the entire application from crashing due to unhandled exceptions.
```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    console.error('Error caught by Error Boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
  }
}
```
In this example, the `ErrorBoundary` component is a class component that implements the error handling strategy in React. It uses the `getDerivedStateFromError` method to update its state when an error occurs, which triggers a re-render to display a fallback UI. The `componentDidCatch` method is used to log the error details for debugging purposes. By wrapping your components with the `ErrorBoundary`, you can ensure that any errors that occur within those components are caught and handled gracefully, preventing the entire application from crashing and providing a better user experience.

## What is testing pyramid in React apps?
The testing pyramid is a concept in software testing that describes the different levels of testing and their relative importance in ensuring the quality of an application. In the context of React applications, the testing pyramid typically consists of three levels: unit tests, integration tests, and end-to-end (E2E) tests. Unit tests focus on testing individual components or functions in isolation, ensuring that they work as expected. Integration tests verify that different components or modules work together correctly, while E2E tests simulate real user interactions to test the entire application flow. The idea behind the testing pyramid is to have a larger number of unit tests at the base, fewer integration tests in the middle, and even fewer E2E tests at the top, as E2E tests tend to be more complex and time-consuming to run. By following this structure, you can ensure that your React application is thoroughly tested while maintaining a balance between test coverage and efficiency.
```jsx
// Example of a simple unit test for a React component using Jest and React Testing Library
import React from 'react';
import { render, screen } from '@testing-library/react';
import '@testing-library/jest-dom/extend-expect';
import MyComponent from './MyComponent';

test('renders MyComponent with correct text', () => {
  render(<MyComponent />);
  const element = screen.getByText(/Hello, World!/i);
  expect(element).toBeInTheDocument();
});
```
In this example, we have a simple unit test for a React component called `MyComponent`. The test uses Jest and React Testing Library to render the component and check if it contains the text "Hello, World!". This is an example of a unit test, which focuses on testing a single component in isolation. In a complete testing strategy, you would also include integration tests to verify that multiple components work together correctly, and end-to-end tests to simulate user interactions and test the entire application flow. By following the testing pyramid, you can ensure that your React application is well-tested and maintainable.