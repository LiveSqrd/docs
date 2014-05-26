[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)

#Basic Authentication

logging in with email and password

##How to enable it
in config under api add 
```json

 "password"	: {
  		 "name" 	: "password"
			,"login"	: true
	}
	
```
##End Points
* /auth/register
* /auth/login
* /logmeout 


##Register
Is a regular post request with params:
* login (The users email)
* password (min 8 chars)
* firstname (optional)
* lastname (optional)
* gender (m/f/o, optional)
* birthday (mm/dd/yy, optional)
* app (true/false, defualt is false, optional)

App param will return the object with instance, client, profile info instead of the index page. 

##Login
* login (The users email)
* password (min 8 chars)
* app (true/false, defualt is false, optional)



