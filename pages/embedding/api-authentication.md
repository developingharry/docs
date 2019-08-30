---
title: API Authentication
sidebar: cyclr_sidebar
permalink: cyclr-api-authentication
tags: [embedding]
---

Cyclr API authentication is provided using [OAuth2](https://oauth.net/2/).

OAuth access tokens are granted to either manage the partner level, or access and modify a partner account.

### Get access token

To get an access token from Cyclr you call the "/token" endpoint with different details, depending on where you wish to work.

**To receive a Partner access token**
Provide the email address and password you use to access your Cyclr Partner Console.

**To receive an Account access token**
Provide the username and password of an account user.

#### Request

**Partner access token**

```http
POST https://yourCyclrInstance/oauth/token
Content-Type: application/x-www-form-urlencoded

client_id={ClientID}&grant_type=password&username={username}&password={password}
```

**Account access token**

```http
POST https://yourCyclrInstance/oauth/token
Content-Type: application/x-www-form-urlencoded

client_id={ClientID}&client_secret={AccountID}&grant_type=password&username={username}&password={password}
```

- **yourCyclrInstance** – your Cyclr instance URL. This could be one of the following: *api.cyclr.com* if your Cyclr account is hosted on our US instance; *api.cyclr.uk* if it's on our UK instance; your own domain if your Cyclr instance is self-hosted.
- **client_id** – the client ID of the Partner. This can be found in the Cyclr Console.
- **client_secret** –  
    _(Optional)_ the ID of the account this token is for
- **grant_type** – the Cyclr Partner API only supports the **password** grant\_type
- **username** – the username of the authenticating user
- **password** – the password of the user

#### Response

```json
{
    "access_token": "************",
    "token_type": "bearer",
    "expires_in": 1209599,
    "refresh_token": "************",
    "userName": "************",
    "clientId": "************",
    ".issued": "Thu, 24 Nov 2016 16:32:59 GMT",
    ".expires": "Thu, 08 Dec 2016 16:32:59 GMT"
}
```

- **access_token** – the token to use when making requests to the Cyclr API
- **expires_in** – the amount of time in seconds until access_token will expire
- **refresh_token** – the token that can be used to generate a new access token without needing to provide username and  
    password details.    See *Refresh access token* below.

### Refresh access token

To obtain a new access token - before or after it has expired - you call the OAuth "/token" endpoint with a **grant_type** of **refresh_token** and pass the refresh token that was included with the current access token. Once used, the old access and refresh tokens will no longer be valid.

```http
POST https://yourCyclrInstance/oauth/token
Content-Type: application/x-www-form-urlencoded

client_id={ClientID}&grant_type=refresh_token&refresh_token={RefreshToken}
```

Refresh tokens from Cyclr's API don't expire so you can keep them until you need to obtain a new access token.

### Calling an API method

To authenticate your requests you need to include the access token in the Authorization HTTP header.

```http
Authorization: Bearer {AccessToken}
```

[View Cyclr’s API Endpoints](./cyclr-api-endpoints)
