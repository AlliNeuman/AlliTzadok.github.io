---
layout: post
title:      "What is a Promise?"
date:       2019-01-01 23:20:50 +0000
permalink:  what_is_a_promise
---


A promise is a proxy for a value that will eventually become available.  When we request information from the server with a fetch request, the promise is how we handle asychronous code.  Simply put, it is an object that may produce a single value some time in the future. The value will either be a resolved value or a reason that it's not resolved.  There are 3 possible states for a promise: fulfilled, rejected or pending.


A promise object serves as a link between the executor and the consuming functions.  Consuming functions are chained by using `.then` or `.catch`.  We use these methods to access the state and result of te Promise objects.
# Promise States
*pending*: the initial state, neither fulfilled or rejected
*fulfilled*: the operation completed successfully
*rejected*: the operation failed

# How do Promises work?

A promise is an object that can be returned sychronously from an asychronous function.  A promise is considered settled if it is not pending. Being settled means it was either resolved or rejected.  Only the function responsible for creating the promise will know the status of the promise. 

If the promise was Fulfilled, `onFulfilled()` will be called.
If the promise was Rejected `onRejected()` will be called.
If a promise is pending that means it was neither resolved or settled.

Once a promise has been settled it cannot be resettled.


