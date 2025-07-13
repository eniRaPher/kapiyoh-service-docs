---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Kapiyoh Service API is a modern RESTful API designed to empower developers and businesses to seamlessly integrate with the Kapiyoh ecosystem.

Our API provides secure, flexible, and easy-to-use endpoints for managing resources, authenticating users, and building scalable applications.

Whether you're creating internal tools, mobile apps, or third-party integrations, Kapiyoh Service API helps you ship features faster and maintain a robust service backbone.

# Authentication
Kapiyoh Service API uses Session + Cookie Authentication to manage secure access to protected resources.

# How it Works

```shell
curl -i -c cookies.txt \
  -X POST https://api.kapiyoh.com/sign_in \
  -H "Content-Type: application/json" \
  -d '{
    "username": "johndoe",
    "password": "secret"
  }'
```

1️⃣ Sign In
Clients authenticate by sending valid login credentials (e.g. username & password) to the /sign_in endpoint.
If authentication is successful, the server creates a session and sets a secure HTTP cookie (_kapiyoh_session) in the response.

2️⃣ Session Cookie
On subsequent requests, the client must include the session cookie (_kapiyoh_session) automatically (your HTTP client or browser does this by default).
The server verifies this cookie to identify the user and authorize the request.

3️⃣ Sign Out
Clients can invalidate the session by calling the /sign_out endpoint.
This clears the session on the server and removes the cookie.

# Admins

## Get All Admins
This endpoint retrieves all Admins.

### HTTP Request
This feature is not supported.

### Query Parameters
This feature is not supported.

## Register
```shell
curl --location 'http://example.com/admins' \
--header 'Content-Type: application/json' \
--data '{
  "admin": {
    "username": "username",
    "password": "supersecret",
    "password_confirmation": "supersecret",
    "first_name": "first name",
    "last_name: "last name",
    "phone": "0988888888",
    "address": "48 bkk thailand"
  }
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": 1,
    "first_name": "first name",
    "last_name": "last name",
    "username": "username",
    "phone": "0988888888",
    "address": "48 bkk thailand"
}
```

This endpoint register Admin.

### HTTP Request

`POST http://example.com/admins`

### Query Parameters

Parameter | Require | Description
--------- | ------- | -----------
username | true | Must be uniq
password | true | Password
password_confirmation | true | The password confirmation must match the password.
first_name | true | First name
last_name | true | Last name
phone | false | Phone
address | false | Address

## Sign in
```shell
curl --location 'http://localhost:3000/admins/sign_in' \
--header 'Content-Type: application/json' \
--data '{
    "admin": {
        "username": "s3",
        "password": "supersecret3"
    }
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": 1,
    "first_name": "first name",
    "last_name": "last name",
    "username": "username",
    "phone": "0988888888",
    "address": "48 bkk thailand"
}
```

This endpoint for Admin Sign in.

### HTTP Request

`POST http://example.com/admins/sign_in`

### Query Parameters

Parameter | Require | Description
--------- | ------- | -----------
username | true | Must be uniq
password | true | Password

## Sign out
```shell
curl --location --request DELETE 'http://localhost:3000/admins/sign_out' \
--header 'Cookie: _kapiyoh_session=kapiyoh_session_dd; _session_id=session_id_ddd'
```

This endpoint for Admin Sign in.

### HTTP Request
`DELETE http://example.com/admins/sign_out`

### Query Parameters
NO


<!-- # Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
 -->
