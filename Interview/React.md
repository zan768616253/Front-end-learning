## What is React? How is it different from other JS frameworks?
React is an open-source JavaScript library created by Facebook for building complex, interactive UIs in web and mobile applications.

Because React is a small library focused on building UI components, it is necessarily different than a lot of other JavaScript frameworks.

For example, AngularJS (1.x) approaches building an application by extending HTML markup and injecting various constructs (e.g. Directives, Controllers, Services) at runtime. As a result, AngularJS is very opinionated about the greater architecture of your application — these abstractions are certainly useful in some cases, but in many situations, they come at the cost of flexibility.

By contrast, React focuses exclusively on the creation of components, and has few (if any) opinions about an application’s architecture. This allows a developer an incredible amount of flexibility in choosing the architecture they deem “best” — though it also places the responsibility of choosing (or building) those parts on the developer.

[React vs Angular](https://www.codementor.io/codementorteam/react-vs-angular-2-comparison-beginners-guide-lvz5710ha)

[React vs Vue](https://www.codementor.io/vuejsdevelopers/react-or-vue-which-javascript-ui-library-should-you-be-using-6hri3num4)

[React vs Angular vs Vue](https://medium.com/unicorn-supplies/angular-vs-react-vs-vue-a-2017-comparison-c5c52d620176)

## What happens during the lifecycle of a React component?
- High-Level Component Lifecycle

At the highest level, React components have lifecycle events that fall into three general categories:

1. Initialization (**getInitialState(), getDefaultProps(), componentWillMount(), render(), componentDidMount()**)
2. State/Property Updates (**componentWillReceiveProps(), shouldComponentUpdate(), componentWillUpdate(), render(), componentDidUpdate()**)
3. Destruction (**componentWillUnmount()**)

Every React component defines these events as a mechanism for managing its properties, state, and rendered output. Some of these events only happen once, others happen more frequently; understanding these three general categories should help you clearly visualize when certain logic needs to be applied.

For example, a component may need to add event listeners to the DOM when it first mounts. However, it should probably remove those event listeners when the component unmounts from the DOM so that irrelevant processing does not occur.

- Low-Level Component Lifecycle

Within these three general buckets exist a number of specific lifecycle hooks — essentially abstract methods — that can be utilized by any React component to more accurately manage updates. Understanding how and when these hooks fire is key to building stable components and will enable you to control the rendering process (improving performance).

Take a look at the diagram above. The events under “Initialization” only happen when a component is first initialized or added to the DOM. Similarly, the events under “Destruction” only happen once (when the component is removed from the DOM). However, the events under “Update” happen every time the properties or state of the component change.

For example, components will automatically re-render themselves any time their properties or state change. However, in some cases a component might not need to update — so preventing the component from re-rendering might improve the performance of our application.

## What can you tell me about JSX?
When Facebook first released React to the world, they also introduced a new dialect of JavaScript called JSX that embeds raw HTML templates inside JavaScript code. JSX code by itself cannot be read by the browser; it must be transpiled into traditional JavaScript using tools like Babel and webpack. While many developers understandably have initial knee-jerk reactions against it, JSX (in tandem with ES2015) has become the default method of defining React components.

## Are you familiar with Flux?
Flux is an architectural pattern that enforces unidirectional data flow — its core purpose is to control derived data so that multiple components can interact with that data without risking pollution.

The Flux pattern is generic; it’s not specific to React applications, nor is it required to build a React app. However, Flux is commonly used by React developers because React components are declarative — the rendered UI (View) is simply a function of state (Store data).

- Description of Flux

In the Flux pattern, the Store is the central authority for all data; any mutations to the data must occur within the store. Changes to the Store data are subsequently broadcast to subscribing Views via events. Views then update themselves based on the new state of received data.

To request changes to any Store data, Actions may be fired. These Actions are controlled by a central Dispatcher; Actions may not occur simultaneously, ensuring that a Store only mutates data once per Action.

The strict unidirectional flow of this Flux pattern enforces data stability, reducing data-related runtime errors throughout an application.

- Flux vs MVC

Traditional MVC patterns have worked well for separating the concerns of data (Model), UI (View) and logic (Controller) — but many web developers have discovered limitations with that approach as applications grow in size. Specifically, MVC architectures frequently encounter two main problems:

Poorly defined data flow: The cascading updates which occur across views often lead to a tangled web of events which is difficult to debug.

Lack of data integrity: Model data can be mutated from anywhere, yielding unpredictable results across the UI.

With the Flux pattern complex UIs no longer suffer from cascading updates; any given React component will be able to reconstruct its state based on the data provided by the store. The flux pattern also enforces data integrity by restricting direct access to the shared data.

- Difference with AngularJS (1.x)

UI components in AngularJS typically rely on some internal $scope to store their data. This data can be directly mutated from within the UI component or anything given access to `$scope` — a risky situation for any part of the component or greater application which relies on that data.

By contrast, the Flux pattern encourages the use of immutable data. Because the store is the central authority on all data, any mutations to that data must occur within the store. The risk of data pollution is greatly reduced.

- Testing

One of the most valuable aspects of applications built on Flux is that their components become incredibly easy to test. Developers can recreate and test the state of any React component by simply updating the store — direct interactions with the UI (with tools like Selenium) are no longer necessary in many cases.

- Popular Flux Libraries

Redux: perhaps the most popular Flux library today.

## What are stateless components?
Stateless components (a flavor of “reusable” components) are nothing more than pure functions that render DOM based solely on the properties provided to them.
``` JavaScript
const StatelessCmp = props => {
  return (
    <div className="my-stateless-component">
      {props.name}: {props.birthday}
    </div>
  );
};

// ---
ReactDOM.render(
  <StatelessCmp name="Art" birthday="10/01/1980" />,
  document.getElementById('main')
);
```
This component has no need for any internal state — let alone a constructor or lifecycle handlers. The output of the component is purely a function of the properties provided to it.

## List some of the major advantages of React.
Some of the major advantages of React are:
- It increases the application’s performance
- It can be conveniently used on the client as well as server side
- Because of JSX, code’s readability increases
- React is easy to integrate with other frameworks like Meteor, Angular, etc
- Using React, writing UI test cases become extremely easy

## What are the limitations of React?
- React is just a library, not a full-blown framework
- Its library is very large and takes time to understand
- It can be little difficult for the novice programmers to understand
- Coding gets complex as it uses inline templating and JSX

## What do you understand by Virtual DOM? Explain its working.
A virtual DOM is a lightweight JavaScript object which originally is just the copy of the real DOM. It is a node tree that lists the elements, their attributes and content as Objects and their properties. React’s render function creates a node tree out of the React components. It then updates this tree in response to the mutations in the data model which is caused by various actions done by the user or by the system.
This Virtual DOM works in three simple steps.
1. Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.
2. Then the difference between the previous DOM representation and the new one is calculated.
3. Once the calculations are done, the real DOM will be updated with only the things that have actually changed.

## Differentiate between Real DOM and Virtual DOM.
Real DOM	<-> Virtual  DOM
1. It updates slow.	<-> It updates faster.
2. Can directly update HTML.	<-> Can’t directly update HTML.
3. Creates a new DOM if element updates.	<-> Updates the JSX if element updates.
4. DOM manipulation is very expensive.	<-> DOM manipulation is very easy.
5. Too much of memory wastage.	<-> No memory wastage.

## Why can’t browsers read JSX?
Browsers can only read JavaScript objects but JSX in not a regular JavaScript object. Thus to enable a browser to read JSX, first, we need to transform JSX file into a JavaScript object using JSX transformers like Babel and then pass it to the browser.

## What is Props?
Props are short hand for Properties in React. They are read-only components which must be kept pure - immutable. They are always passed down from the parent to the child components through out the application. A child component can never send a prop back to the parent component. This help in maintaining the unidirectional data flow and are generally used to render the dynamically generated data.

## Explain the lifecycle methods of React components in detail.
- componentWillMount() – Executed just before rendering takes place both on the client as well as server-side.
- componentDidMount() – Executed on the client side only after the first render.
- componentWillReceiveProps() – Invoked as soon as the props are received from the parent class and before another render is called.
- shouldComponentUpdate() – Returns true or false value based on certain conditions. If you want your component to update, return true else return false. By default, it returns false.
- componentWillUpdate() – Called just before rendering takes place in the DOM.
- componentDidUpdate() – Called immediately after rendering takes place.
- componentWillUnmount() – Called after the component is unmounted from the DOM. It is used to clear up the memory spaces.

## What do you understand by refs in React?
Refs is the short hand for References in React. It is an attribute which helps to store a reference to a particular React element or component, which will be returned by the components render configuration function. It is used to return references to a particular element or component returned by render(). They come in handy when we need DOM measurements or to add methods to the components.
```JavaScript
class ReferenceDemo extends React.Component{
     display() {
         const name = this.inputDemo.value;
         document.getElementById('disp').innerHTML = name;
     }
     render() {
      return(        
           <div>
              Name: <input type="text" ref={input => this.inputDemo = input} />
              <button name="Click" onClick={this.display}>Click</button>
              <h2>Hello <span id="disp"></span> !!!</h2>
          </div>
      );
     }
 }
 ```
## What do you know about controlled and uncontrolled components?
Controlled Components	<-> Uncontrolled Components
1. They do not maintain their own state	<-> They maintain their own state
2. Data is controlled by the parent component	<-> Data is controlled by the DOM
3. They take in the current values through props and then notify the changes via callbacks	<-> Refs are used to get their current values

## What are Higher Order Components(HOC)?
Higher Order Component is an advanced way of reusing the component logic. Basically, it’s a pattern that is derived from React’s compositional nature. HOC are custom components which wraps another component within it. They can accept any dynamically provided child component but they won’t modify or copy any behavior from their input components. You can say that HOC are ‘pure’ components.
i.e. `connect()` in Redux, `withRouter()` in React-Route.

## What can you do with HOC?
HOC can be used for many tasks like:
- Code reuse, logic and bootstrap abstraction
- State abstraction and manipulation
- Props manipulation

## What are Pure Components?
Pure components are the simplest and fastest components which can be written. They can replace any component which only has a `render()`. These components enhance the simplicity of the code and performance of the application.

## What are the three principles that Redux follows?
Redux is one of the hottest libraries for front end development in today’s marketplace. It is a predictable state container for JavaScript applications and is used for the entire applications state management. Applications developed with Redux are easy to test and can run in different environments showing consistent behavior.
- **Single source of truth**: The state of the entire application is stored in an object/ state tree within a single store. The single state tree makes it easier to keep track of changes over time and debug or inspect the application.
- **State is read-only**: The only way to change the state is to trigger an action. An action is a plain JS object describing the change. Just like state is the minimal representation of data, the action is the minimal representation of the change to that data.
- **Changes are made with pure functions**: In order to specify how the state tree is transformed by actions, you need pure functions. Pure functions are those whose return value depend solely on the values of their arguments.

## List down the components of Redux.
- Action – It’s an object that describes what happened.
- Reducer –  It is a place to determine how the state will change.
- Store – State/ Object tree of the entire application is saved in the Store.
- View – Simply displays the data provided by the Store.

## Explain the role of Reducer.
Reducers are pure functions which specify how the application’s state changes in response to an ACTION. Reducers work by taking in the previous state and action, and then it returns a new state. It determines what sort of update needs to be done based on the type of the action, and then returns new values. It returns the previous state as it is, if no work needs to be done.

## What are the advantages of Redux?
- **Predictability of outcome** – Since there is always one source of truth, i.e. the store, there is no confusion about how to sync the current state with actions and other parts of the application.
- **Maintainability** – The code becomes easier to maintain with a predictable outcome and strict structure.
- **Server side rendering** – You just need to pass the store created on the server, to the client side. This is very useful for initial render and provides a better user experience as it optimizes the application performance.
- **Developer tools** – From actions to state changes, developers can track everything going on in the application in real time.
- **Community and ecosystem** – Redux has a huge community behind it which makes it even more captivating to use. A large community of talented individuals contribute to the betterment of the library and develop various applications with it.
- **Ease of testing** – Redux’s code is mostly functions which are small, pure and isolated. This makes the code testable and independent.
- **Organization** – Redux is precise about how code should be organized, this makes the code more consistent and easier when a team works with it.
