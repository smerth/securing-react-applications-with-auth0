# React - Securing Applications with Auth0

This project demonstrates how to set up 0Auth authentication with the Auth0 service. The app is comprised of an ExpressJS server which makes use of JWT to manage authentication tokens. The client implements Auth0 session authentication.

![App Screenshot](https://raw.githubusercontent.com/smerth/securing-react-applications-with-auth0/master/screenshot.png)

## Setup and installation

### App and dependancies

- clone the repository
- install server dependancies

```bash
yarn install
```

- install client dependancies

```bash
yarn install
```

### Secrets

To authenticate with Auth0 you will need to set up an account. You will need to copy you credentials into the Auth folder

@ src/Auth/ create file:

```bash
touch auth0-variables.js
```

Add a variables object:
@ src/Auth/auth0-variables

```javascript
export const AUTH_CONFIG = {
  domain: "YOUR-DOMAIN",
  clientId: "YOUR-CLIENT-ID",
  callbackUrl: "YOUR-CALLBACK-URL",
  apiUrk: "YOUR-API-URK"
};
```

## Run Server and Client

```bash
yarn start
```

## Build Notes

See the docs folder for notes about building the server and app.
