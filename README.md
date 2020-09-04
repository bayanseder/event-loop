# event-loop

JavaScript has a concurrency model based on an event loop, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks.
The Event Loop has one simple job — to monitor the Call Stack and the Callback Queue. If the Call Stack is empty, it will take the first event from the queue and will push it to the Call Stack, which effectively runs it.
![](https://miro.medium.com/max/700/1*FA9NGxNB6-v1oI2qGEtlRQ.png)

### Heap
This is where the memory allocation happens

### The call stack
The call stack is a LIFO queue (Last In, First Out).
The event loop continuously checks the call stack to see if there’s any function that needs to run.
While doing so, it adds any function you call it to the call stack and executes each one in order.

### Queue
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
In the beginning ,The state is clear. The browser console is clear, and the Call Stack is empty.
![](https://miro.medium.com/max/700/1*9fbOuFXJHwhqa6ToCc_v2A.png)
`console.log('Hi')` is added to the Call Stack.
![](https://miro.medium.com/max/700/1*dvrghQCVQIZOfNC27Jrtlw.png)
Now `console.log('Hi')` is executed.After that `console.log('Hi')` is removed from the Call Stack.
![](https://miro.medium.com/max/700/1*iBedryNbqtixYTKviPC1tA.png)
Now, setTimeout(function cb1() { ... }) is added to the Call Stack.
![](https://miro.medium.com/max/700/1*HIn-BxIP38X6mF_65snMKg.png)
The browser creates a timer as part of the Web APIs. It is going to handle the countdown for you.
![](https://miro.medium.com/max/700/1*vd3X2O_qRfqaEpW4AfZM4w.png)
 The `setTimeout(function cb1() { ... })` itself is complete and is removed from the Call Stack.
 ![](https://miro.medium.com/max/700/1*_nYLhoZPKD_HPhpJtQeErA.png)
 Then `console.log('Bye')` is added to the Call Stack.
 ![](https://miro.medium.com/max/700/1*1NAeDnEv6DWFewX_C-L8mg.png)
 `console.log('Bye')` is executed.
 ![](https://miro.medium.com/max/700/1*UwtM7DmK1BmlBOUUYEopGQ.png)
 `console.log('Bye')` is removed from the Call Stack.
 ![](https://miro.medium.com/max/700/1*-vHNuJsJVXvqq5dLHPt7cQ.png)
 After 5000 ms, the timer completes and it pushes the cb1 callback to the Callback Queue.
 ![](https://miro.medium.com/max/700/1*eOj6NVwGI2N78onh6CuCbA.png)
 The Event Loop takes cb1 from the Callback Queue and pushes it to the Call Stack.
 ![](https://miro.medium.com/max/700/1*jQMQ9BEKPycs2wFC233aNg.png)
 `cb1` is executed and adds `console.log('cb1')` to the Call Stack.
 ![](https://miro.medium.com/max/700/1*hpyVeL1zsaeHaqS7mU4Qfw.png)
 `console.log('cb1')` is executed.
 ![](https://miro.medium.com/max/700/1*lvOtCg75ObmUTOxIS6anEQ.png)
 `console.log('cb1')` is removed from the Call Stack.
 After that `cb1` is removed from the Call Stack.
 
 
 
 
 
