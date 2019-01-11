# React Securing Applications

## Initial Setup

### Make project folder

```bash
mkdir project && cd project
```

### React Create App

```bash
create-react-app secure
```

### Add basic project code

Replace `public` and `src` in the create react app with those folders from the exercise files.

### Install `react-router-dom` 

```bash
yarn add react-router-dom
```

### Run app

```bash
yarn start
```

### Install Flow

```bash 
yarn add flow-bin
```

### Add a script to run flow

@ `package.json`

```json
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject",
    "flow": "flow"
  }
```

### Setup flow

```bash
yarn flow init
```

@ `.flowconfig`

Here you can add flow config.  [See Flow Docs - Config](https://flow.org/en/docs/config/)

### Add Flow to a document

@ `App.js` 

```javascript
// @flow
```

You can add this decorator to any files you want Flow to parse.

### Test flow

```bash
yarn flow
```

Returns the errors in the `Appjs` file in the terminal.

### Setup ESLint

```bash
yarn global add eslint
```

### Install `eslint-airbnb-config`

```bash
yarn add eslint-airbnb-config
```

Warns of unmet dependancies

```bash
warning " > eslint-config-airbnb@16.1.0" has unmet peer dependency "eslint@^4.9.0".
warning " > eslint-config-airbnb@16.1.0" has unmet peer dependency "eslint-plugin-import@^2.7.0".
warning " > eslint-config-airbnb@16.1.0" has unmet peer dependency "eslint-plugin-jsx-a11y@^6.0.2".
warning " > eslint-config-airbnb@16.1.0" has unmet peer dependency "eslint-plugin-react@^7.4.0".
```

Not sure why these are not installed but they need to be, so

```bash
yarn add eslint@^4.9.0 eslint-plugin-import@^2.7.0 eslint-plugin-jsx-a11y@^6.0.2 eslint-plugin-react@^7.4.0
```

### Config `eslint`

```bash
touch .eslintrc
```

@ `.eslintrc`

```javascript
{
  "extends": "airbnb",
  "plugins": ["react", "jsx-a11y", "import"],
  "rules": {
    "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }]
  }
}
```



## Commit a release to Github

### Add docs

```bash
mkdir docs
```

### Edit readme

```md
# React - Securing Applications

## Releases

- Release 1.0.0 - Initial setup
```

Move the create-react-app readme into docs and rename to create-react-app.md

### Setup Github Repo

```bash
git init && git add . && git commit
```

### Push to master

```bash
git push origin master
```

### Tag this

```bash
git tag -a 1.0.0 && git push origin 1.0.0
```



##  Setup Server

```bash
mkdir client && mkdir server
```





Move everything but the readme and the invisible files into client





## Edit `.gitignore`

Make sure you include `client/src/Auth/auth0-variables.js`. We'll explain that later but just in case we forget, later, we do not want that file included in the git repo!

```
# See https://help.github.com/ignore-files/ for more about ignoring files.

# dependencies
client/node_modules
server/node_modules

# Auth0 secrets
client/src/Auth/auth0-variables.js

# testing
/coverage

# production
/build

# misc
.DS_Store
.env.local
.env.development.local
.env.test.local
.env.production.local

npm-debug.log*
yarn-debug.log*
yarn-error.log*
```



### Install dependancies

```bash
cd server
```



Setup `package.json`

```bash
npm init
```

npm has a better series of prompts for init than yarn...

install

```bash
yarn add body-parser cors express express-jwt jwks-rsa nodemon
```



### Install dev dependancies

```bash
yarn add -D babel-cli babel-preset-env babel-preset-stage-0
```



### Add script to start server

```javascript
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon ./index.js --exec babel-node -e js"
  },
```



### Write the server

```bash
touch index.js
```

@ `index.js`

import modules

```javascript
import express from 'express';
import jwt from 'express-jwt';
import cors from 'cors';
import jwks from 'jwks-rsa';
import bodyParser from 'body-parser';
```

Create the server

```javascript
const app = express();
```

Allow the server to serve json 

```javascript
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(cors());
```

Tell the server where to listen

```javascript
app.listen(4000, () => {
    console.log('Server is running on port 4000');
});
```



### Compile server using ES6

```bash
touch .babelrc
```



### Config babel

Add presets that allow us to write in ES6

@ `.babelrc`

```
{
    "presets": [
        "env",
        "stage-0"
    ]
}
```



OK, you can run the server but it won't serve anything…

### Commit to Github and Release

```bash
cd .. && git add . && git commit
```

Push repo

```bash
git push origin master
```

Tag

```bash
git tag -a 1.1.0 && git push origin 1.1.0
```





## Create API endpoints



### Get stuff from the server

@ `index.js`

```javascript
app.get('/courses', (req, res) => {
    let courses = [
        {
            "id": 1,
            "title": "Building an App with ReactJS and MeteorJS",
            "link": "https://www.lynda.com/React-js-tutorials/Building-App-React-js-MeteorJS/533228-2.html",
            "description": "Meteor and React are a powerhouse combination. Meteor gives you a fast, easy-to-use solution for data management across clients and servers, and React gives you a way to structure your app's UI from reusable components. The combination allows you to create your dream apps: dynamic, data driven, and cross-platform."
          },
          {
            "id": 2,
            "title": "Framer for UX design",
            "link": "https://www.lynda.com/FramerJS-tutorials/UX-Design-Tools-Framer/562923-2.html",
            "description": "You can use Framer to create JavaScript-based app prototypes quickly and easily. UX designers, engineers, interaction designers, and more can get refreshed on UX fundamentals in this course, and then dive into navigating Framer."
          },
          {
            "id": 3,
            "title": "Migrating to TypeScript 2",
            "link": "https://www.lynda.com/JavaScript-tutorials/Migrating-TypeScript-2/585078-2.html",
            "description": "TypeScript is a newer Microsoft language built on JavaScript that is finding wide adoption in the Microsoft, Google, and Angular communities. Like many things JavaScript these days, TypeScript is changing rapidly as it grows."
          },
            {
            "id": 4,
            "title": "From React to React Native",
            "link": "https://www.lynda.com/React-Native-tutorials/From-React-React-Native/577371-2.html",
            "description": "With React Native, you can leverage your existing React knowledge to build native iOS and Android apps. In this course, explore the different components that make up a basic React Native application, and learn how to use this platform to build your own native projects."
          },
            {
            "id": 5,
            "title": "React Native Ecosystem and Workflow",
            "link": "https://www.lynda.com/React-Native-tutorials/React-Native-Ecosystem-Workflow/560206-2.html",
            "description": "React Native makes it easy to develop applications and then deploy them natively to multiple mobile platforms. That said, building a complete app means looking beyond React Native to the different options that can help you customize your workflow."
          },
            {
            "id": 6,
            "title": "Create a CRM mobile application with React Native",
            "link": "https://www.lynda.com/Web-tutorials/Create-CRM-Mobile-Application-React-Native/585274-2.html",
            "description": "You can develop a mobile CRM application using React Native. Learn how set up a project, code the login, work with Redux, add views, use CRUD operations, and more."
          },
            {
            "id": 7,
            "title": "Prototype a CRM mobile application with Framer",
            "link": "https://www.lynda.com/FramerJS-tutorials/Prototype-Mobile-CRM-Application-Framer/587677-2.html",
            "description": "You can create a prototype for a mobile CRM application using Framer. Learn how to create assets, build a mockup, simulate interactions with animations, prototype concepts, and more."
          },
            {
            "id": 8,
            "title": "React Ecosystems",
            "link": "https://www.lynda.com/React-js-tutorials/React-Ecosystems/601831-2.html",
            "description": "React is rarely used by itself. As a result, working effectively with React—especially when developing in a group—means mastering a set of tools. Some of these tools supplement React, while others establish and maintain workflows for efficient development or help React mesh with another set of web-centric tools."
          },
            {
            "id": 9,
            "title": "React: Testing and debugging",
            "link": "https://www.lynda.com/React-js-tutorials/React-Testing-Debugging/592511-2.html",
            "description": "Tracking down bugs in React and among the many different pieces it communicates with can be a challenge. While basic JavaScript testing and debugging tools certainly work, solutions designed specifically to work with React will save you time and effort."
          },
            {
            "id": 10,
            "title": "InVision Craft for UX design",
            "link": "https://www.lynda.com/Craft-tutorials/InVision-Craft-UX-Design/599634-2.html",
            "description": "InVision Craft is suite of plugins that equip designers with tools that simplify some of the more tedious tasks in their UX design workflow and, in turn, speed up the entire process."
          },
            {
            "id": 11,
            "title": "InVision for UX Design",
            "link": "https://www.lynda.com/InVision-tutorials/InVision-UX-Design/599633-2.html",
            "description": "InVision is a platform that provides UX designers with a set of powerful tools for creating interactive prototypes, collaborating with teammates, and managing their UX design workflow."
          },
            {
            "id": 12,
            "title": "GraphQL: Data fetching with Relay",
            "link": "https://www.lynda.com/GraphQL-tutorials/GraphQL-Data-Fetching-Relay/595829-2.html",
            "description": "Want to build more efficient, data-driven React.js applications? Streamline data retrieval with GraphQL and Relay. You can get exactly the data you need—nothing more, nothing less—and predictable results every time."
          }
    ]
    res.json(courses);
})
```

That's how we can serve some json!!



### Postman

install [Postman](https://app.getpostman.com)

Signup and go to the console and enter the url into the get request box

`http://localhost:4000/courses`

your JSON is returned!!



## Initial Auth0 Setup

### Sign up

Set up account with [Auth0](https://auth0.com) and go to [Auth0 Console](https://manage.auth0.com)

### Create an API

Name it anything you want.  Maybe: "react-secure-tutorial"

For the identifier use a fictitious url "https://smerth"

Signing algorithm: "RS256"

Hit create

### Scopes

Under name add `read:courses`.  

Description: `Grant access to all courses.`

Hit the `ADD` button

This scope will be used in the client later.

Later you can add scopes for updating, deleting, etc...



### Create Client

Go to clients and click `Create Client`

Give it a name: `react-secure-tutorial`

Choose "single page application"

Click `Create`



### Client Settings

Go into settings for that client

You can add a logo which will be added to the signup page for logging in with Auth0

Add a description: `Courses for Linked-In`

Add an Allowed Callback URL: `http://localhost:3000/callback`

Allowed Origins (CORS): `http://localhost:3000`

Hit `Save`



## Adding the files and code from Auth0



Go to the Client page then choose the Quickstart tab then choose the React Project.  At the top of the page there will be a download link for demo project code… download the code.



Copy the `Auth` folder and `history.js` from the sample code and paste into the `src` dir of our `client` folder.



Copy the `Callback` folder and place inside the `components` folder in our client.



`auth0-variables.js` is loaded with the credentials for the API and Client you set up on Auth0

These variables are epxorted and then imported into `Auth.js` where they are used to connect to Auth0.

`history.js` provides code to track url changes so the user can go back in the browser.

`Callback` contains a component to load in between while waiting for a connection to Auth0, with a `loading.svg` image.

All we need to do is change the route we want to go to on authentication.  We will go the route `/feed`

@`Auth.js`

```jsx
  handleAuthentication() {
    this.auth0.parseHash((err, authResult) => {
      if (authResult && authResult.accessToken && authResult.idToken) {
        this.setSession(authResult);
        history.replace('/feed');
      } else if (err) {
        history.replace('/feed');
        console.log(err);
        alert(`Error: ${err.error}. Check the console for further details.`);
      }
    });
  }
```



Similarly we change the path for history

@`Auth.js`

```jsx
  setSession(authResult) {
    // Set the time that the access token will expire at
    let expiresAt = JSON.stringify((authResult.expiresIn * 1000) + new Date().getTime());
    localStorage.setItem('access_token', authResult.accessToken);
    localStorage.setItem('id_token', authResult.idToken);
    localStorage.setItem('expires_at', expiresAt);
    // navigate to the home route
    history.replace('/feed');
  }
```





and under `handleAuthentication()` we will add a function to get a token



```jsx
  getAccessToken() {
    const accessToken = localStorage.getItem('access_token');
    if (!accessToken) {
      return new Error('No access token found');
    }
    return accessToken; 
  }
```



Client will not work yet but its a good time to commit everything and tag a release...





## Adding routes for Auth0

@ `client/src/components`

```bash
touch routes.js
```



@ routes.js

Copy and paste all the code from the `routes.js` file in the demo client app from Auth0

Delete 

```jsx
import Home from './Home/Home';
```

Add our components for each page

```jsx
import Contact from './Contact';
import About from './About';
import Feed from './Feed';
```

Make sure we are looking in the right directories

```jsx
import Auth from '../Auth/Auth';
import history from '../history';
```

And add our routes

```jsx
export const makeMainRoutes = () => {
  return (
      <Router history={history} component={App}>
        <div className="container">
          <Route path="/" render={(props) => <App auth={auth} {...props} />} />
          <Route path="/feed" render={(props) => <Feed auth={auth} {...props} />} />
          <Route path="/about" render={(props) => <About auth={auth} {...props} />} />
          <Route path="/contact" render={(props) => <Contact auth={auth} {...props} />} />
          <Route path="/callback" render={(props) => {
            handleAuthentication(props);
            return <Callback {...props} /> 
          }}/>
        </div>
      </Router>
  );
}
```





Now @ `client/index.js`



Remove un-needed modules

```jsx
import React from 'react';

import App from './components/App';
```



add

```jsx
import { makeMainRoutes } from './components/routes';
```



add 

```jsx
const routes = makeMainRoutes();
```



Lastly instead of loading `<App />` we load `routes`

```jsx
ReactDOM.render(routes, document.getElementById('root'));
```





Thats it for routes… push a release.



## Finalizing App Component

@ `client/src/components/App.js`

remove

```jsx
import Feed from "./Feed";
import Contact from "./Contact";
import About from "./About";
import data from "../data/data.json";
```

and remove

```jsx
import Navigation from "./Navigation";
```

Change the import for react-router-dom to link

```jsx
import { Link } from "react-router-dom";
```



Add some functions that are related to authentication



`goTo(route)` will take a route and replace a route in the browser with the route that is passed to the function

```jsx
  goTo(route) {
    this.props.history.replace(`/${route}`)
  }
```



And these two functions. We attaching the `.auth.login()` function from Auth0 to the props so we can access it.  And the same with logout.

```jsx
  login() {
    this.props.auth.login();
  }

  logout() {
    this.props.auth.logout();
  }
```



Now we want to render a different menu for when we are logged in and when we are logged out.

So starting with

```jsx
  render() {
    return (
      )
  }
```



We can create a pull constant from the auth on props `const { isAuthenticated } = this.props.auth;`





```jsx
  render() {
    const { isAuthenticated } = this.props.auth;
    return (
      )
  }
```



and use it to build an if logic to return a different `<div>`

```jsx
      <div>
        {
          !isAuthenticated() && (
            some content
          )
        }
        {
          isAuthenticated() && (
            some other content
          )
        }
      </div>
```



add the markup for the two different menus

```jsx
render() {
    const { isAuthenticated } = this.props.auth;
    return (
      <div>
        {
          !isAuthenticated() && (
            <div>
              <div className="header">
                <ul className="nav nav-pills pull-right">
                    <li className="btn btn-primary" onClick={this.login.bind(this)}>Log in</li>
                </ul>
                <h3 className="text-muted">Securing React</h3>
              </div>
              <Jumbotron title={this.state.jumbotronTitle} />
            </div>
          )
        }
        {
          isAuthenticated() && (
            <div>
              <div className="header">
                <ul className="nav nav-pills pull-right">
                <li><a onClick={this.goTo.bind(this, 'feed')}>Home</a></li>
                <li><Link to="/about">About</Link></li>
                <li><Link to="/contact">Contact</Link></li>
                    <li className="btn btn-primary" onClick={this.logout.bind(this)}>Log out</li>
                </ul>
                <h3 className="text-muted">Securing React</h3>
              </div>
              <Jumbotron title={this.state.jumbotronTitle} />
            </div>
          )
        }
      </div>
    )
  }
}

export default App;
```



>Important! - Whenever we use a function inside of ES6 we need to bind it...
>
>so instead of this
>
>`onClick={this.goTo('feed')}`
>
>we do...
>
>`onClick={this.goTo.bind(this, 'feed')}`



Lastly delete the data folder from the client because we don't need it...



That finishes the app component...





## Finalizing Feed Component





cd into the client

```bash
cd client
```



Install dependancies

```bash
yarn add auth0-js axios history jwt-decode
```



In the client components delete the `Navigation.js` because it is not being used anymore



@ `Feed.js`

Import modules.

We import `Component` because we are going to import the current stateless component into a statefull component.

```jsx
import React, { Component } from 'react';
import axios from 'axios';
import FeedItem from './FeedItem';
```



Start with a standard statefull component

```jsx
class Feed extends Component {
 render() {
    return (

    )
  }
}
```

initialize the class with a constructor and initialize the state which contains an empty feeds array. 

```jsx
  constructor(props) {
    super(props);
    this.state = {
      feeds: [],
    };
  }
```



Use some life-cycle functions:

Axios module is a promise based HTTP client for the browser and node.js.  We will use it to make a get request of our api.  It takes in the url and a config object which will be used to add items to the request header (like the AccessToken)

We pull the `getAccessToken`, which is a function, out of the auth object on props.  

We add the `getAccessToken()` function to a headers constant.  We use ES6 template strings to build the value of 'Authorization' `like this`Bearer ${getAccessToken()}``

The get request returns a promise so we can use `.then()` to handle the response to place the data into the feeds array (thus updating state)



```jsx
  componentWillMount() {
    const { getAccessToken } = this.props.auth;
    const headers = { 'Authorization': `Bearer ${getAccessToken()}`}
    const url = 'http://localhost:4000/courses';
    return axios.get(url, { headers})
      .then(response => this.setState({ feeds: response.data }));
  }

  login() {
    this.props.auth.login();
  }
```

Now we can render the component

Pull the value `isAuthenticated` out of auth which is on props.

Then return a div containing one of two sets of markup depending on the boolean value of isAuthenticated…  This is what we did in `App.js` already...

Remember you need to bind function which is used in jsx `onClick={this.login.bind(this)}`



>  This bit of javascript magic `{' '}` does what? Prints a blank space?



Remember when mapping  an array into a component you need to use a key

```jsx
this.state.feeds.map((item) => 
          <FeedItem key={item.id} feed={item} />
```



So the render looks like this:

```jsx
  render() {
    const { isAuthenticated } = this.props.auth;

    return (
      <div>
      {
        !isAuthenticated() && (
          <h4>
            You are not logged in! Please {' '}
            <a
              style={{ cursor: 'pointer'}}
              onClick={this.login.bind(this)}
            >Log in</a>
            {' '}to continue.
          </h4>
        )
      }
      {
        isAuthenticated() && (
          this.state.feeds.map((item) => 
          <FeedItem key={item.id} feed={item} />
        )
        )
      }
    </div>
    )
  }
```



Start the server

@ `server`

```bash
yarn start
```

Start the client

@ `client`

```bash
yarn start
```



So now the client is secure, you need to log in to see the data called from the api.



## Secure Server API files

CD into the server

```bash
cd server
```

Add dependancies

```bash
yarn add express-jwt-authz
```



@ `server/index.js`

import dependancies

```jsx
import jwtAuthz from 'express-jwt-authz';
```



Now lets get some code from Auth0… go to your Auth0 control panel, go to APIs, click of the API you created, go to Quick Start and copy the code for the  `jwtCheck()` function

```jsx
var jwtCheck = jwt({
    secret: jwks.expressJwtSecret({
        cache: true,
        rateLimit: true,
        jwksRequestsPerMinute: 5,
        jwksUri: "https://smc.auth0.com/.well-known/jwks.json"
    }),
    audience: 'https://smerth',
    issuer: "https://smc.auth0.com/",
    algorithms: ['RS256']
});
```



Change to a const `const secureApi` and then paste below `app.use(cors());`

Add the scopes we created in the Auth0 console

```jsx 
const checkScopes = jwtAuthz([ 'read:courses' ]);
```

Now in the get call for the feed we can use what we just created

```jsx
app.get('/courses', secureApi, checkScopes, (req, res) => {
```

Now we will not be able to complete the get request if secret, audience and issuer doesn't match and we will only be able to operate with the defined scope (read all the posts)

Ok, if you run the server now you will not be able to access the api, one more peice of work to do, coming up next...



## Finalize API security

Copy the audience variable from the server `index.js`

```jsx
audience: "https://smerth",
```

And add it to `auth0-variables.js`

```jsx
export const AUTH_CONFIG = {
  domain: "YOUR-DOMAIN",
  clientId: "YOUR-CLIENT-ID",
  callbackUrl: "YOUR-CALLBACK-URL",
  apiUrk: "YOUR-API-URK"
};
```



@ `Auth.js`

Change the audience variable, and add the scope

```jsx
  auth0 = new auth0.WebAuth({
    domain: AUTH_CONFIG.domain,
    clientID: AUTH_CONFIG.clientId,
    redirectUri: AUTH_CONFIG.callbackUrl,
    audience: AUTH_CONFIG.apiUrl,
    responseType: "token id_token",
    scope: "openid read:courses"
  });
```



And some time ago we created the function `getAccessToken()` we need to include it in the constructor

```jsx
  constructor() {
    this.login = this.login.bind(this);
    this.logout = this.logout.bind(this);
    this.handleAuthentication = this.handleAuthentication.bind(this);
    this.isAuthenticated = this.isAuthenticated.bind(this);
    this.getAccessToken = this.getAccessToken.bind(this);
  }
```





## Conclusion



In the course we secured our application with a single sign-on and then we secured the API. But if you logout of the application and try to access the contact and about page they will show up. 

So always make sure that all areas of your application are properly secured when you don't want them to be public. 

To do this use the authenticated check we've done on the app.js file across any area you want secured and properly render the pages based on whether someone is or is not authenticated.

Also, there are many online security communities where you can find help. A great place to start is the OWASP site. In the social media section you will find their Slack channel, Meetup links, social links and more. 



