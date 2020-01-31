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

Hush expects the id token to be included in most API requests to the server in an Authorization header that looks like the following:

`Authorization: Bearer token`

<aside class="notice">
You must replace "token" with the token received from Firebase authentication.
</aside>

# Preferences

## Music and podcast preferences

```shell
curl "http://example.com/api/preference"
  -X GET 
```
> The above API call returns a list of all preferences in a JSON object like this:

```json
  [{"id":1,"type":1,"title":"News"},
  {"id":2,"type":1,"title":"Sport"},
  {"id":3,"type":2,"title":"Soul"},
  {"id":4,"type":2,"title":"80s"},
  {"id":5,"type":2,"title":"African"},
  {"id":6,"type":2,"title":"Blues"}]
```

```shell
curl "http://example.com/api/preference/type/music"
  -X GET 
```
> The above API call returns a list of music preferences in a JSON object like this:

```json
  [{"id":1,"type":2,"title":"Pop"},
  {"id":2,"type":2,"title":"Party"},
  {"id":3,"type":2,"title":"Soul"},
  {"id":4,"type":2,"title":"80s"},
  {"id":5,"type":2,"title":"African"},
  {"id":6,"type":2,"title":"Blues"}]
```

The preference end point returns all preferences, both music and podcast. Additionally, the endpoint that specifies a type returns a specific list of preferences that are either music or podcast.

### HTTP Request

`GET http://example.com/api/preferences` OR 
`GET http://example.com/api/preferences/type/music` OR 
`GET http://example.com/api/preferences/type/podcast`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
type | music | A field representing what type of preferences should be returned. 

<aside class="success">
The user does NOT have to be authenicated to make this call
</aside>

# Login and registration

## New user registration

```shell
curl "http://example.com/api/user/save"
  -X POST 
  -H "Authorization: Bearer <token>"
  -d "auth_id=<uuid_from_firebase>"
  -d "name=<name>"
  -d "email=<mail_address>"
  -d "password=<password>" 
  -d "preferences= {
    music: [23, 24, 34, 5],
    podcast: [3, 4, 9, 33]
  }"
```
> If successfully registered:
```
Http Ok 200 with a response of true
```

> If registration failed because of an invalid user model:
```
Bad request 400 with a response of false
```

> If registration failed because of an invalid or expired token:
```
Unauthorized 401
```

This endpoint registers a new user.

### HTTP Request

`POST http://example.com/api/user/save`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
auth_id | '' | A required field representing the users firebase uuid
name | '' | A required field representing the users name
email | '' | A required field representing the users email
password | '' | A required field to secure the users account
preferences | { music: [], podcast: []} | A required field of at least two int id's in each array
device_info | {} | Information about the users device for analytics purposes

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

# Home content

## Intro

The home call occurs after a user has successfully registered both on firebase and in the hush database, or if the user is successfully logged in.

One call is made to the api, and the full response can be seen at "https://hush.primedia.co.za/Home/response.clean.json. Each section is discussed below

## Trending

## Recent

## OnAir

## Radio

## Podcasts

## CatchUp

## Music