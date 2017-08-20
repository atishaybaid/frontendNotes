
# Browser Router(React Route v4)

//Introduction needed

React Router features  dynamic routing,which is different from earlier versions of react-router,and other frameworks
such as angular,ember supporting static routing.


#### Installation
`npm install --save react-router-dom`

### Dynamic Routing

It allows us to define routes,anywhere inside our react application whereever we need(as your app is rendering, not in a configuration or convention outside of a running app.),earlier with static routing
we had difine all the routes before the app getting bootstraped.



### Rendering with React Router

Router components only expect to receive a single child element.

````
ReactDOM.render(
  <BrowserRouter>
    <App/>
  <BrowserRouter/>,
  document.getElementById('app'));
````

To Overcome this limitation we can put our application/routing logic inside app component.

````
const App = () => (
  <div>
    <Header />
    <Main />
  </div>
)

````

//Need more clarification
#### History


Three important types of History i.e  browser, hash, and memory.


````
import {
  createBrowserHistory,
  createHashHistory,
  createMemoryHistory
} from 'history'

````

History contains a object which have various properties

1. Location->Reflects where your application currently is.
contains properties
````
{
  pathname: '/here',
  search: '?key=value',
  hash: '#extra-information',
  state: { modal: true },
  key: 'abc123'
}
````


The browser maintains a array of Location objects and keeps a pointer to the current Location.
For the memory history, these are explicitly defined. For both the browser and hash histories, the array and index is controlled by the browser and cannot be directly accessed


//Need more clarificatoin

2. Navigation ->It contains number of methods which makes the router interesting.

`history.push({ pathname: '/new-place' })`->Good for link 

`history.replace({ pathname: '/go-here-instead' })` ->Good for redirections.
 

##### Listen ->History uses observer pattern to allow outside code to be notified when the location changes.


````
const youAreHere = document.getElementById('youAreHere')
history.listen(function(location) {
  youAreHere.textContent = location.pathname
})

````

A React Router’s router component will subscribe to its history object so that it can re-render whenever the location changes.







#### Routes ->. Main building block of react application,Anywhere that you want to only render something if it matches the location’s pathname, you should create a <Route> element. ####
#### Path ->A `<Route>` expects a path prop string that describes the type of pathname that the route matches — for example, <Route path='/roster'/> should match a pathname that begins with /roster[2]. When the current location’s pathname is matched by the path, the route will render a React element. ####


````

<Route path='/roster'/>
// when the pathname is '/', the path does not match
// when the pathname is '/roster' or '/roster/2', the path matches
// If you only want to match '/roster', then you need to use
// the "exact" prop. The following will match '/roster', but not
// '/roster/2'.
<Route exact path='/roster'/>


````




#### Creating our routes -> <Route>s can be created anywhere inside of the router, but often it makes sense to render them in the same place. 
You can use the<Switch> component to group <Route>s. The <Switch> will iterate over its children elements (the routes) and only render the first one that matches the current pathname.


````
<Switch>
  <Route exact path='/' component={Home}/>
  {/* both /roster and /roster/:number begin with /roster */}
  <Route path='/roster' component={Roster}/>
  <Route path='/schedule' component={Schedule}/>
</Switch>

````


#### Route Renders in following three ways


1. Component — A React component. When a route with a component prop matches, the route will return a new element whose type is the provided React component (created using React.createElement).
2. render — A function that returns a React element [5]. It will be called when the path matches. This is similar to component, but is useful for inline rendering and passing extra props to the element.
3. children - A function that returns a React element. Unlike the prior two props, this will always be rendered, regardless of whether the route’s path matches the current location.


````


<Route path='/page' component={Page} />
const extraProps = { color: 'red' }
<Route path='/page' render={(props) => (
  <Page {...props} data={extraProps}/>
)}/>
<Route path='/page' children={(props) => (
  props.match
    ? <Page {...props}/>
    : <EmptyPage {...props}/>
)}/>

````






#### Refs
1. Offical Docs -> https://reacttraining.com/react-router/web/guides/philosophy
