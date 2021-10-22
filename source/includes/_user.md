# User

## Register a user

> Your request:

```javascript
const response = await axios.post('/user', {
  email: 'user@gmail.com',
  password: 'y0urPassw0rd',
  first_name: "Henry",
  last_name: 'Henryson',
  user_role: 'USER'
});
```

> The above request returns JSON structured like this:

```json
{
  "id": 1,
  "email": "user@gmail.com",
  "first_name": "Henry",
  "last_name": "Henryson",
  "user_role": {
    "id": 1,
    "name": "USER"
  }
}
```

### HTTP Request

`POST /user`

### Query Body

Prop | Required | Type | Description
--------- | -------- | ---- | ---------
email | true | string |
password | true | string | A password with minimum 8 characters
first_name | true | string |
last_name | true | string |
user_role | false | enum("USER","ADMIN","SUPER") | Defaults to USER

<aside class="notice">
Only an admin with a SUPER role has the permission to create ADMIN or SUPER users
</aside>

## Get all users

> Your request:

```javascript
const refreshToken = getRefreshToken();

const response = await axios.get('/user', {
  Authorization: `Bearer ${refreshToken}`
});
```

> The above request returns JSON structured like this:

```json
{
  "page": 1,
  "totalPages": 2,
  "totalResults": 20,
  "results": [
    {
      "id": 1,
      "email": "user@gmail.com",
      "first_name": "Henry",
      "last_name": "Henryson",
      "user_role": {
        "id": 1,
        "name": "USER"
      }
    }
  ]
}
```

### HTTP Request

`GET /user`

### Query Parameters

Parameter | Required | Description
--------- | -------- | ---- 
page      | false | page number, starting from 0 (defaults to 0)
limit | false | number of records desired per page in response (defaults to 20)

<aside class="warning">
This is a protected route - please provide an access token with your request
</aside>

## Get single user

> Your request:

```javascript
const refreshToken = getRefreshToken();

const response = await axios.get('/user/22', {
  Authorization: `Bearer ${refreshToken}`
});
```

> The above request returns JSON structured like this:

```json
{
  "id": 22,
  "email": "user@gmail.com",
  "first_name": "Henry",
  "last_name": "Henryson",
  "user_role": {
    "id": 1,
    "name": "USER"
  }
}
```

### HTTP Request

`GET /user/:id`

<aside class="warning">
This is a protected route - please provide an access token with your request
</aside>

## Update user

> Your request:

```javascript
const refreshToken = getRefreshToken();

const response = await axios.patch('/user/22',
  {
    first_name: 'NewFirstName',
    email: 'newEmail@email.com'
  },
  {
    Authorization: `Bearer ${refreshToken}`
  });
```

> The above request returns JSON structured like this:

```json
{
  "id": 22,
  "email": "newEmail@email.com",
  "first_name": "NewFirstName",
  "last_name": "Henryson",
  "user_role": {
    "id": 1,
    "name": "USER"
  }
}
```

To update any detail on your user, you must have ADMIN or SUPER permission, or be logged in as that user. Only admins
with SUPER permission are allowed to change user_role status

### HTTP Request

`PATCH /user/:id`

<aside class="warning">
This is a protected route - please provide an access token with your request
</aside>

## Delete user

> Your request:

```javascript
const refreshToken = getRefreshToken();

const response = await axios.delete('/user/22',
  {
    Authorization: `Bearer ${refreshToken}`
  });
```

> The above request returns a status 200 

To delete your user, you must have ADMIN or SUPER permission, or be logged in as that user. Admins with SUPER permission 
cannot be deleted without sending james@subtap.co.uk a grovelling email.

### HTTP Request

`PATCH /user/:id`

<aside class="warning">
This is a protected route - please provide an access token with your request
</aside>
