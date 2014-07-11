Validation
=======

How to use on server
---
It is part of lsq object (Also called db).

The class has 2 optional params:
* schema (js object with defined rules and modifiers)
* model (js object to validate against)
* opttions (stop and strict)

The class will return it self, to be able to access and rerun validation later.

On create of the validation Object, if both schema and model are entered the function validate will run instantly.
Allowing you to retrieve the error with the error property.

The error will be a boolean false if there is no error.
Other wise the error will be a string with the key of where it errored plus information on why.
The validation stops as soon as the first error happens.

Sample:
---
```js

var validate = new db.validation(schema,model);
if(!validate.error){
}


```

All the keys in the schema are deep body.
example:
```js

{body:{
      address:{
        city:"New York"
        ,zip:"10013"
      }
      ,name:"joe"
  }}


// becomes

{
 "body":{}
,"body.name":"joe"
,"body.address":{}
,"body.address.city":"New York"
,"body.address.zip":"10013"
}
```

Options:
---
* stop |boolean| 
 * true (defualt: it will stop checking as soon as one error)
 * false (it will make object of errors fill up with array for each key with error)
* strict |boolean|
 * true (will populate an object result with just keys you set in schema)
 * false (defualt: does't make result)

Methods:
----
* validate (it uses the model and schema properties)
* setModel (this also sets the original model)

Properties:
---
* schema (object with defined rules and modifiers)
* model (object to validate against)
* error (false or a string)
* originalModel (the unmodified model)
* errors (object of errors fill up with array for each key with error stop:false)
* result ( object with just keys you set in schema strict:true)

Schema Types: (all lowercase)
---
- string
- boolean
- number
- array
- function
- object 
- date (can be a valid date format or timestamp or date object)

Schema Modifiers:
---
- modify (a function that the return will replace the value of that key)
- default (will be placed in if key doesn't exisit)
- String:
 - trim -true-
 - uppercase -true-
 - lowercase -true-
 - stripTags -true- (strip html or xml tags)
 - toType -"string"- will convert:
  - Object/Array (json)
  - Number/Boolean (string)
  - Date (toJson string)
- Boolean:
 - toType -"boolean"- (will convert "true" to true and "false" to false)
- Number:
 - toType -"float","int"- (will convert "12.3" to 12.3 and "12.3" to 12)
- Object:
 - toType -"object"- (will convert from json to obj)
- Date:
 - toType -"date","string","number"- 
  - "date" (Date object)
  - "string" (to json)
  - "number" (unix timestamp)

Schema Validators:
---
- require -true-
- equals (will check for compare)
- String:
 - min -number- (minime number of charactors)
 - max -number- (max number of charactors)
 - length -number- (exact number of charactors)
 - match -RegExp,string- (will check it that is a match in value)
- Number
 - min -number-
 - max -number-
- Array
 - min -number- (minime array size)
 - max -number- (max array size)
 - length -number- (exact length of array)
- Date
 - min -date,string,number- (at least new)
 - max -date,string,number- (at max older)


Sample Schema:
---
```js

var schema = {
         "hello":{"trim":true,"uppercase":true}
        ,"body.name":{"match":"hel"}
        ,"body.num":{"type":"number","toType":"int","min":25}
        ,"body.json":{"type":"object","toType":"object"}
        ,"body.day":{"require":true}
  }
var model = {
         "hello":"jasd asd  asd  "
        ,"body":{
             "name":"hello"
            ,"num":"30"
            ,"bday":"7/13/90"
            ,"json":"{\"me\":\"you\"}"
            ,"arr":[0,1,2]
        }

var validate = new db.validation(schema,model);
if(!validate.error){
 console.log(error); // errors: "body.day Not Found"
}

// validate.schema = {
//     "hello": {
//         "trim": true,
//         "uppercase": true,
//         "require": false,
//         "type": "string"
//     },
//     "body.name": {
//         "match": "hel",
//         "require": false,
//         "type": "string"
//     },
//     "body.num": {
//         "type": "number",
//         "toType": "int",
//         "min": 25,
//         "require": false
//     },
//     "body.json": {
//         "type": "object",
//         "toType": "object",
//         "require": false
//     },
//     "body.day": {
//         "require": true
//     }
// },
// validate.model = {
//     "hello": "JASD ASD  ASD",
//     "body": {
//         "name": "hello",
//         "num": 30,
//         "bday": "7/13/90",
//         "json": {
//             "me": "you"
//         },
//         "arr": [
//             0,
//             1,
//             2
//         ]
//     }
// },
// validate.originalModel = {
//     "hello": "jasd asd  asd  ",
//     "body": {
//         "name": "hello",
//         "num": 30,
//         "bday": "7/13/90",
//         "json": {
//             "me": "you"
//         },
//         "arr": [
//             0,
//             1,
//             2
//         ]
//     }
// },
```
