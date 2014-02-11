PostMan setup 

Url is your domain + "api/v1/" + schema
E.G. 
https://dev-voting.lsq.io/api/v1/client

Header Set
Content-Type = application/json


Method Post

Raw data set as JSON

`{
  "data":
 {"token" : "123456"
  , "request" : "delete"
  ,"query": {}
  ,"select":{}
  ,"show":true
 }
}`

Options
*limit (number)
*skip (number)
*sort (object)
*select (object)
*show (boolean)

Types of Schemas
*instance
*client
*profile
*item
*loader

