# Groups
Communications in PostIt takes place in groups. 
<aside class="notice">All group routes are protected, and so require authentication. You must set the x-auth token in the header to access them</aside>

## Create Groups
A registered user can create a new group with this endpoint

### Request Parameters

Parameter  | Description
---------- | ------------
name       | required


### Response Parameters

Parameter | Description
--------- | -----------
message   | A descriptive notification of the outcome of the request
group     | An object that contains the id, name, createdAt and UpdatedAt properties for the group


> Sample Request

```javascript
{
  "name":"man united",

}

```

> Sample Response Body

```javascript
{
  "message": "Group Created Successfully",
  "group": {
    "id": 1,
    "name": "Man United",
    "updatedAt": "2017-12-14T16:54:09.951Z",
    "createdAt": "2017-12-14T16:54:09.951Z"
  }
}
```

### Request
  * Endpoint: : POST: https://postit-app-ralph.herokuapp.com/api/group
  * Body `(application/json)`

### Response
  * Status: `201: Created`
  * Body `(application/json)`


## Add User to Groups

Registered Users can be added to groups

### Request Parameters

Parameter  | Description
---------- | ------------
userId     | required


### Response Parameters

Parameter | Description
--------- | -----------
message   | A descriptive notification of the outcome of the request


> Sample Request

```javascript
{
  "userId": 1
}

```

> Sample Response Body

```javascript
{
  "message": "User Added Successfully"
}
```

### Request
  * Endpoint: : POST: https://postit-app-ralph.herokuapp.com/api/group/16/user
  * Body `(application/json)`

### Response
  * Status: `201: Created`
  * Body `(application/json)`


## Get Group Users

We can retrieve a list of all users belonging to a particular group

### Request Parameters

Parameter  | Description
---------- | ------------
userId     | required

> Sample Request

```javascript
{
  "userId": 1
}

```

> Sample Response Body

```javascript
[
    {
        "id": 7,
        "email": "oleoleole@gmail.com",
        "username": "oleoleole",
        "createdAt": "2017-12-14T12:34:59.991Z",
        "updatedAt": "2017-12-14T12:34:59.991Z"
    },
    {
        "id": 1,
        "email": "raphaelumoh@gmail.com",
        "username": "raphael",
        "createdAt": "2017-11-30T10:59:47.473Z",
        "updatedAt": "2017-12-14T16:03:02.432Z"
    }
]
```

### Request
  * Endpoint: : POST: https://postit-app-ralph.herokuapp.com/api/group/16/users
  * Body `(application/json)`

### Response
  * Status: `200: OK`
  * Body `(application/json)`


## Add User to Groups

Registered Users can be added to groups

### Request Parameters

Parameter  | Description
---------- | ------------
userId     | required


### Response Parameters

Parameter | Description
--------- | -----------
message   | A descriptive notification of the outcome of the request


> Sample Request

```javascript
{
  "userId": 1
}

```

> Sample Response Body

```javascript
{
  "message": "User Added Successfully"
}
```

### Request
  * Endpoint: : POST: https://postit-app-ralph.herokuapp.com/api/group/16/user
  * Body `(application/json)`

### Response
  * Status: `201: Created`
  * Body `(application/json)`


## Post Message 

We can post a message to a particular group

### Request Parameters

Parameter  | Description
---------- | ------------
content    | required
priority   | required

> Sample Request

```javascript
{
  "content": "Hello Africa",
  "priority", "Normal"
}

```

> Sample Response Body

```javascript
{
    "message": {
        "id": 10,
        "senderId": 7,
        "content": "Hello Africa",
        "priority": "Normal",
        "groupId": 16,
        "updatedAt": "2017-12-15T09:32:22.422Z",
        "createdAt": "2017-12-15T09:32:22.422Z",
        "User": {
            "username": "oleoleole"
        }
    }
}
```

### Request
  * Endpoint: : POST: https://postit-app-ralph.herokuapp.com/api/group/16/message
  * Body `(application/json)`

### Response
  * Status: `201: Created`
  * Body `(application/json)`


## Get Messages 

We can retrieve a list of messages that has been posted to a group.


> Sample Response Body

```javascript
[
    {
        "id": 10,
        "content": "Hello Africa",
        "priority": "Normal",
        "groupId": 16,
        "senderId": 7,
        "createdAt": "2017-12-15T09:32:22.422Z",
        "updatedAt": "2017-12-15T09:32:22.422Z",
        "User": {
            "username": "oleoleole"
        }
    },
    {
        "id": 11,
        "content": "Hello Africa",
        "priority": "Urgent",
        "groupId": 16,
        "senderId": 7,
        "createdAt": "2017-12-15T09:34:27.871Z",
        "updatedAt": "2017-12-15T09:34:27.871Z",
        "User": {
            "username": "oleoleole"
        }
    }
]
```

### Request
  * Endpoint: : POST: https://postit-app-ralph.herokuapp.com/api/group/16/messages
  * Body `(application/json)`
  * Requires Authentication

### Response
  * Status: `200: OK`
  * Body `(application/json)`