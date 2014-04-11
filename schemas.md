[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)

#### The collection is the data collection name (string) :
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
* [command](#command)
* [report](#report)


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
		"x": {
			"type": "Number"
		},
		"y": {
			"type": "Number"
		},
		"z": {
			"type": "Number"
		},
		"width": {
			"type": "Number"
		},
		"height": {
			"type": "Number"
		},
		"color": {
			"type": "String"
		},
		"role":{
			"type": "Schema.Types.ObjectId",
			"ref": "role"
		},
		"permisson": [
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
		"geo": { 
			"type": "[Number]", 
			"index": "2dsphere",
			 "sparse": true 
		},
		"box":{
			"type": "[Number]", 
			"index": "2d",
			 "sparse": true 
		},
		"due": {
			"date": {
				"type": "Date"
			},
			"period": {
				"type": "Number"
			},
			"freq": {
				"type": "Number"
			}
		},
		"tags":{"type":"[String]"}
	}
```


## Instance
* Short life span, public user client identification information
* Created and destroyed with Socket.io events
* Output

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

##Client

* Session based storage and identification, used for user login, credentials, and other pertaining parameters
* Session based entails anonymous and profile attached logins. Unlike [Instances](#instance) they have a long life span: 30 days (subject to change)

* Output

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

##Profile
*Used for user profiles, levels (groups, collaborations, companies, teams)


```json
	{
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
		"profile": [
			{
				"id": {
					"type": "Schema.Types.ObjectId",
					"ref": "profile"
				},
				"title": {
					"type": "String"
				},
				"start": {
					"type": "Date"
				},
				"end": {
					"type": "Date"
				}
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
    	}
    	 "states":{
        	"rating": 20
    	}
    }
	
```

##Role
* Use to define rights, such as create, delete, update, read, add, remove, edit, destroy, master etc. 
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
			"type": "Number",
			"default": 0
		},
		"delete": {
			"type": "Number",
			"default": 0
		},
		"update": {
			"type": "Number",
			"default": 0
		},
		"read": {
			"type": "Number",
			"default": 0
		},
		"add": {
			"type": "Number",
			"default": 0
		},
		"remove": {
			"type": "Number",
			"default": 0
		},
		"edit": {
			"type": "Number",
			"default": 0
		},
		"destroy": {
			"type": "Number",
			"default": 0
		},
		"master": {
			"type": "Number",
			"default": 0
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
	      "master": 1
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
	      "read": 1	      
	    },
	    "query":{},
	    "request":"create"
		}
	}
```

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
			"type": "[Number]", 
			"index": "2dsphere",
			 "sparse": true 
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
		],
		"tags":{"type":"[String]"}
	}
	
```

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
		"action": {
			"type": "String",
			"default": "",
			"lowercase": true,
			"trim": true
		},
		"path": {
			"type": "String",
			"lowercase": true,
			"trim": true
		},
		"date": {
			"type": "Date"
		},
		"instance": {
			"type": "Schema.Types.ObjectId",
			"ref": "instance"
		},
		"client": {
			"type": "Schema.Types.ObjectId",
			"ref": "client"
		},
		"profile": {
			"type": "Schema.Types.ObjectId",
			"ref": "profile"
		},
		"level": {
			"type": "Schema.Types.ObjectId",
			"ref": "level"
		},
		"item": {
			"type": "Schema.Types.ObjectId",
			"ref": "item"
		},
		"loader": {
			"type": "Schema.Types.ObjectId",
			"ref": "loader"
		},
		"event": {
			"type": "Schema.Types.ObjectId",
			"ref": "event"
		},
		"reciver": [
			{"profile":{
				"type": "Schema.Types.ObjectId",
				"ref": "profile"},
			"seen":{"type": "Date"}
			}
		],
		"message": {
			"type": "String"
		},
		"done": {
			"type": "Boolean",
			"default": false
		},
		"data": {
			"type": "Schema.Types.Mixed"
		}
	}
```

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



[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)
