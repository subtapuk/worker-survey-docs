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
