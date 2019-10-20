# API reference index

Below are the operation that can be performed.
- [Authentication](#authentication) 
- [Creating Admin](#creating-admin)
- [Creating User](#Creating-User) 
- [Generating Token](#Generating-Token)
- [Promoting User](#Promoting-User)
- [Search for a movie](#Search-for-a-movie)
- [Add to wishlist](#Add-to-wishlist)

## General API endpoints.
This can be accessed without any authentication.

|  API                   |  Result                                                      |
|------------------------|--------------------------------------------------------------|
| `GET / HTTP/1.1`       |  Return a list of all the movies in DB                       |
| `GET /<id>  HTTP/1.1`  |  Return a specific movie object with associated information  |

## Authentication
    - There are two levels of access with this api.
    - A user with valid access token can only have access to the account and can exercise features like 
    add to watchlist. An Admin can only create other admin.
    - An admin with valid token can exercise the features like add, delete and update a particular movie.
    - Here I have used "pyjwt" to create tokens that get renewed every 4 hours, hence a user has to generate a token every 4 hours.
    - Also I am not storing direct password in to the DB instead of that I am storing a hashed password, hence even if someone get holds of the DB data no one can decipher it.

## Creating Admin

This API helps to create an Admin, that can then add more admin or promote other users to become admin.
This request won't be exposed to the users.

```bash
POST /create_superuser 
```

```bash
curl -X POST http://127.0.0.1:5000/create_superuser -H 'authorization: Basic Z2F1cmFuZzpnYXVyYW5n' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: 6a5bedea-e030-ab64-ae23-8ea1dfaf0b03' -d '{"name":"name","password":"password"}'
```
### Payload

| Parameter       | Description        |
|-----------------|--------------------|
| name            |Enter the username  |
| password        |Enter the password  |

### Response

```bash
Status: 200 OK
{
    "message": "New Admin created with Admin access!"
}
```

## Creating User
    Example text blah. Example text blah. Example text blah. Example text blah. 
Example text blah. Example text blah. Example text blah. Example text blah. 
Example text blah. Example text blah. Example text blah. Example text blah. 
Example text blah. Example text blah. 

## Generating Token
jdcjshj

## Promoting-User
kjkj

## Search for a movie
