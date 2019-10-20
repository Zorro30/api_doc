# API reference index

Below are the operation that can be performed.
- [Authentication](#authentication) 
- [Creating Admin](#creating-admin)
- [Creating User](#Creating-User) 
- [Generating Token](#Generating-Token)
- [Promoting User](#Promoting-User)
- [Search for a movie](#Search-for-a-movie)
- [Add to wishlist](#Add-to-wishlist)
- [Remove from wishlist](#remove-from-wishlist)
- [Get Watchlist](#get-watchlist)

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
curl -X POST https://imdb-flaskapi.herokuapp.com/create_superuser -H 'authorization: Basic Z2F1cmFuZzpnYXVyYW5n' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: 6a5bedea-e030-ab64-ae23-8ea1dfaf0b03' -d '{"name":"name","password":"password"}'
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

This API helps to create User, anyone can create a user with user access to add and remove movies from watch list. And also to search movies across the database.

```bash
POST /user
```

```bash
curl -X POST https://imdb-flaskapi.herokuapp.com/user -H 'authorization: Basic Z2F1cmFuZzpnYXVyYW5n' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: 9170dacf-8637-d14d-9f64-748069884be8' -d '{"name":"name",
 "password":"password"
}'
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
    "message": "New user created with User access, Only Admin can make an Admin!"
}
```

## Generating Token
This API helps in generating a token which is valid for 4 hours for each user and Admin. 

```bash
GET /login
```

```bash
curl -X GET https://imdb-flaskapi.herokuapp.com/login -H 'authorization: Basic Z2F1cmFuZzpnYXVyYW5n' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: 68a79d5a-4b58-6566-898f-a6e25faa1043' -d '{"name":"name",
 "password":"password"
}'
```

### Response
```bash
Status: 200 OK
{
    "token": "sample-token"
}
```

## Promoting-User
This API helps an admin to promote a user to admin giving him access to add, delete and update movies in Database. Only an admin can access this API.

```bash
PUT /user/<id>
```

```bash
curl -X PUT https://imdb-flaskapi.herokuapp.com/user/<id> -H 'authorization: Basic R2F1cmFuZzpwYXNzd29yZA==' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: c851431c-128b-a97f-8ea8-fd7894a798c7' -H 'x-access-token: admin-access-token' -d '{"name":"admin username",
 "password":"admin password"
}'
```
`<id>` passed above is the ID of the user, that Admin wants to upgrade.

### Response
```bash
Status: 200 OK
{
    "message": "The user has been promoted!"
}
```


## Search for a movie
This API helps in searching for a specific movie. It also assists in searching for a movie starting with specific letter and lists down all the movies starting with the letter. This API is accessible to anyone using it.

```bash
GET /moviesearch/<tag>
```

```bash
curl -X GET https://imdb-flaskapi.herokuapp.com/moviesearch/<tag> -H 'authorization: Basic R2F1cmFuZzpwYXNzd29yZA==' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: 8a012abb-30f6-86b8-ca70-8c10bc61d2bd' 
```

### Response
```bash
Status: 200 OK
[
    {
        "id": 3,
        "name": "Cabiria"
    },
    {
        "id": 8,
        "name": "Casablanca"
    },
    {
        "id": 27,
        "name": "Rosemarys Baby"
    },
    {
        "id": 98,
        "name": "Lawrence of Arabia"
    }
]
```

## Add to Wishlist
This API helps to add movies to wishlist. This API can only be accessed by authenticated users and Admin.

```bash
POST /watchlist
```

```bash
curl -X POST https://imdb-flaskapi.herokuapp.com/watchlist -H 'authorization: Basic R2F1cmFuZzpwYXNzd29yZA==' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: b5f83ec3-14d7-da41-288e-8464901e7eda' -H 'x-access-token: your-access-token' -d '{"movie_id":"1"}'
```
### Payload

| Parameter       | Description                         |
|-----------------|-------------------------------------|
| movie_id        | id that is accosiated with the movie, which you want to add to watchlist|


### Response
```bash
Status: 200 OK
{
    "message": "Movie added to wishlist!"
}
```

## Remove from Wishlist
This API helps in removing movie from Wishlist. This API can only be accessed by authenticated users and Admin.

```bash
DELETE /watchlist/<movie_id>
```

```bash
curl -X DELETE https://imdb-flaskapi.herokuapp.com/watchlist/<movie_id> -H 'authorization: Basic R2F1cmFuZzpwYXNzd29yZA==' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: c2fa1f30-d3a7-028d-f15a-5cafbcb96555' -H 'x-access-token: your-access-token' -d '{"movie_id":"1"}'
```

### Payload

| Parameter       | Description                         |
|-----------------|-------------------------------------|
| movie_id        | id that is accosiated with the movie, which you want to delete from watchlist|


### Response
```bash
Status: 200 OK
{
    "message": "Movie removed from watchlist!"
}
```

## Get Watchlist
This API gets all the movies in the watchlist for a particular user.

```bash
GET /watchlist
```

```bash
curl -X GET https://imdb-flaskapi.herokuapp.com/watchlist -H 'authorization: Basic R3A6cGFzc3dvcmQ=' -H 'cache-control: no-cache' -H 'content-type: application/json' -H 'postman-token: 0db49245-308f-270a-6fc8-00c2db3d15ee' -H 'x-access-token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6MywiZXhwIjoxNTcxNTkzOTQ4fQ.K_oMvq8gnPUBhRd1jSd7Zy4p2-qVXwfjw_6GtYV0Goc'
```

### Response
```bash
Status: 200 OK
{
    "message": [
        {
            "99popularity": 83,
            "director": "Victor Fleming",
            "genre": [
                "Adventure",
                " Family",
                " Fantasy",
                " Musical"
            ],
            "id": 1,
            "imdb_score": 8.3,
            "name": "The Wizard of Oz"
        },
        {
            "99popularity": 85,
            "director": "David Lean",
            "genre": [
                "Adventure",
                " Biography",
                " Drama",
                " History",
                " War"
            ],
            "id": 98,
            "imdb_score": 8.5,
            "name": "Lawrence of Arabia"
        }
    ]
}
'''



