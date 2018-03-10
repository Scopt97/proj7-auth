# Project 7: Authenticated brevet time calculator service. Extension of proj6.

## What?

An api for the brevets calculator database with authorization

## REST Resources

* RESTful services to expose what is stored in MongoDB.
Specifically, the following:

** "http://<host:port>/listAll" should return all open and close times in the database

** "http://<host:port>/listOpenOnly" should return open times only

** "http://<host:port>/listCloseOnly" should return close times only

* Also designed two different representations: one in csv and one 
 in json. For the above, JSON should be your default representation. 

** "http://<host:port>/listAll/csv" should return all open and close times in CSV format

** "http://<host:port>/listOpenOnly/csv" should return open times only in CSV format

** "http://<host:port>/listCloseOnly/csv" should return close times only in CSV format

** "http://<host:port>/listAll/json" should return all open and close times in JSON format

** "http://<host:port>/listOpenOnly/json" should return open times only in JSON format

** "http://<host:port>/listCloseOnly/json" should return close times only in JSON format

* also added a query parameter to get top "k" open and close
times. For examples, see below.

** "http://<host:port>/listOpenOnly/csv?top=3" should return top 3 open times only (in ascending order) in CSV format 

** "http://<host:port>/listOpenOnly/json?top=5" should return top 5 open times only (in ascending order) in JSON format

* also designed consumer program (in php) to expose the services.

## Added Functionality

Add the following functionality:

- POST **/api/register**

    Registers a new user. On success a status code 201 is returned. The body of the response contains
a JSON object with the newly added user. Specifically, `Location` (unique id), `username`, and `hash` (password hash) On failure status code 400 (bad request) is returned. Note: The 
password is hashed before it is stored in the database. Once hashed, the original 
password is discarded. The database has three fields: id (unique index),
username and password. 

- GET **/api/token**

    Returns a token. This request is authenticated using a HTTP Basic
Authentication. On success a JSON object is returned 
with a field `token` set to the authentication token for the user and 
a field `duration` set to the (approximate) number of seconds the token is 
valid. On failure status code 401 (unauthorized) is returned.

- GET **/RESOURCE-FROM-ABOVE**

    Return a protected <resource>, listed above. This request is authenticated using token-based authentication only. HTTP password-based (basic) authentication is not allowed. On success, the requested resource is returned. On failure status code 401 (unauthorized) is returned.

**IMPORTANT** The Server gets the token from the `token` HTTP header.  
/api/register expects a form via POST with fields 'username' and 'password'.  
The default token duration is 30 seconds. 

/api/register/page is an html page to easily register a new user.  
/api/token/page is intended for debugging and only sends username/password as args, rather than through basic auth.

## credentials.ini

credentials.ini should go in the Auth/app/ folder, and it should have values SECRET_KEY and PORT under \[DEFAULT\]

## Use

cd into Auth/ and run `sudo docker compose up` to start the server

* api (auth and resources) is on port 5001
* app (calculate brevets and store them in the database) is on port 5002. It should be noted that, since the calculator is standalone, it does not have the auth features of the api
* consumer is on port 5000. The consumer is unchanged from proj6 and may not work with the auth for the api.


### Author: Kyle Nielsen  Contact: kylen@uoregon.edu
