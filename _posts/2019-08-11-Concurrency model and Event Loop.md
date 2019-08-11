---
layout: post
title: Concurrency model and Event Loop
subtitle: Web Development
date: 2019-08-11
author: Jalever
header-img: img/post_2019_web_development_bg.png
catalog: true
tags:
    - Web Development
---

- [Runtime concepts](#runtime-concepts)
    - [Visual representation](#visual-representation)
    - [Stack](#stack)
    - [Heap](#heap)
    - [Queue](#queue)
- [Event loop](#event-loop)
    - [Run-to-completion](#run-to-completion)
    - [Adding messages](#adding-messages)
    - [Zero delays](#zero-delays)
    - [Several runtimes communicating together](#several-runtimes-communicating-together)
- [Never blocking](#never-blocking)

JavaScript has a concurrency model based on an "event loop". This model is quite different from models in other languages like C and Java.

## Runtime concepts
The following sections explain a theoretical model. Modern JavaScript engines implement and heavily optimize the described semantics.

#### Visual representation
![exS0hj.png](https://s2.ax1x.com/2019/08/11/exS0hj.png)

#### Stack
Function calls form a stack of frames.
![exSyj0.png](https://s2.ax1x.com/2019/08/11/exSyj0.png)
When calling <strong>bar</strong>, a first frame is created containing <strong>bar</strong>'s arguments and local variables. When <strong>bar</strong> calls <strong>foo</strong>, a second frame is created and pushed on top of the first one containing <strong>foo</strong>'s arguments and local variables. When <strong>foo</strong> returns, the top frame element is popped out of the stack (leaving only <strong>bar</strong>'s call frame). When <strong>bar</strong> returns, the stack is empty.

#### Heap
Objects are allocated in a heap which is just a name to denote a large mostly unstructured region of memory.

#### Queue
A JavaScript runtime uses a message queue, which is a list of messages to be processed. Each message has an associated function which gets called in order to handle the message.

At some point during the event loop, the runtime starts handling the messages on the queue, starting with the oldest one. To do so, the message is removed from the queue and its corresponding function is called with the message as an input parameter. As always, calling a function creates a new stack frame for that function's use.

The processing of functions continues until the stack is once again empty; then the event loop will process the next message in the queue (if there is one).

## Event loop
The event loop got its name because of how it's usually implemented, which usually resembles:
![expnvq.png](https://s2.ax1x.com/2019/08/11/expnvq.png)
<strong>queue.waitForMessage()</strong> waits synchronously for a message to arrive if there is none currently.

#### Run-to-completion
Each message is processed completely before any other message is processed. This offers some nice properties when reasoning about your program, including the fact that whenever a function runs, it cannot be pre-empted and will run entirely before any other code runs (and can modify data the function manipulates). This differs from C, for instance, where if a function runs in a thread, it may be stopped at any point by the runtime system to run some other code in another thread.

A downside of this model is that if a message takes too long to complete, the web application is unable to process user interactions like click or scroll. The browser mitigates this with the "a script is taking too long to run" dialog. A good practice to follow is to make message processing short and if possible cut down one message into several messages.

#### Adding messages
In web browsers, messages are added anytime an event occurs and there is an event listener attached to it. If there is no listener, the event is lost. So a click on an element with a click event handler will add a message--likewise with any other event.

The function <strong>setTimeout</strong> is called with 2 arguments: a message to add to the queue, and a time value (optional; defaults to 0). The time value represents the (minimum) delay after which the message will actually be pushed into the queue. If there is no other message in the queue, the message is processed right after the delay; however, if there are messages, the <strong>setTimeout</strong> message will have to wait for other messages to be processed. For that reason, the second argument indicates a minimum time and not a guaranteed time.

Here is an example that demonstrates this concept (<strong>setTimeout</strong> does not run immediately after its timer expires):
![expHRs.png](https://s2.ax1x.com/2019/08/11/expHRs.png)

#### Zero delays
Zero delay doesn't actually mean the call back will fire-off after zero milliseconds. Calling <strong>setTimeout</strong> with a delay of 0 (zero) milliseconds doesn't execute the callback function after the given interval.

The execution depends on the number of waiting tasks in the queue. In the example below, the message ''this is just a message'' will be written to the console before the message in the callback gets processed, because the delay is the minimum time required for the runtime to process the request, but not a guaranteed time.

Basically, the setTimeout needs to wait for all the code for queued messages to complete even though you specified a particular time limit for your setTimeout.
![expxdU.png](https://s2.ax1x.com/2019/08/11/expxdU.png)
![ex99JJ.png](https://s2.ax1x.com/2019/08/11/ex99JJ.png)

#### Several runtimes communicating together
A web worker or a cross-origin <strong>iframe</strong> has its own stack, heap, and message queue. Two distinct runtimes can only communicate through sending messages via the <strong>postMessage</strong> method. This method adds a message to the other runtime if the latter listens to <strong>message</strong> events.

## Never blocking
A very interesting property of the event loop model is that JavaScript, unlike a lot of other languages, never blocks. Handling I/O is typically performed via events and callbacks, so when the application is waiting for an <strong>IndexedDB</strong> query to return or an <strong>XHR</strong> request to return, it can still process other things like user input.

Legacy exceptions exist like <strong>alert</strong> or synchronous XHR, but it is considered as a good practice to avoid them.
