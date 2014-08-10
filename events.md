[<-](https://github.com/LiveSqrd/docs#some-usefull-resources)

Events
===

Events allow you to queue and schedule tasks, to be done in the future or to be spread between squares. 
Every square checks for tasks to do based on a interval, with a max amount to do at a give time.
In the config you can set them with the keys, eventMaxTasks (defaults to 10) and eventInterval (defaults to 30000 "30 secs").

Everytime the interval hits it gets the next events to be done up to the eventMaxTasks. These events are formated to match the express node framework so you can use your normal api calls to be used for the event functions with no changes,to natually extend functionality.



*lsq = db*

Add on event function
---

To do something on an event, in your hooks you put.
```js

//lsq.onEvent(route,callback)

lsq.onEvent("userInvite",function(req,res){
  sendEmail(req.body.email,req.body.user+" would like to invite you to "+req.body.company)
  //res.status(200)
  //res.send(200,"email sent")
  res.send("email sent")
})

```


Event fields [schema](https://github.com/LiveSqrd/docs/blob/master/schemas.md#event)
---
- route *the key for onEvent*
- date *the date to be executed if you put current date it will be ran asap*
- params *the same params as in [express](http://expressjs.com/api#req.params)*
- query *the same query as in [express](http://expressjs.com/api#req.query)*
- body *the same body as in [express](http://expressjs.com/api#req.body)*
- session *the same used in api requests*
- response *the response from the function*
- statusCode *default is 200 but matches http statuscode for error checking*
- timeout *default is 300000 "5 mins", the amount of time given to execute function*
- starting *date that will be filled in once event has started to process*
- done *date that will be filled in once event has sent a response*
- stale *date that executing the event is to late and to disreguard event*
- receiver *if someone would be notified*
  - profile
  - seen
- sender *who is to make the request*
- group 
- states
- role
- permission


Event defualt status codes
---
the status code and marked as done for the following:
- 404 *if no route with function found*
- 408 *Timed out*
- 410 *stale*
- 200 *everything is ok*



