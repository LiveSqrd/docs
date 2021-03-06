[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)

#Collections:
* [item](#item)
* [instance](#instance)
* [client](#client)
* [profile](#profile)
* [role](#role)
* [loader](#loader)
* [level](#level)
* [grid](#grid)
* [blob](#blob)
* [event](#event)
* [media](#media)
* [command](#command)
* [report](#report)

**[custom](#custom)**

[^](#collections)

Schemas
========================

##Item
```json

	"item": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"path": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},
		"title": {
			"type": "String",
			"default": ""
		},
		"photo": {
			"type": "String"
		},
		"body": {
			"type": "Schema.Types.Mixed"
		},
		"group": {
			"type": "String",
			"default": "",
			"lowercase": true,
			"trim": true
		},
		"role":{
			"type": "Schema.Types.ObjectId",
			"ref": "role"
		},
		"media": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "media"
				},
				"group":"String",
				"extra":"Schema.Types.Mixed"
			}
		],
		"permission": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "profile"
				},
				"role": {
					"type": "Schema.Types.ObjectId",
					"ref": "role"
				},
				"extra":"Schema.Types.Mixed"
			}
		],
		"item": {
			"type": "Schema.Types.ObjectId",
			"ref": "item"
		},
		"lock": {
			"type": "Schema.Types.Mixed"
		},
		"date": {
			"type": "Date"
		},
		"publish":{
			"type": "Boolean"
		},
		"box":{
			"type": "Schema.Types.Mixed", 
			"index": "2d",
			 "sparse": true 
		},
		"geo": { 
			"type": "Schema.Types.Mixed", 
			"index": "2dsphere",
			 "sparse": true 
		},
		"tags":{"type":"[String]"}
	}
```
[^](#collections)

## Instance
* Short life span, public user client identification information
* Created and destroyed with Socket.io events
* Output
```json
	"instance": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"body": {
			"type": "Schema.Types.Mixed"		
		},
		"group":{
			"type": "String"
		},
		"device": {
			"type": "String"
		},
		"browser": {
			"type": "String"
		},
		"touch":{
			"type": "Boolean"
		},
		"version": {
			"type": "String"
		},
		"deviceType": {
			"type": "String"
		},
		"os": {
			"type": "String"
		},
		"osVersion": {
			"type": "String"
		},
		"width": {
			"type": "Number",
			"default": 1024
		},
		"height": {
			"type": "Number",
			"default": 768
		},
		"client": {
			"type": "Schema.Types.ObjectId",
			"ref": "client"
		},
		"profile": {
			"type": "Schema.Types.ObjectId",
			"ref": "profile"
		},
		"page": {
			"type": "String"
		},
		"layout": {
			"type": "String"
		},
		"media": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "media"
				},
				"group":"String",
				"extra":"Schema.Types.Mixed"
			}
		],
		"date": {
			"type": "Date",
			"expires": "24h"
		}
	}
```
* Example Usage

```json

    {
        "touch": false,
        "date": "2013-07-12T20:11:13.598Z",
        "os": "Mac OS X",
        "osVersion": "10.8.4",
        "browser": "Chrome",
        "version": "27.0.1453.116",
        "device": "Desktop",
        "deviceType": "pc",
        "client": "51def86fe7ae632a2b0000b8",
        "profile": "41aef86fa4ae62fa2b0000a8",
        "page": "projects",
        "_id": "51e062e1178e53e46500000e",            
        "height": 1079,
        "width": 1049
    }
```
* Save custom terms, etc, in the states ObjectId

```json
    "states": {
		"type": "Schema.Types.Mixed"		
	}
```
* Ex: save number of clicks user makes, and number of no results are served

```json
    "states": {
		"click_counter": 1,
		"noresults": 11
	}
```
[^](#collections)

##Client
* Session based storage and identification, used for user login, credentials, and other pertaining parameters
* Session based entails anonymous and profile attached logins. Unlike [Instances](#instance) they have a long life span: 30 days (subject to change)

* Output

```json
	"client": {
		"title":{
				"type": "String"
			},
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"body": {
			"type": "Schema.Types.Mixed"
		},
		"path": {
			"type": "String",
			"trim": true,
			"unique":true,
			"required":true
		},
		"ip": 
			{
				"type": "[String]"
			}
		,
		"device":[
			{	
				 "name": "String"
				,"nick": "String" 
				,"primary": { "type":"Boolean", "default": false}
				,"id": "String"
				,"data": {
					"type": "Schema.Types.Mixed"
				}
				,"date": {
					"type":"Date"
					,"default": "Date.now"
				}

			}
		],
		"login": [
			{
				"name": {
					"type": "String"
				},
				"id": {
					"type": "String"
				},
				"data": {
					"type": "Schema.Types.Mixed"
				}
				,"date": {
					"type":"Date"
					,"default": "Date.now"
				}
			}
		],
		"email": {
			"type": "String",
			"lowercase": true,
			"trim": true,
			"unique": true
		},
		"v": [
			{
				"name": {
					"type": "String"
				},
				"v": {
					"type": "Boolean",
					"required": true,
					"default": false
				}
			}
		],
		"page": {
			"type": "String"
		},
		"date": {
			"type": "Date",
			"default": "Date.now"
		},

		"lang": {
			"type": "String",
			"default": "en"
		},
		"a": {
			"type": "String",
			"required": true,
			"unique": true
		},
		"birthday": {
			"type": "Date"
		},
		"timezone":{
			"type":"Number"
		},
		"gender": {
			"type": "String"
		},
		"photo": {
			"type": "String"
		},
		"profile": {
			"type": "Schema.Types.ObjectId",
			"ref": "profile"
		},
		"ver": {
			"type": "Boolean",
			"default": false
		},
		"media": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "media"
				},
				"base":"String",
				"group":"String",
				"extra":{"type":"Schema.Types.Mixed"}
			}
		],
		"event": 
			{
				"type": "[Schema.Types.ObjectId]",
				"ref": "event"
			},
		"expire": {
			"type": "Date",
			"default": "Date.now",
			"expires": "4d"
		}
	}
```
* Example Usage

```json
	{            
	    "_id": "51e06df7a3cd97400c000001",
	    "a": "uebkjvhg9uwdBBdBflJ1zvej",
	    "date": "2013-07-12T20:58:31.585Z",
	    "email": "user@example.com",
	    "gender": "m",
	    "page": "login",
	    "path": "uebkjvhg9uwdbbdbflj1zvej",
	    "profile": "41aef86fa4ae62fa2b0000a8",
	    "photo": "",
	    "states": {},
	    "timezone": 0,
	    "event": [],
	    "ver": false,
	    "lang": "en",
	    "v": [],
	    "login": [],
	    "ip": [
	        "165.254.85.1"
	    ]
    }
```
* ver is for verification of a user via email: boolean
* a is the session token: auto generated string
* login is the array of oAuth credentials and there tokens for later access: can be multiple, e.g., Facebook, twitter, Linkedin, etc. 
* Save custom terms, etc, in the states Object

```json
    "states": {
		"type": "Schema.Types.Mixed"		
	}
```
* Ex: save number of pages user goes to, and number of errors are served

```json
    "states": {
		"page_counter":1,
		"errors":11
	}
```
[^](#collections)

##Profile
*Used for user profiles, levels (groups, collaborations, companies, teams)


```json
	"profile": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"body": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"title": {
			"type": "String",
			"required": true
		},
		"path": {
			"type": "String",
			"required": true,
			"unique":true
		},
		"photo": {
			"type": "String"
		},
		"gender": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},
		"info": {
			"type": "String",
			"editor": true
		},
		"email": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},
		"group": {
			"type": "String",
			"default": "",
			"lowercase": true,
			"trim": true
		},

		"lang": {
			"type": "String"
		},
		"link":{"type": "Schema.Types.Mixed"},
		"contact":{"type": "Schema.Types.Mixed"},
		"birthday": {
			"type": "Date"
		},
		"timezone":{
			"type":"Number"
		},
		"media": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "media"
				},
				"group":"String",
				"extra":"Schema.Types.Mixed"
			}
		],
		"profile": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "profile"
				},
				"extra":"Schema.Types.Mixed"
			}
		]
	}

	
```
* Example Usage

```json
	{
        "__v": 0,
        "_id": "51cf7a5894831db810000009",
        "email": "user@example.com",
        "gender": "m",
        "lang": "en",
        "link": {
                "facebook": "https://www.facebook.com/zuck",
                "twitter": "https://www.twitter.com/mark",
                "linkedin": "http://www.linkedin.com/pub/mark-zuckerberg/46/895/358"
        	},
        "path": "yj5iluktq5rlhgqcgvdaxdrq",
        "photo": "",
        "timezone": -4,
        "title": "First Last",
        "profile": [],
        "group": "client",
        "body":{
        	"firstname": "Mark",
        	"lastname": "Zuckerberg"
    	},
    	 "states":{
        	"rating": 20
    	}
    }
	
```
[^](#collections)

##Role
* Use to define rights, such as create, delete, update, read, master etc. 
* CRUD (Create Read Update Delete): for the current item.
* The defined role permission set is applied to different Objects such as [Levels](#level), [Loaders](#loader), [Items](#item)


```json
	"role": {
		"states": {
			"type": "Schema.Types.Mixed"
		},
		"path": {
			"type": "String",
			"required": true,
			"lowercase": true,
			"trim": true,
			"unique": true
		},
		"title": {
			"type": "String",
			"required": true
		},
		"create": {
			"type": "String"
		},
		"delete": {
			"type": "String"
		},
		"update": {
			"type": "String"
		},
		"read": {
			"type": "String"
		},
		"child":[
			{
				"group":{
					"type": "String",
					"lowercase": true
				},
				"model":{
					"type": "String",
					"lowercase": true
				},
				"create": {
					"type": "String"
				},
				"delete": {
					"type": "String"
				},
				"update": {
					"type": "String"
				},
				"read": {
					"type": "String"
				}
			}
		],
		"master": {
			"type": "String"
		},
		"custom": {
			"type": "Schema.Types.Mixed"
		}
	}
```
* Example role: owner with all permissions, master.

```json	
	{
	  "data":{
		"token":"123456",
	    "model": {
	      "title":"owner",
	      "path":"owner",
	      "master": "true"
	    },
	    "query":{},
	    "request":"create"
		}
	}
```

* Example role: private, default role, by not defining a permission, the default rights are 0, none. 

```json	
	{
	  "data":{
		"token":"123456",
	    "model": {
	      "title":"private",
	      "path":"private"	      
	    },
	    "query":{},
	    "request":"create"
		}
	}
```

* Example role: public, default role, default state for read only.

```json	
	{
	  "data":{
		"token":"123456",
	    "model": {
	      "title":"public",
	      "path":"public",
	      "read": "true"	      
	    },
	    "query":{},
	    "request":"create"
		}
	}
```
[^](#collections)

##Loader
* Used for projects
```json
		"loader": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"path": {
			"type": "String",
			"lowercase": true,
			"trim": true,
			"unique":true
		},
		"title": {
			"type": "String"
		},
		"photo": {
			"type": "String"
		},
		"level": {
			"type": "Schema.Types.ObjectId",
			"ref": "level"
		},
		"publish": {
			"type": "Boolean",
			"default": true
		},
		"date": {
			"type": "Date",
			"required": true
		},
		"end": {
			"type": "Date"
		},
		"body":{
				"type": "Schema.Types.Mixed"
		},
		"module": [{
			"item":{
				"type": "Schema.Types.ObjectId",
				"ref": "item"
				}
			,"extra":{
				"type": "Schema.Types.Mixed"
				}
			,"group":{
				"type": "String"
				}
		}],
		"loader": {
			"type": "Schema.Types.ObjectId",
			"ref": "loader"
		},
		"role": {
			"type": "Schema.Types.ObjectId",
			"ref": "role"
		},
		"group": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},"geo": { 
			"type": "Schema.Types.Mixed", 
			"index": "2dsphere",
			"sparse": true 
		},
		"media": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "media"
				},
				"group":"String",
				"extra":"Schema.Types.Mixed"
			}
		],
		"permission": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "profile"
				},
				"role": {
					"type": "Schema.Types.ObjectId",
					"ref": "role"
				},
				"extra":"Schema.Types.Mixed"
			}
		],
		"tags":{"type":"[String]"}
	}
	
```
[^](#collections)

##Level
```json
	"level": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"path": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},
		"body": {
			"type": "Schema.Types.Mixed"
		},
		"profile": {
			"type": "Schema.Types.ObjectId",
			"ref": "profile"
		},
		"level": {
			"type": "Schema.Types.ObjectId",
			"ref": "level"
		},
		"role": {
			"type": "Schema.Types.ObjectId"
		},
		"group": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},
		"permission": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "profile"
				},
				"role": {
					"type": "Schema.Types.ObjectId",
					"ref": "role"
				}
			}
		]
	}
```
[^](#collections)

#Grid 
```json
	"grid": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"path": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},
		"title": {
			"type": "String",
			"default": ""
		},
		"width": {
			"type": "Number",
			"default": 0
		},
		"height": {
			"type": "Number",
			"default": 0
		},
		"item": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "item"
				},
				"col": {
					"type": "Number"
				},
				"size_x": {
					"type": "Number"
				},
				"size_y": {
					"type": "Number"
				},
				"row": {
					"type": "Number"
				}
			}
		]
	}
```
[^](#collections)

##Blob
```json
	"blob": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"body": {
			"type": "Schema.Types.Mixed"
		},
		"group": {
			"type": "String"
		},
		"date": {
			"type": "Date"
		}
	}
```
[^](#collections)

##Event
```json
	"event": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"group": {
			"type": "String",
			"default": "",
			"lowercase": true,
			"trim": true
		},
		"route": {
			"type": "String",
			"default": "",
			"trim": true
		},
		"hostname":{
			"type": "String",
			"default": "",
			"trim": true
		},
		"retry":{
			"type": "Number",
			"default": 0
		},
		"maxRetry":{
			"type": "Number",
			"default": 0
		},
		"path": {
			"type": "String",
			"trim": true,
			"unique":true,
			"required":true
		},
		"date": {
			"type": "Date",
			"default": "Date.now"
		},
		"timeout":{
			"type": "Number",
			"default": 3000000
		},
		"stale":{
			"type": "Date"
		},
		"progress":{
			"total":{
				"type": "Number",
				"default": 0
			}
			,"complete":{
				"type": "Number",
				"default": 0
			}
		},
		"session":{
			"type": "Schema.Types.Mixed"
		},
		"query": {
			"type": "Schema.Types.Mixed"
		},
		"params": {
			"type": "Schema.Types.Mixed"
		},
		"body": {
			"type": "Schema.Types.Mixed"
		},
		"response":{
			"type": "Schema.Types.Mixed"
		},
		"statusCode": {
			"type":"Number"
		},
		"receiver": [
			{"profile":{
				"type": "Schema.Types.ObjectId",
				"ref": "profile"},
				"seen":{"type": "Date"}
			}
		],
		"message": {
			"type": "String"
		},
		"started": {
			"type": "Date"
		},
		"done": {
			"type": "Date"
		},
		"sender": {
					"type": "Schema.Types.ObjectId",
					"ref": "profile"
		},
		"role":{
			"type": "Schema.Types.ObjectId",
			"ref": "role"
		},
		"permission": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "profile"
				},
				"role": {
					"type": "Schema.Types.ObjectId",
					"ref": "role"
				},
				"extra":{"type":"Schema.Types.Mixed"}
			}
		]
	}
```
[^](#collections)

##Media
```json
	"media":{
   		"path": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},
		"title": {
			"type": "String",
			"default": ""
		},
		"ext": {
			"type": "String",
			"default": ""
		},
   		"filename": {
			"type": "String",
			"default": ""
		},
		"filesize": {
			"type": "Number",
			"default": 0
		},
		"url": {
			"type": "String",
			"default": ""
		},
		"body": {
			"type": "Schema.Types.Mixed"
		},
		"states": {
			"type": "Schema.Types.Mixed"
		},
    	"width": {
			"type": "Number",
			"default": 0
		},
		"height": {
			"type": "Number",
			"default": 0
		},
		"unit": {
			"type": "String"
		},
		"group": {
			"type": "String",
			"default": "",
			"lowercase": true,
			"trim": true
		},
		"role":{
			"type": "Schema.Types.ObjectId",
			"ref": "role"
		},
    	"permission": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "profile"
				},
				"role": {
					"type": "Schema.Types.ObjectId",
					"ref": "role"
				},
				"extra":"Schema.Types.Mixed"
			}
		],
		"tags":{"type":"[String]"}
	}
```
[^](#collections)

##Command
```json
	"command": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"refresh": {
			"id": {
				"type": "Schema.Types.ObjectId",
				"ref": "profile"
			},
			"date": {
				"type": "Date"
			}
		},
		"command": {
			"id": {
				"type": "Schema.Types.ObjectId",
				"ref": "profile"
			},
			"date": {
				"type": "Date"
			},
			"data": {
				"type": "String"
			},
			"time": {
				"type": "Number"
			}
		},
		"publishSite": {
			"id": {
				"type": "Schema.Types.ObjectId",
				"ref": "profile"
			},
			"date": {
				"type": "Date"
			},
			"data": {
				"type": "Number"
			},
			"message": {
				"type": "String"
			}
		}
	}
```
[^](#collections)

##Report 
```json
	"report": {
		"states": {
			"type": "Schema.Types.Mixed",
			"hidden": true
		},
		"date": {
			"type": "Date"
		},
		"totals": [
			{
				"name": {
					"type": "String"
				},
				"total": {
					"type": "Number"
				},
				"removed": {
					"type": "Schema.Types.Mixed"
				}
			}
		],
		"errs": {
			"type": "Schema.Types.Mixed"
		},
		"message": {
			"type": "String"
		}
	}
```


##Custom
You can access and modify your schemas using your api, by using the collection schemas "/api/v1/schemas"
You will see all the schemas that are in here. Use these as guides plus the [mongoose](http://mongoosejs.com/docs/guide.html) documentation.
When you add a key that will be your models name, and its object is the schema. 
Once you restart your instance the new schemas will instantly take effect.

[^](#collections)

[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)
