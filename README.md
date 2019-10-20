# API reference index

Below are the operation that can be performed.
- [Authentication](#authentication) 
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
    - Here I have used pyjwt to create tokens that get renewevery 4 hours, hence a user has to generate a token every 4 hours.

Example text blah. Example text blah. Example text blah. Example text blah. 
Example text blah. Example text blah. Example text blah. Example text blah. 
Example text blah. Example text blah.

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
