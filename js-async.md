# Promises

https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261
A promise is an object that may produce a single value some time in the future: either a resolved value, or a reason that it’s not resolved (e.g., a network error occurred). A promise may be in one of 3 possible states: fulfilled, rejected, or pending. Promise users can attach callbacks to handle the fulfilled value or the reason for rejection.

##A promise is an object which can be returned synchronously from an asynchronous function. It will be in one of 3 possible states:##

Fulfilled: onFulfilled() will be called (e.g., resolve() was called)
Rejected: onRejected() will be called (e.g., reject() was called)
Pending: not yet fulfilled or rejected

promise.then(
onFulfilled?: Function,
onRejected?: Function
) => Promise

# Event loop

https://hackernoon.com/understanding-js-the-event-loop-959beae3ac40

https://medium.com/@Rahulx1/understanding-event-loop-call-stack-event-job-queue-in-javascript-63dcd2c71ecd

https://flaviocopes.com/javascript-event-loop/

https://medium.com/front-end-weekly/javascript-event-loop-explained-4cd26af121d4

https://medium.com/swlh/understanding-the-node-js-event-loop-181c2cbfcbb1

https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/

https://stackoverflow.com/questions/46375711/what-is-the-relationship-between-event-loop-and-promise
