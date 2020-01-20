---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  
toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Hush API! You can use our API to access Hush API endpoints, which can get information on around live radio streams, catch up clips and podcasts.

# Authentication

Hush expects the session token to be included in most API requests to the server in an Authorization header that looks like the following:

`Authorization: token`

<aside class="notice">
You must replace "token" with your own token.
</aside>

# Login and registration

## New user registration

```shell
curl "http://example.com/api/auth/registration"
  -X POST 
  -d "name=<name>&email=<mail_address>&password=<password>" 
```
> The above command returns JSON structured like this:

```json
{
  "id_token": "<id_token>",
  "session_token": "<session_token>"
}
```

This endpoint registers a new user.

### HTTP Request

`POST http://example.com/api/auth/registration`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
Name | '' | A required field representing the users name.
Email | '' | A required field representing the users email.
Password | '' | A required field to secure the users account.
Device Info | {} | Information about the users device for analytics purposes.

## Existing user login

```shell
curl "http://example.com/api/auth/login"
  -X POST 
  -d "email=<mail_address>&password=<password>" 
```
> The above command returns JSON structured like this:

```json
{
  "id_token": "<id_token>",
  "session_token": "<session_token>"
}
```

This endpoint logs in an existing user.

### HTTP Request

`POST http://example.com/api/auth/login`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
Username | '' | A required field representing the users username (an email address).
Password | '' | A required field representing the users password.
Device Info | {} | Information about the users device for analytics purposes.

<aside class="success">
Remember — an authenticated user is a happy user!
</aside>

## Preferences

```shell
curl "http://example.com/api/preferences/type/music"
  -X GET 
```
> The above command returns JSON structured like this:

```json
  [{"id":1,"type":2,"title":"Pop"},
  {"id":2,"type":2,"title":"Party"},
  {"id":3,"type":2,"title":"Soul"},
  {"id":4,"type":2,"title":"80s"},
  {"id":5,"type":2,"title":"African"},
  {"id":6,"type":2,"title":"Blues"}]
```

This endpoint returns a list of preferences the user can choose from.

### HTTP Request

`GET http://example.com/api/preferences/type/music` OR 
`GET http://example.com/api/preferences/type/podcast`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
Type | All | A field representing what type of preferences should be returned. 

<aside class="success">
Is a secure call</aside>

