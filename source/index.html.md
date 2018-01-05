---
title: PostIt API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/ludralph/PostIt-Raphael-Etim'> &copy PostIt API by Raphael Etim</a>

includes:
  - users
  - groups
  - errors

search: true
---

# Introduction
Welcome to the PostIt API - A RESTful web service that allow users create accounts, create groups, add users to groups and post messages to created groups. The Postit API is organized around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use JSON Web Tokens (JWT) for authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. JSON is returned by all API responses, including errors. this documentation will get you started on how you can easily consume this API. To consume this API, your stack should definitely be Javascript as we are yet to cover other languages. You can view code examples in the dark area to the right.

>Base API Endpoint

```
https://postit-app-ralph.herokuapp.com/api/v1

```

# Development

PostIt application was built with Node.js running express server. Postgres is the database used for the application and sequelize is the ORM used for connecting to the database.

# Installation

To test out the endpoints in this API documentation, you need to set up your working environment locally. Follow the steps below to get you started.
First, get Node.js v6.11.0 or later installed in your machine Ensure you have postgres installed also. Clone the github repo and run this command in your terminal, `git clone https://github.com/ludralph/PostIt-Raphael-Etim.git`. After cloning, run the command `cd PostIt-Raphael-Etim` to be in the project directory. Setup your database url in the .env file. Also run `npm install` to install all the npm package dependencies. Finally, to get the app running, start up the server with the command `npm start`.

# Authentication
PostIt uses (username and password) fields to allow users access to the API protected routes. On registering or login, a token is generated.

PostIt expects for the token to be included in all API requests to the server in a header that looks like the following:

Authorization: **token**.

Some endpoints (routes) in this API are protected. They require an access token (x-auth) in the request headers. You can get this token when you signup as a new user or login as existing user.
<aside class="notice">You must replace YOUR_AUTH_TOKEN with our own x-auth token, which the server sends back in the response headers when you sign up or sign in.</aside>

> To authorize requests to protected endpoints, set the x-auth token in the request header like this:

```javascript
{
  "x-auth":"YOUR_AUTH_KEY"
}

```

# Endpoints Summary

Base Endpoint: `https://postit-app-ralph.herokuapp.com/api/v1`

The endpoints for the listed routes should be appended to the base endpoint to get the full endpoint.

### User Routes

Feature | Request type | Endpoint
--------| -------- | --------
Sign up | POST     | '/signup'
Sign in | POST     | '/signin'
Get User groups | GET | '/user/:userId/groups'
Search Users | GET | '/search/users'

### Recovery Routes
 
Feature | Request type | Endpoint
--------| -------- | --------
Forgot Password | PUT | '/forgotpassword'
Reset Passwprd | PUT | '/resetpassword/:token'

### Group Routes

Feature | Request type | Endpoint
--------| -------- | --------
Create new Group | POST | '/group'
Add user to Group | POST | '/group/:groupId/user'
Get Group Users | GET | '/group/:groupId/users'
Post New Message | POST | '/group/:groupId/message'
Get Group Messages | GET | '/group/:groupId/messages'