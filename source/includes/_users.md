# Users
To use the API, you would have to signup as a user. Users can create groups, search other users, add them to their groups and send messages in groups to which they belong.
<aside class="notice">Some routes here are protected. You would need to set the x-auth token in the request header to access them.</aside>

## Signup user
This endpoint allows new users create accounts and access protected routes. If the request is successful, the response body would contain a message that welcomes the new user, and a user object that contains user data. This user object contains:

### Request Parameters

Parameter  | Description
---------- | ------------
username   | required  
email      | required
password   | required

### Response Parameters

Parameter | Description
--------- | -----------
message   | A descriptive notification of the outcome of the request
user      | An object that contains the id, name and email of the user
token     | The jwt token returned from the server that will be used to set the x-auth token in the request header
          | 

> Sample Request

```javascript
{
  "username":"johndoe",
  "email":"johndoe@gmail.com",
  "password":"mypassword"
}

```


> Sample Response Body

```javascript
{
    "message": "Signup Successful!",
    "user": {
        "id": 7,
        "name": "johndoe",
        "email": "johndoe@gmail.com"
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7ImlkIjo3LCJuYW1lIjoib2xlb2xlb2xlIiwiZW1haWwiOiJvbGVvbGVvbGVAZ21haWwuY29tIn0sImlhdCI6MTUxMzI1NDkwMSwiZXhwIjoxNTEzMzQxMzAxfQ.JxCIhtDH72ctdKZBYJgE-Q2Aa6InKrAWlAgT82UqkFo"
}

```

### Request
  * Endpoint: : POST: https://postit-app-ralph.herokuapp.com/api/v1/v1/signup
  * Body `(application/json)`

### Response
  * Status: `201: Created`
  * Body `(application/json)`
 
## Signin user
This endpoint allows existing users signin with the same credentials with which they created their accounts. The signin process returns an x-auth token in the header which identifies and authorizes the user to access other endpoints that require authentication. It returns a message welcoming the user, and a user object with the same fields as in the Signup response.

### Request Parameters

Parameter  | Description
---------- | ------------
username   | required  
password   | required

### Response Parameters

Parameter | Description
--------- | -----------
message   | A descriptive notification of the outcome of the request
user      | An object that contains the id, name and email of the user
token     | The jwt token returned from the server that will be used to set the x-auth token in the request header

> Sample Request

```javascript
{
  "username":"johndoe",
  "password":"mypassword"
}

```

> Sample Response Body

```javascript
{
    "message": "Signin successful!",
    "user": {
        "id": 7,
        "name": "johndoe",
        "email": "johndoe@gmail.com"
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7ImlkIjo3LCJuYW1lIjoib2xlb2xlb2xlIiwiZW1haWwiOiJvbGVvbGVvbGVAZ21haWwuY29tIn0sImlhdCI6MTUxMzI2MTIwOCwiZXhwIjoxNTEzMzQ3NjA4fQ.60OV2dUqiVCFsBalsbPHjnE9sKSS2JNxgirZeWfRN9k"
}

```

### Request
  * Endpoint: : POST: https://postit-app-ralph.herokuapp.com/api/v1/v1/signin
  * Body `(application/json)`

### Response
  * Status: `200: OK`
  * Body `(application/json)`

## Get groups a user belongs to

This endpoint retrieves a list of groups the user belongs to. It requires authentication.

### Response Parameters

Parameter | Description
--------- | -----------
id   | An integer value that represnts the group id
name | The name of the group the user belongs to
createdAt | Time the user record was created in the database.
updatedAt | Last time the user record was modified.

> Sample Response Body

```javascript
[
    {
        "id": 16,
        "name": "man united",
        "createdAt": "2017-12-14T14:37:02.792Z",
        "updatedAt": "2017-12-14T14:37:02.792Z"
    },
    {
        "id": 17,
        "name": "Real Madrid",
        "createdAt": "2017-12-14T14:37:26.754Z",
        "updatedAt": "2017-12-14T14:37:26.754Z"
    },
    {
        "id": 18,
        "name": "Bayern Munich",
        "createdAt": "2017-12-14T14:37:53.875Z",
        "updatedAt": "2017-12-14T14:37:53.875Z"
    }
]

```
### Request
  * Endpoint: : GET: https://postit-app-ralph.herokuapp.com/api/v1/v1/user/7/groups
  * Requires Authentication
  * Body `(application/json)`

### Response
  * Status: `200: OK`
  * Body `(application/json)`

## Search Users 

This endpoint searches for users that have registered on the application. It returns a paginated list of users.
It requires authentication.

### Query Parameters

Parameter | Default  | Description
--------- | ---------| -----------
searchTerm | "" |   search query
group      |    | omit users from this group
limit      | 10 |  sets the limit
offset     | 0  | sets the offset

> Sample Response Body

```javascript
{
    "users": [
        {
            "id": 6,
            "email": "raphaelumoh@yahoo.com",
            "username": "raphaelumoh",
            "createdAt": "2017-12-11T15:35:19.468Z",
            "updatedAt": "2017-12-11T15:41:48.047Z"
        },
        {
            "id": 1,
            "email": "raphaelumoh@gmail.com",
            "username": "raphael",
            "createdAt": "2017-11-30T10:59:47.473Z",
            "updatedAt": "2017-11-30T10:59:47.473Z"
        }
    ],
    "pagination": {
        "page": 1,
        "pageCount": 1,
        "pageSize": 2,
        "totalCount": 2
    }
}

```
### Request
  * Endpoint: : GET: https://postit-app-ralph.herokuapp.com/api/v1/v1/search/users?searchTerm=a&group=16&limit=2&offset=0
  * Requires Authentication
  * Body `(application/json)`

### Response
  * Status: `200: OK`
  * Body `(application/json)`

## Forgot Password

This endpoint sends user's email containing the link to help them reset their password.

Parameter | Description
--------- |-----------
email |   User's email address

> Sample Request

```javascript
{
  "email":"johndoe@gmail.com"
}

```

> Sample Response Body

```javascript
{
    "message": "An email has been sent to johndoe@gmail.com with further instructions."
}

```
### Request
  * Endpoint: : PUT: https://postit-app-ralph.herokuapp.com/api/v1/forgotpassword
  * Requires Authentication
  * Body `(application/json)`

### Response
  * Status: `200: OK`
  * Body `(application/json)`


## Reset Password

Users who have gotten a reset email, can change their passwords, using the reset link as authentication. When making requests to this endpoint, simply copy the reset hash sent in the reset mail and attach to the (token) request pararmeter of this endpoint. This reset hash expires after a six hours and can only be used once.

Parameter | Description
--------- |-----------
password |   User's password

> Sample Request

```javascript
{
  "password":"updatedpassword"
}

```

> Sample Response Body

```javascript
{
    "message": "Password Reset Successful"
}

```
### Request
  * Endpoint: : PUT: http://postit-app-ralph.herokuapp.com/#/resetpassword/jAiifzghGcPH72i8kfFAByusDNe84hpXY0uoQbb9aGwCH3foIC 
  * Requires Authentication
  * Body `(application/json)`

### Response
  * Status: `200: OK`
  * Body `(application/json)`
