# Event Loop
As we know JavaScript code runs in single threaded.This means that only one set of instructions is executed at any single time.But in JavaScript `later` doesn’t necessarily happen strictly and immediately after `now`. In other words, tasks that cannot complete now are going to complete asynchronously.

JavaScript has a concurrency model based on an event loop, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks.

The Event Loop has one simple job — to monitor the Call Stack and the Callback Queue. If the Call Stack is empty, it will take the first event from the queue and will push it to the Call Stack, which effectively runs it.
![](https://miro.medium.com/max/700/1*FA9NGxNB6-v1oI2qGEtlRQ.png)

## Memory Heap
Memory Heap is a place to store and write information and data for our app(variables, objects, etc..).
For examble 
```js
const number = 5
```
The above code is saying please allocate memory for the number variable and have it point to the value 5 in our memory heap.

## The call stack
The call stack is a LIFO queue (Last In, First Out).
The event loop continuously checks the call stack to see if there’s any function that needs to run.
While doing so, it adds any function you call it to the call stack and executes each one in order.We push and pop functions off the stack one by one. And so Javascript is synchronous — only one thing can happen at a time.

## Queue
A JavaScript runtime uses a queue, which is a list of messages to be processed. Each message has an associated function which gets called in order to handle the message.
At some point during the event loop, the runtime starts handling the messages on the queue, starting with the oldest one. To do so, the message is removed from the queue and its corresponding function is called with the message as an input parameter. As always, calling a function creates a new stack frame for that function's use.
The processing of functions continues until the stack is once again empty. Then, the event loop will process the next message in the queue (if there is one).


For example, let's see what will happend when we execute this code ...
```js
console.log('Hi');
setTimeout(function cb1() { 
    console.log('cb1');
}, 5000);
console.log('Bye');
```
### 1.In the beginning ,The state is clear. The browser console is clear, and the Call Stack is empty.
![](https://miro.medium.com/max/700/1*9fbOuFXJHwhqa6ToCc_v2A.png)

### 2.`console.log('Hi')` is added to the Call Stack.
![](https://miro.medium.com/max/700/1*dvrghQCVQIZOfNC27Jrtlw.png)

### 3.Now `console.log('Hi')` is executed.
### 4.After that `console.log('Hi')` is removed from the Call Stack.
![](https://miro.medium.com/max/700/1*iBedryNbqtixYTKviPC1tA.png)

### 5.Now, setTimeout(function cb1() { ... }) is added to the Call Stack.
![](https://miro.medium.com/max/700/1*HIn-BxIP38X6mF_65snMKg.png)

### 6.The browser creates a timer as part of the Web APIs. It is going to handle the countdown for you.
![](https://miro.medium.com/max/700/1*vd3X2O_qRfqaEpW4AfZM4w.png)

 ### 7.The `setTimeout(function cb1() { ... })` itself is complete and is removed from the Call Stack.
 ![](https://miro.medium.com/max/700/1*_nYLhoZPKD_HPhpJtQeErA.png)
 
 ### 8.Then `console.log('Bye')` is added to the Call Stack.
 ![](https://miro.medium.com/max/700/1*1NAeDnEv6DWFewX_C-L8mg.png)
 
 ### 9.`console.log('Bye')` is executed.
 ![](https://miro.medium.com/max/700/1*UwtM7DmK1BmlBOUUYEopGQ.png)
 
 ### 10.`console.log('Bye')` is removed from the Call Stack.
 ![](https://miro.medium.com/max/700/1*-vHNuJsJVXvqq5dLHPt7cQ.png)
 
 ### 11.After 5000 ms, the timer completes and it pushes the cb1 callback to the Callback Queue.
 ![](https://miro.medium.com/max/700/1*eOj6NVwGI2N78onh6CuCbA.png)
 
 ### 12.The Event Loop takes cb1 from the Callback Queue and pushes it to the Call Stack.
 ![](https://miro.medium.com/max/700/1*jQMQ9BEKPycs2wFC233aNg.png)
 
 ### 13.`cb1` is executed and adds `console.log('cb1')` to the Call Stack.
 ![](https://miro.medium.com/max/700/1*hpyVeL1zsaeHaqS7mU4Qfw.png)
 
 ### 14.`console.log('cb1')` is executed.
 ![](https://miro.medium.com/max/700/1*lvOtCg75ObmUTOxIS6anEQ.png)
 ### 15.`console.log('cb1')` is removed from the Call Stack.
 ### 16.After that `cb1` is removed from the Call Stack.
 <br>
 ## Blocking the event loop
 Any JavaScript code that takes too long to return back control to the event loop will block the execution of any JavaScript code in the page, even block the UI thread, and the user cannot click around, scroll the page, and so on. This is why JavaScript is based so much on callbacks, and more recently on promises and async/await.
 <br>
 ## Resources
 - https://flaviocopes.com/javascript-event-loop/
 - https://blog.sessionstack.com/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-2f077c4438b5
 - https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop
 
 
 
 
 
