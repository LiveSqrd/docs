#PostMan setup 

###Url is your domain + "api/v1/" + schema

E.G. 
https://dev-voting.lsq.io/api/v1/client

Header Set
---
Content-Type = application/json

###Method Post

Raw data set as JSON
---
```
{
  "data":
 {"token" : "123456"
  , "request" : "delete"
  ,"query": {}
  ,"select":{}
  ,"show":true
 }
}
```

***you can change the token in you config***

Requests
---
* Create
* Read
* Update
* Delete
* Count

Options
---
* limit (number)
* skip (number)
* sort (object)
* select (object)
* show (boolean)

###Limit

Limits the number of results
```
"limit":10
```


###Skip
***expects a number***
Skips to the next set of results
```
"skip":10
```


###Sort
***expects a object***
What to sort the database call by 
A positive 1 is ascending and negiative 1 ***(-1)*** is Descending 
```
"sort":{"title":1}
```
```
"sort":{"title":-1}
```


####if you want to do pagination
***equivalent of third page of 20 results***
```
"limit":20
,"skip":40
,"sort":{"title":1}
```

###Select
***expects a object***
Allows you to omit or only get select fields
Use 1 to include fields and 0 to omit fields
```
//query
"select":{"title":1,"body.city":1}

//result
{"_id":146378461237849126213
,"title":"South Beach"
,"body":{
    "city":"Miami"
    }
}
```

```
//query
"select":{"body.email":0}

//result
{"_id":146378461237849126213
,"title":"South Beach"
,"path":"south_beach"
,"body":{
         "city":"Miami"
        ,"state":"fl"
        ,"contact":"John Smith"
    }
}
```
###Show
***expects a boolean (true/false) default false***
To show what results that are deleted or updated
when you do a multi delete or update (without using id) the result will only be the number that was effect. But when you use show it will give back the objects.
```
//query
"show":true

//result
{"results":[
    {"_id":146378461237849126213
    ,"title":"South Beach"
    ,"path":"south_beach"
    ,"body":{
             "city":"Miami"
            ,"state":"fl"
            ,"contact":"John Smith"
            ,"email":"john.smith@gmail.com"
        }
    }]
}
```

```
//query
"show":false

//result
{"results":[1]
}
```

Types of Schemas
---
* instance
* client
* profile
* item
* loader


====

#CURL

