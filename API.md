[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)

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
* [Create](#create)
* [Read](#read)
* [Update](#update)
* [Delete](#delete)
* [Count](#count)

[options](#options)

###Create
Create a new item
```
{
  "data":
  {"token" : "123456"
    , "request" : "create"
    ,"model": {
      "title":"South Beach"
      ,"body":{
        "city":"Miami"
      }
    }
  }
}
```
###Read
Get the objects
```
{
  "data":
  {"token" : "123456"
    , "request" : "read"
    ,"query":{
      ,"body.city":"Miami"
    }
  }
}
```

###Update
Update an existing one by specifiying _id in query
```
{
  "data":
  {"token" : "123456"
    , "request" : "update"
    ,"query":{
      "_id": "531438bfdff0e4fe250000a4"
    }
    ,"model": {
      "title":"South Beach"
      ,"body":{
        "city":"Miami"
      }
    }
  }
}
```

###Delete
Delete by query or id 
```
{
  "data":
  {"token" : "123456"
    , "request" : "delete"
    ,"query":{
      "_id": "531438bfdff0e4fe250000a4"
    }
  }
}
```

###Count
Get the number of objects
```
{
  "data":
  {"token" : "123456"
    , "request" : "count"
    ,"query":{
      ,"body.city":"Miami"
    }
  }
}
```

Options 
---
* [limit](#limit) (number)
* [skip](#skip) (number)
* [sort](#sort) (object)
* [select](#select) (object)
* [show](#show) (boolean)
* [send](#send) (boolean)
* [total](#total) (boolean)
all are optional 

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
### Total
***expects a boolean (true/false) default false***
Show the total number of objects for the query reguardless of the limit of results. This can be used for pagenation to know the end of possible results.

```
//query
 "total":true

//result
{ "total":123
  ,"limit":1
  ,"length":1
  ,"results":[
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

Types of Schemas
---
* [item](https://github.com/LiveSqrd/docs/edit/master/schemas.md#item)
* [instance](https://github.com/LiveSqrd/docs/edit/master/schemas.md#instance)
* [client](https://github.com/LiveSqrd/docs/edit/master/schemas.md#client)
* [profile](https://github.com/LiveSqrd/docs/edit/master/schemas.md#profile)
* [role](https://github.com/LiveSqrd/docs/edit/master/schemas.md#role)
* [loader](https://github.com/LiveSqrd/docs/edit/master/schemas.md#loader)
* [level](https://github.com/LiveSqrd/docs/edit/master/schemas.md#level)
* [grid](https://github.com/LiveSqrd/docs/edit/master/schemas.md#grid)
* [blob](https://github.com/LiveSqrd/docs/edit/master/schemas.md#blob)
* [event](https://github.com/LiveSqrd/docs/edit/master/schemas.md#event)
* [command](https://github.com/LiveSqrd/docs/edit/master/schemas.md#command)
* [report](https://github.com/LiveSqrd/docs/edit/master/schemas.md#report)


====

#CURL

curl -i -H "Accept: application/json" -H "Content-Type: application/json" -d '{"data":{"token" : "123456", "request" : "delete","query": {},"select":{},"show":true}}' https://dev-voting.lsq.io/api/v1/item



[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)
