# ![RealWorld Example App](logo.png)

> ### TypeScript + React + Redux Toolkit + NodeJS + Express + PostgreSQL codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the [RealWorld](https://github.com/gothinkster/realworld) spec and API.

### Demo (on the Todo list)&nbsp;&nbsp;&nbsp;&nbsp;[RealWorld](https://github.com/gothinkster/realworld)

This codebase was created to demonstrate a fully fledged fullstack application built with **TypeScript + React + Redux Toolkit + NodeJS + Express + PostgreSQL** including CRUD operations, authentication, routing, pagination, and more.

For more information on how to this works with other frontends/backends, head over to the [RealWorld](https://github.com/gothinkster/realworld) repo.

# Content

1. [How it works](#how-it-works)
   1. [General functionality](#general-functionality)
   2. [Routing Guidelines](#routing-guideline)
   3. [Application structure](#application-structure)
   4. [Dependencies](#dependencies)
   5. [Authentication](#authentication)
   6. [Error handling](#error-handling)
2. [Getting Started](#getting-started)
   1. [Run locally](#run-locally)
   2. [Port](#port)
3. [Contributing](#contributing)
4. [License](#license)

# How it works

## General functionality

I added to my project the functionalities, that was in the [general functionalities](https://realworld-docs.netlify.app/docs/implementation-creation/features) on the [RealWorld website](https://realworld-docs.netlify.app/)

## Routing Guidelines

I added to my project the routes, that was in the [routing guideline](https://realworld-docs.netlify.app/docs/specs/frontend-specs/routing) on the [RealWorld website](https://realworld-docs.netlify.app/)

## Application structure

### Client

`index.tsx`, `index.css` - The entry point of the client.

`App.tsx` - The main component of the component tree. This contains the main layout route and other routes.

`app/` - This folder contains

- the types of the client side,
- create instance function of axios package,
- constants,
- hooks definitions and
- store.ts file for Redux Toolkit.

`components/` This folder contains

- compnents and
- css files.

`features/` - This folder contains

- the feature related components
- css files and
- feature related redux slice and API files.

`pages/` - This folder contains

- the page related components and
- css files.

`utils/` - This folder contains the utility functions of client side.

### Server

`app.ts` - The entry point of the client. This file contains

- express server definition and
- binding of setHeaders, errorHandler middleware and routing.

`controller/` - This folder contains controller functions.

`db/` - This folder contain db.ts file, that create a new Pool.

`middleware/` - This folder contains middleware functions.

`models/` - This folder contains functions that communicate with the database and queryTexts.ts file. There are sql queries in the queryText.ts.

`routes/` - This folder contains the route functions. The app use Express Router.

`types/` - This folder contains the types of the server side.

`utils/` - This folder contains the utility functions of server side.

## Dependencies

### Client

- Basic react packages
  - `react`, `@types/react`
  - `react-dom`, `@types/react-dom`
  - `react-scripts`
  - `@types/node`
- `typescript` - The app use TypeScript.
- `react-markdown` - For rendering the article body.
- Redux Toolkit
  - `reduxjs/toolkit` - The app use Redux Toolkit.
  - `react-redux`, `@types/react-redux` - For connection between React and Redux.
- `react-router-dom` - For the routing using React Router package version 6.
- `axios` - For the requests using axios package.
- Font Awesome
  - `fortawesome/fontawesome-svg-core` - For using SVG icons.
  - `fortawesome/free-solid-svg-icons` - For using free solid icons from Font Awesome package.
  - `fortawesome/free-regular-svg-icons` - For using free regular icons from Font Awesome package.
  - `fortawesome/react-fontawesome` - For using FontAwesomeIcon component.
- Testing
  - `@types/jest`
  - `testing-library/jest-dom`
  - `testing-library/react`
  - `testing-library/user-event`

### Server

- `typescript` - The app use TypeScript.
- `express`, `@types/express` - The app use Express framework.
- `bcrypt`, `@types/bcrypt` - For hashing the password.
- `dotenv` - For the env variables in the server side.
- `jose` - For the jwt authentication.
- `pg, @types/pg` - For the connection to the postgres database.
- `randomstring`, `@types/randomstring` - For create unique ids and resource ids.
- `slugify` - For create URL friendly slug from title.
- `ts-node-dev` - For the running the server.

## Authentication

The app use for the authentication JWT Token.
The request header has Authorization property. This property contain a string or null.
The string looks like:

```
'Token (the value of the token)'
```

The app use Express Router for the routes. The routes can contain

- authRequired or
- authOptional middleware.

The authRequired middleware check the token is exist or not. Verify the token with jwt verifyToken method and get the payload with the user data, if the token exist. The username will be searched in the database and add to the req.user or throw an error message with status code 401.

The authOptional middleware is same as the authRequired middleware, but add to the req.user a null value, if token is not exist.

Sign Token method of JWT use for create a token.

## Error Handling

The app use classes for the Errors. Each Error has

- an id (type: string),
- a name (type: string) and
- a message (type: string) properties.

The errorHandler middleware return a json with status code based on the error classes or in default case with status code 500.

The returned error looks like:

```json
{
  "errors": {
    "body": [
      {
        "id": "KHDLKkjdfk",
        "name": "Not Found Error",
        "message": "User is not found"
      }
    ]
  }
}
```

## Input Validation

The given inputs on the client side are validate on the server side. The input validation functions have check functions, that return an array.
This array looks like:

```json
[
  {
    "id": "KHDLKkjdfk",
    "text": "Username must be between 6 and 15 characters"
  }
]
```

The input validation function run the next function if there are not errors. If there are errors throw an error message with status code 422.

# Getting started

## Run locally

### Clone Repository and install dependencies

```
  clone this repository
  open the client folder
    npm ci
  open the server folder
    npm ci
```

### Modify the tsconfig.json

```json
  open the tsconfig.json in the server folder
  if name of the top-level folder is not realworld-implementation, then change this property
    "rootDir": "../../<name of the top-level folder>"
```

### Install PostgreSQL Server and create database

```
  install PostgreSQL 13.3 Server or higher
  create db
  open psql shell
  create a database with CREATE DATABASE <DB_NAME>; command
```

### Create .env file

```
  create a .env file in the server folder, that has this values
  API_PORT: select a port (not 3000) for example: 8080
  DB_HOST: localhost
  DB_USER: postgres username (default postgres)
  DB_PASS: password of the PostgreSQL Server
  DB_PORT: postgres port
  (values of the DB_PASS and the DB_PORT you can add in the installer of the PostgresSQL Server)
  DB_NAME: name of your database
  JWT_SECRET: add a string
```

### Create tables

```
    open the server folder and run one of the command with the right values from the .env files
      MacOS with Postgres.app
        DATABASE_URL=postgres://<DB_USER>@localhost:<DB_PORT>/<DB_NAME> npm run migrate up
      Windows with Git Bash
        DATABASE_URL=postgres://<DB_USER>:<DB_PASS>@localhost:<DB_PORT>/<DB_NAME> npm run migrate up
      Windows with CMD
        set DATABASE_URL=postgres://<DB_USER>:<DB_PASS>@localhost:<DB_PORT>/<DB_NAME>&&npm run migrate up
      Windows wiht Powershell
        $env:DATABASE_URL="postgres://<DB_USER>:<DB_PASS>@localhost:<DB_PORT>/<DB_NAME>";
        npm run migrate up
```

### Run the app

```
  start the client
    npm start
  start the server
    npm run dev
```

## Port

Client use port 3000. You can add the port of the server in the .env file.

# Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what would like to change.

# License

MIT
