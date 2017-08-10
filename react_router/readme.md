##### History


Three important types of History browser, hash, and memory.


````
import {
  createBrowserHistory,
  createHashHistory,
  createMemoryHistory
} from 'history'

````

History contains a object which have various properties

1.Location->Reflects where your application currently is.
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




2.Navigation ->IT contains number of methods which makes the router interesting.
`history.push({ pathname: '/new-place' })`->Good for link 

`history.replace({ pathname: '/go-here-instead' })` ->Good for redirections.
 

#####Listen ->History uses observer pattern to allow outside code to be notified when the location changes.


````
const youAreHere = document.getElementById('youAreHere')
history.listen(function(location) {
  youAreHere.textContent = location.pathname
})

````

A React Router’s router component will subscribe to its history object so that it can re-render whenever the location changes.
