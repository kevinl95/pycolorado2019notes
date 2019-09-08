# Advanced asyncio: Solving Real-World Production Problems
## Lynn Root, Staff Engineer at Spotify
[Link to Slides](http://www.rogue.ly/aio)
---

### Async All the Things
Mayhem Mandrill - restart instances when message received
'await' is before a line that should be blocking. Anything after this line will have to wait to be run until the task running in that line finishes
Can create concurrent tasks with asyncio create_task
Great if you have a bunch of tasks that do not depend on each other
Needing sequential tasks does not preclude using async, you can use await for things that have to happen in order.
Can define callbacks to create tasks that run when the async task returns. Great for cleanup/processing. Await may be cleaner than using callbacks. Fewer lines
Asycn != concurrent
Serial != blocking
Just say 'no' to callbacks

### Graceful Shutdowns
Need a signal handler
Waches the task
Collects current/pending/all tasks and cancel them. May need to collect outstanding metrics if you are collecting them
Need to define signals for the handler, like the keyboard interrupt signal. Lets you stop everything gracefully rather than have the service end in an incomplete/unknown state.
More here with code: https://www.roguelynn.com/words/asyncio-exception-handling

This talk was an excellent coding walkthrough, it is better if you read her code along with her commentary rather than have me comment on it her: http://www.rogue.ly/aio
