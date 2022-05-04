# Virtual DOM

https://www.freecodecamp.org/news/a-quick-guide-to-learn-react-and-how-its-virtual-dom-works-c869d788cd44/

Many frameworks such as React and Vue.js get around this problem. They come up with a solution called the Virtual DOM.

The idea is simple. Reading and updating the DOM tree is very expensive. So make as few changes as possible and update as few nodes as possible.

Reducing calls to DOM API involves keeping DOM tree representation in memory. Since we are talking about JavaScript frameworks, choosing JSON sounds legitimate.

This approach immediately reflects changes in the Virtual DOM.

https://medium.com/@deathmood/how-to-write-your-own-virtual-dom-ee74acc13060

https://programmingwithmosh.com/react/react-virtual-dom-explained/

When new elements are added to the UI, a virtual DOM, which is represented as a tree is created. Each element is a node on this tree. If the state of any of these elements changes, a new virtual DOM tree is created. This tree is then compared or “diffed” with the previous virtual DOM tree.

Once this is done, the virtual DOM calculates the best possible method to make these changes to the real DOM. This ensures that there are minimal operations on the real DOM. Hence, reducing the performance cost of updating the real DOM.

# Render Props

https://reactjs.org/docs/render-props.html

```
class Cat extends React.Component {
  render() {
    const mouse = this.props.mouse;
    return (
      <img src="/cat.jpg" style={{ position: 'absolute', left: mouse.x, top: mouse.y }} />
    );
  }
}

class Mouse extends React.Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove(event) {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>

        {/*
          Instead of providing a static representation of what <Mouse> renders,
          use the `render` prop to dynamically determine what to render.
        */}
        {this.props.render(this.state)}
      </div>
    );
  }
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>
        <Mouse render={mouse => (
          <Cat mouse={mouse} />
        )}/>
      </div>
    );
  }
}
```

# React Context

https://hackernoon.com/how-do-i-use-react-context-3eeb879169a2

We use createContext() and pass it an empty object as the default value:

`const FamilyContext = React.createContext({});`
We then create a Provider and a Consumer component and export them so they are available for consumption by other components in your application.

```
export const FamilyProvider = FamilyContext.Provider;
export const FamilyConsumer = FamilyContext.Consumer;

```

<FamilyConsumer /> uses a render prop to expose the context object to its children (in this case a <p /> tag but it could be anything).

# React Hooks

https://levelup.gitconnected.com/dissecting-react-hooks-how-to-use-them-and-are-they-replacing-redux-4bb96fa7569d

https://reactjs.org/docs/hooks-intro.html

https://www.reddit.com/r/reactjs/comments/9tto1x/are_react_hooks_going_to_kill_redux/

The hook state calls are no more “magical” than state calls inside classes. In both cases, the React renderer is maintaining the state for you separately from the class instance / function itself (setState is asynchronous, remember?). Hooks actually make the fact that this is happening more obvious, rather than deceiving you into thinking the state is actually stored on this inside the class instance. React is the one managing state - period.

What hooks allow is for you to package together related logic, which may take place across different parts of the lifecycle of a component, in one place. And then you can reuse this logic in other components. That’s simply not possible with class components. You might have some logic pertaining to one feature split across componentDidMount, componentDidUpdate, and componentWillUnmount, along with a few state calls and state initialization in the constructor and maybe some callbacks that you have to bind in your constructor as well. Hooks let you bundle all that logic together in one place. Do you not see the value in that?

I see myself and other developers doing the same thing over and over again in class components, so I’m personally really excited for hooks as it will let us reuse this logic instead of duplicating it.

Here’s a gif demonstrating what that means for your code structure: https://twitter.com/prchdk/status/1056960391543062528?s=21

https://tinkerylabs.com/ajax-calls-with-react-hooks/

```
function useFetch(url, defaultData) {
    const [data, updateData] = useState(defaultData)

    useEffect(async () => {
        const resp = await fetch(url)
        const json = await resp.json()
        updateData(json)
    }, [url])

    return data
}
```

# Custom Hooks

https://reactjs.org/docs/hooks-custom.html

When we want to share logic between two JavaScript functions, we extract it to a third function. Both components and Hooks are functions, so this works for them too!

_A custom Hook is a JavaScript function whose name starts with ”use” and that may call other Hooks._ For example, useFriendStatus below is our first custom Hook:

# Binding

https://stackoverflow.com/questions/48931995/performance-implications-of-implementing-2-way-data-binding-in-react

https://www.quora.com/What-is-dirty-checking-in-AngularJs-and-how-does-it-work

# Async

https://medium.com/capbase-engineering/asynchronous-functional-programming-using-react-hooks-e51a748e6869

The React.useEffect hook takes a function as an argument and it will call that function after the main render cycle has completed, meaning that you can use it to complete async operations, like calls to an API remote, whether it be GraphQL or RESTful (or SOAP or really whatever you like)

# React and Declarative Programming

https://overreacted.io/making-setinterval-declarative-with-react-hooks/
A React component may be mounted for a while and go through many different states, but its render result describes all of them at once.

```
// Describes every render
  return <h1>{count}</h1>

```

Hooks let us apply the same declarative approach to effects:

```
// Describes every interval state
useInterval(() => {
setCount(count + 1);
}, isRunning ? delay : null);

```

We don’t set the interval, but specify whether it is set and with what delay. Our Hook makes it happen. A continuous process is described in discrete terms.

By contrast, setInterval does not describe a process in time — once you set the interval, you can’t change anything about it except clearing it.

# Functional programming with React

https://levelup.gitconnected.com/functional-react-is-it-possible-ceaf5ed91bfd

# JSX behind the scenes

https://alligator.io/react/jsx-introduction/

Here’s a simple button component, for example:

```
function MyButton() {
  return (
    <button id="main-btn" className="btn btn-small">
      Click me!
    </button>
  );
}
```

Behind the scenes, after transpilation, the code will look like this:

```
function MyButton() {
  return React.createElement(
    "button",
    { id: "main-btn", className: "btn btn-small" },
    "Click me!"
  );
}
```
