items collection
===
##Fetch In Backbone w/ extras

###options
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

## Example Use
### items is a collection pre defined:

1st Part:
```
define(['require', 'jquery', 'underscore', 'bb', 'i/item/c']
        , function(require, $, _, Backbone, Items) {........

......});
````

2nd Part:
```
    return Backbone.View.extend({
            id: 'index',
            initialize: function(options) {
                this.items = new Items(null,{ s: this.___.so});
                .....//Collections, Templates, are Initilized here as well
```

3rd Part: Here we can use the items to perform several functions, in this case fetch. 
Fetch is a Backbone function with LiveSqrd Extensions and Options such as success, error etc. 
Once the fetch is performed on the items we can now iterate through them using each, in this case we are printing a log and appending the model to a template

```
    that.items.fetch({
        success:function(){                                    
            that.items.each(function(m){                            
                console.log(m.toJSON())                            
                that.$("ul.startups").append(
                    that.startupSingle(m.toJSON())
                );
            });

        }
        , data: {"group":"startup"}        
    });
```


Creating New Item
====

Once your items has been initilized you can put things into it.
In this Example the item is populated from input fields in the View.

```
    that.items.create(
        {
            "title":($("#company_name").val()),
            "body":{
                "founders" : ($("#founders").val()),
                "city" : ($("#city").val()),
                "url" : ($("#url").val())

            },
            "group":"startup"
        }
        ,{
            callback:function(json,m){
                console.log("m:",m);
            }
        }
    );
```
