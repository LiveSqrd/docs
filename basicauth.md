[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)

#Basic Authentication

logging in with email and password

##How to enable it
in config under api add 
```json

 "password"	: {
  	"name" 	: "password"
	,"login": true
}
	
```
##End Points
* POST     /auth/register
* POST     /auth/login
* GET/POST /auth/logout 
* POST     /auth/password
* POST     /auth/forgot

```
 HEADERS:
 Content-Type: application/json
```

##Register
Is a regular post request with params:
* login (The users email)
* password (min 8 chars)
* firstName (optional)
* lastName (optional)
* gender (m/f/o, optional)
* birthday (mm/dd/yy, optional)
* app (true/false, default is false, optional)
* ANY (any other param added will be saved in the client data object, that can be access later on)
```javascript
{
	"login":"email@example.com",
	"password": "12345678",
	"firstName": "John", //optional
	"lastName": "Smith", //optional
	"gender": "m", //optional "m" "f" "o"
	"birthday": "01/01/1990",  //optional 
	"phoneNumber": "888-999-0000" //optional ** any other field name with be added and accessable
}
```
###Possible errors:
```javascript
{"errors":["emailLogin","noPass"]}
{"errors":["shortPass"]}
{"errors":["exists"]}
{"errors":["already logged in"]}
```
App param will return the object with instance, client, profile info instead of the index page. 

##Login
* login (The users email)
* password (min 8 chars)
* redirect (url,optional)
* app (true/false, defualt is false, optional)
```javascript
{
	"login":"email@example.com",
	"password": "12345678"
}
```

##Password
Changed password must be logged in for it to work
* password (old password)
* newPassword (new password)
```javascript
{
	"password":"12345678",
	"newPassword": "abcdefgh"
}
```
##Forgot 
Will send a email with a new password, both passwords will work till it is changed.
* login (email address)
```javascript
{
	"login":"email@example.com"
}
```

