# React

## Router

To create a router in react, you will have to install the react-router-dom package.

```BASH
npm install react-router-dom --save
```

Then modify the main file (not the main component but the index.js file ) with this:

```JS
import React from 'react';
import ReactDOM from 'react-dom';
//CSS
import './Assets/style.css';
// Component
import App from './App';
import Pseudo from './Pseudo';
import NotFound from './NotFound'
// Rooter
import { BrowserRouter as Router, Route, Link, Switch } from 'react-router-dom';

import registerServiceWorker from './registerServiceWorker';

const Root = () => {
	return (
		<Router>
            <div>
                <ul>
                    <li><Link to="/">Home</Link></li>
                    <li><Link to="/Pseudo">Pseudo</Link></li>
                    <li><Link to="/NotFound">NotFound</Link></li>
                </ul>
                <hr />
                <Switch>
                    <Route exact path='/' component={ App } />
                    <Route exact path='/Pseudo' component={ Pseudo } />
                    <Route component={ NotFound } />
                </Switch>
            </div>
        </Router>
	)
}

ReactDOM.render(<Root />, document.getElementById('root'));
registerServiceWorker();

```

Import the components that you need in your router and use this patern. Easy peasy 😁

- ```<Router> </Router>``` -> Anything you need for routes
- ```<Link to="/">Home</Link>``` -> Link about the URL
- ```<Switch> </Switch>``` -> differents directions
- ```<Route exact path='/' component={ App } />``` -> the differents router
- ```<Route component={ NotFound } />``` a route without path for the 404

That's it  :)