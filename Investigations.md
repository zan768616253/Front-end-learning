## [React](https://facebook.github.io/react/)
Primary Javascript libraries.
- [Lifecycle](https://facebook.github.io/react/docs/react-component.html#the-component-lifecycle)
 - [Why not suggest using `setState()` in `componentDidMount`](https://github.com/airbnb/javascript/issues/684)
- [PureComponent](): changes the life-cycle method `shouldComponentUpdate` and adds some logic to automatically check whether a re-render is required for the component. This allows a PureComponent to call method `render` only if it detects changes in `state` or `props`. It should be used carefully, as the PureComponent does shallow comparison, changes **inside** `props` or `state` will be ignored.
- [Refs and Dom](https://facebook.github.io/react/docs/refs-and-the-dom.html#adding-a-ref-to-a-class-component)
- Server side rendering
- [value and defaultValue](https://github.com/facebook/react/issues/2764)
- [Composition vs inheritance](https://reactjs.org/docs/composition-vs-inheritance.html), see why [Composition over inheritance](https://en.wikipedia.org/wiki/Composition_over_inheritance)
## [Redux](http://redux.js.org/)
- [Core Concepts](http://redux.js.org/docs/introduction/CoreConcepts.html#core-concepts)
- Three Principles
  - Single source of truth
  - State is read-only
  - Changes are made with pure functions
- [redux-thunk](https://github.com/gaearon/redux-thunk)
- [How should I split my logic between reducers and action creators? Where should my “business logic” go?](https://redux.js.org/docs/faq/CodeStructure.html#how-should-i-split-my-logic-between-reducers-and-action-creators-where-should-my-business-logic-go)
- [Tests for Redux](http://redux.js.org/docs/recipes/WritingTests.html)
  - In order to be able to test the App component itself without having to deal with the decorator, we recommend you to also export the undecorated component:([Why?](https://github.com/reactjs/redux/issues/1534))

 ```Javascript
  import { connect } from 'react-redux'
  // Use named export for unconnected component (for tests)
  export class App extends Component { /* ... */ }

  // Use default export for the connected component (for app)
  export default connect(mapStateToProps)(App)
  ```

## [react-router](https://github.com/ReactTraining/react-router)
React Router v4 is a complete rewrite, the gap between it and v2/v3 is in this [Link](https://github.com/ReactTraining/react-router/blob/master/packages/react-router/docs/guides/migrating.md)
One of the changes we need to accept is for Nesting Routes: There is no longer a configuration object. Instead, the application serves as its own “configuration”, determining what to render while it renders.
- The problem multiple paths for the same component
  1. Use a regular expression to cover multiple paths. `<Route path="/(|info)" component={Information} />`
  2. Use array.map to render several <Route>s.
  ```Javascript
  [`${this.path}`, `${this.path}/:activePanel`].map((p, i) =>
    <Route
      exact
      key={i}
      path={p}
      component={
      props => (<Navigations {...props} links={links} />)
      }
    />)
  ```
- Global 404 page solution(For React-Router v4).[Reference](https://medium.com/@pshrmn/no-config-no-problem-part-2-e93ad3559801)
  1. Redirect to /404. In this way, the path would be lost.
  2. Via Redux. Use a component to change the state of store, then the root component will re-render the whole page.
  > There is limitation for this approach, the back button of browser does not work as the state would not be changed until refresh. One solution is checking url in NoFound component, need more investigation to find a better way.

## [Lerna](https://github.com/lerna/lerna)
Lerna is a tool that optimizes the workflow around managing multi-package repositories with git and npm.

- `$ lerna bootstrap` Bootstrap the packages in the current Lerna repo. Installs all of their dependencies and links any cross-dependencies. When run, this command will:
  1. `npm install` all external dependencies of each package.
  2. Symlink together all Lerna `packages` that are dependencies of each other.
  3. `npm prepublish` all bootstrapped packages.

## Gulp
## Babel
## [Webpack](https://webpack.js.org)
- [webpack-dev-middleware](https://webpack.js.org/guides/development/#using-webpack-dev-middleware)
The middleware will cause webpack to compile files in-memory. When a compilation is running, it will delay the request to a file until the compilation is done.
- [Migrating-from-v1-to-v2](https://webpack.js.org/guides/migrating/ )
Some changes' details are available here.
- [isparta](https://github.com/douglasduteil/isparta)
DEPRECATED
Not all the istanbul command/options are available with isparta and it is No Maintenance Intended.
- [isparta-loader](https://github.com/deepsweet/isparta-loader)
DEPRECATED
The same as isparta.
- [babel-plugin-istanbul](https://github.com/istanbuljs/babel-plugin-istanbul)
This babel plugin is used for coverage.
- [UglifyJS Webpack Plugin](https://github.com/webpack-contrib/uglifyjs-webpack-plugin)
This plugin uses UglifyJS v2 to minify your JavaScript.
- [UglifyJS — the compressor](http://lisperator.net/uglifyjs/compress)
The compressor is a tree transformer which reduces the code size by applying various optimizations on the AST
- [CommonsChunkPlugin](https://webpack.js.org/plugins/commons-chunk-plugin/)
Separating common modules from bundles, the resulting chunked file can be loaded once initially, and stored in cache for later use.
- [Devtool](https://webpack.js.org/configuration/devtool/)
This option controls if and how source maps are generated.

## Jasmine
## [Karma](https://github.com/karma-runner/karma)
## [Enzyme](https://github.com/airbnb/enzyme)
 - DOM Rendering APIs: http://airbnb.io/enzyme/docs/api/index.html
 - Selector such as Foo[bar="baz"] previously would not return any components when rendering with mount. See details in this opened PR: https://github.com/airbnb/enzyme/pull/538
 - Test a component that uses DOM api's such as `elem.getBoundingClientRect();` that require the DOM nodes be attached to a document. More details for the options: http://airbnb.io/enzyme/docs/api/ReactWrapper/detach.html

## [PhantomJS](http://phantomjs.org/)
One major use case of PhantomJS is headless testing of web applications. It is suitable for general command-line based testing, within a precommit hook, and as part of a continuous integration system.
> A **headless browser** is a web browser without a graphical user interface. [Reference](https://en.wikipedia.org/wiki/Headless_browser)

## [Protractor](http://www.protractortest.org)
`Protractor` is a convenient wrapper around `WebDriverJS` with several really neat Angular specific features. It does not mean you have to use them or you cannot test other non-angular applications. `Protractor` is a **generic e2e tool** that you can use for e2e testing of any web application.
 - `Protractor` would start a selenium-webdriver server automatically if you omit the `seleniumAddress` config option. But before running a standalone Selenium Server, you'll need to install the necessary binaries with `webdriver-manager update`.
 - `PhantomJS` not support ES6 yet(will do in [2.5](https://github.com/ariya/phantomjs/issues/14506)). So we we need to include `babel-polyfill` when build in `webpack`.

## [Selenium](http://www.seleniumhq.org/docs/01_introducing_selenium.jsp#test-automation-for-web-applications)

## [NGINX](https://www.nginx.com/)
- Use NGINX As A Reverse Proxy To Your Containerized Docker Applications: https://www.thepolyglotdeveloper.com/2017/03/nginx-reverse-proxy-containerized-docker-applications/

## [fetch-mock api document](https://npmdoc.github.io/node-npmdoc-fetch-mock/build/apidoc.html)

## [SASS](http://sass-lang.com/guide)
- Partials
You can create partial Sass files that contain little snippets of CSS that you can include in other Sass files. This is a great way to modularize your CSS and help keep things easier to maintain. A partial is simply a Sass file named with a leading underscore. You might name it something like `_partial.scss`. The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file. Sass partials are used with the `@import` directive.
- [Mixin](http://sass-lang.com/guide#topic-6-SCSS)
Some things in CSS are a bit tedious to write, especially with CSS3 and the many vendor prefixes that exist. A mixin lets you make groups of CSS declarations that you want to reuse throughout your site. You can even pass in values to make your mixin more flexible. A good use of a mixin is for vendor prefixes. Here's an example for `border-radius`.
  ```CSS
  @mixin border-radius($radius) {
    -webkit-border-radius: $radius;
       -moz-border-radius: $radius;
        -ms-border-radius: $radius;
            border-radius: $radius;
  }
  .box { @include border-radius(10px); }
  ```
- [Sass Maps](https://webdesign.tutsplus.com/tutorials/an-introduction-to-sass-maps-usage-and-examples--cms-22184)

## Scroll in Animation
  - [Web animation API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API), this is still an experimental technology, does not support to IE & Safari yet.
  - Open Source React package: [React-Scroll](https://github.com/fisshy/react-scroll): Component for basic scrolling and smooth scrolling.
  - Visual reference for scrolling in animation: http://easings.net/

## Responsive Layout
  - ICS Design guide: https://design-guide.w3ibm.mybluemix.net/layout/responsive-grid
  - Pink components comes with bootstrap's grid, which makes creating page layouts easy. If you're familiar with bootstrap, you can use all of the bootstrap grid classes (.col-sm-4 etc). Find out more about bootstrap grid [here](https://v4-alpha.getbootstrap.com/layout/grid/).
