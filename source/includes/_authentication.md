# Authentication

## Login

> Your request:

```javascript
const response = await axios.post('/auth/login', {
    email: 'youremail@gmail.com',
    password: 'y0urPassw0rd'
});
```

> The above request returns JSON structured like this:

```json
{
  "accessToken": "yourAccessToken",
  "refreshToken": "yourRefreshToken",
  "user": {
    "id": 3,
    "email": "youremail@gmail.com",
    "created_at": "2020-02-02 11:22:334",
    "first_name": "John",
    "last_name": "Johnson",
    "user_role": {
      "id": 2,
      "name": "ADMIN"
    }
  }
}
```

WFC uses an access/refresh token based authentication flow. First login using email/password credentials to receive your
first set of tokens



### HTTP Request

`POST /auth/login`

### Query Body

Prop | Required | Type | Description
--------- | -------- | ---- | ---------
email | true | string | Email address used to register account
password | true | string | Password used to register account

<aside class="notice">
Save your refresh_token somewhere to avoid having to login with credentials in future
</aside>

## Requesting access tokens

> Your request:

```javascript
const refreshToken = getTokenFromStorage();

const response = await axios.get('/auth/access-token', {
  Authorization: `Bearer ${refreshToken}`
});
```

> The above request returns JSON structured like this:

```json
{
  "accessToken": "yourAccessToken"
}
```
To get your latest access token, you need to make a request to the endpoint below, including the refresh token in your
Authorization header.
Each access token will expire within an hour.


### HTTP Request

`GET /auth/access-token`


## Revoking refresh tokens

> Your request:

```javascript
const refreshToken = getTokenFromStorage();

const response = await axios.post('/auth/revoke-token', {}, {
  Authorization: `Bearer ${refreshToken}`
});
```

> If successful, you'll receive a status 200 OK


By default, refresh tokens take a year to expire - so your user can stay 'logged in' for a long time without having to
fill in their credentials. If they want to log out of a device, you can revoke the refresh token by calling this
endpoint, with the token you want to revoke in the Authorization header.


### HTTP Request

`POST /auth/revoke-token`
