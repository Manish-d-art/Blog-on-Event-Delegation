# "Mastering Asynchronous JavaScript with Promises, Async/Await and AJAX: A Guide to Building Fast and Efficient Web Applications"

Hello there 🙋‍♂️ and welcome to my blog! I'm so glad you found your way here! let's dive into some great conversations!

Now, to understand what asynchronous JavaScript code is, we first need to understand what synchronous code is. So basically the opposite of asynchronous.

## Introduction to Asynchronous JavaScript:-

Synchronous code executes one line at a time, in the order, it is written, from top to bottom. It's a simple way to write code, but it can cause problems if you need to do things that take a long time, like getting information from the internet, working with files, or doing complex calculations. That's where Asynchronous JavaScript comes in. It helps you deal with these types of issues more efficiently.

**For example**, the following code is Synchronous:

```javascript
console.log("start");
const p = document.querySelector('.p');
p.textContent = 'Example of synchronous code';
alert('Text Set!');
p.style.color = 'red';
consol.log('END');
```

**In the above code**, the code is executed line by line. Now, this can create problems when one line of code takes a long time to run, For example in the above code we have an alert statement, which creates this alert this alert window. Now, this alert window will block the code execution, right? Nothing will happen on the page until we will click this ok button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676792740013/396d9558-1189-4b6a-957a-db92fdc9a086.png align="center")

And only then the code can continue executing. So, this is a nice illustration of the problem with Synchronous code.

But imagine that execution would have to wait for example, for a five-second timer to finish. That would be terrible, right? because meanwhile, nothing on the page would work during these five seconds. And so here Asynchronous code comes into play.

## Introduction to Asynchronous JavaScript:

**Asynchronous JavaScript** is a Programming technique that allows code to run without blocking the main thread. In other words, the program can continue to execute code while a task is being performed in the background without waiting for the task to complete.

Asynchronous code is typically used when dealing with time-consuming operations, such as network requests, file I/O, or complex computations to ensure that the program remains responsive and does not freeze.

In JavaScript, there are several ways to write asynchronous code, including callbacks, promises and async/ await.

**For example**, the following code is asynchronous:

```javascript
console.log("Start");
const p = document.querySelector('.p');
setTimeout(function() {
p.textContent = 'Example of asynchronous code';
}, 5000);
p.style.color = 'red';
console.log('END');
```

Now, the first line and second line of code are still synchronous here, and also we move to the first, second and third line in a Synchronous way, But here in the third line of code, we encountered the setTimeout function which will start a timer in an Asynchronous way. This means the timer will run in the background without preventing the main code from executing. And this is going to be executed after the timer has finished.

**<mark>point to remember:</mark>** Please bear in mind that callback functions alone do not make code asynchronous; this is an extremely crucial aspect to keep in mind.

**<mark>eg (i).</mark>** *\[1, 2, 3\].map(v =&gt; v\*2); // here Callbacks does not automatically make code Asynchronous.*

**<mark>eg (ii).</mark>** Moreover, just as Callback functions alone do not make code asynchronous, neither do Event Listeners. For instance, an event listener that is waiting for a button click is not working in the background. It's not doing anything; it's just waiting for a click to occur. Hence, there is absolutely no asynchronous behavior involved.

## What are AJAX calls?

**Asynchronous JavaScript And XML:** Allow us to communicate with remote web servers in an Asynchronous way with AJAX calls, we can request data from web servers dynamically.

### <mark>client-server model</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676805837676/68efb6c5-56ea-44b0-ba49-1410b6416ecc.png align="center")

In the **client-server** model, one computer serves as the server and delivers services to other computers (the clients). Clients submit requests to the server, which manages the resources, and the server fulfills those requests by providing the resources required by the clients.

### So, What is an API?

**\-&gt;** **<mark>API:</mark>** a piece of software that can be used by another piece of software, to allow applications to talk to each other.

**\-&gt;** there are many types of APIs in Web Development: like **DOM API Geolocation API, own class API, and online API**.

But now let's talk about the important type of API that we are interested in when we use AJAX and those are APIs that I like to call Online APIs.

**\-&gt; Online API:** Application running on a server, that receives requests for data, and sends data back as a response.

Some people also called it Web API as just simply API.

**\-&gt;** We can build our own Web APIs (require back-end development, eg. with node.js) or use 3rd-party APIs.

So, AJAX stands for Asynchronous JavaScript and XML. XML used to be a popular data format for transmitting data on the web, but these days most APIs don't use XML anymore. Instead, they use JSON as the preferred data format. Although AJAX is an old term that became popular in the past, it's still used today, even though we don't use XML as much. So, when you hear the term AJAX, just remember that it's referring to a way of using JavaScript to communicate with a server asynchronously, and the data is now more commonly transmitted in JSON format.

**ex:**

`{ "publisher": "101 CookBooks",`

`"title": "Best Pizza ever",`

`"social-work": 100`

`}`

So, JSON is the most popular data format today because it's just a JavaScript object, but converted to a string. And therefore it's very easy to send across the web and also to use in JavaScript once the data arrives.

All right, we now understand what Asynchronous JavaScript, AJAX, and APIs are.

**Now, let's make our first AJAX call:-**

*The syntax for creating an* ***XMLHttpRequest*** *Object:-*

<mark>const request = new XMLHttpRequest();</mark>

*For sending a request to a server, we use the open() and send() methods of the XMLHttpRequest object:*

<mark>request.open('GET', 'https://restcountries.com/v2/all');</mark>

<mark>request.send()</mark> ;

this AJAX call that we just send off here, is being done in the background while the rest of the code keeps running. And this is Asynchronous behavior.

<mark>request.addEventListener('load', function() { });</mark>

By using the 'load' event Listener, we are waiting for that event. As soon as the data arrives this callback function will be executed.

***combing them for a better understanding:***

```javascript
const request = new XMLHttpRequest('GET', 'https://restcountries.com/v2/all');
request.send();
request.addEventListener('load', function() {
    const data = JSON.parse(this.responseText);
    console.log(data);
});
```

**<mark>Note:</mark>** ***responseText returns the text received from a server following a request being sent.***

we need to convert the data in because we received the data in JSON and it is a big string of text. So, we converted it into a JS object.

## Now, let's learn about a modern JavaScript feature called Promises.

promises are <mark>ES6</mark> features, so they become available in 2015. So, they are now widely used by everyone.

### What are Promises?

**\-&gt; <mark>Promise:</mark>** An object that is used as a placeholder for the future result of an Asynchronous operation.

**\-&gt;** Now, we no longer need to rely on events and callbacks passed into Asynchronous functions to handle Asynchronous results.

**\-&gt;** we can chain promises for a sequence of Asynchronous operations.

**Let me make you more clear with a real-world example:**

* *<mark>Promise</mark>* that I will receive money if I guess the correct outcome.
    
* I buy a Lottery ticket(<mark>Promise</mark>) right now.
    
* The lottery draw happens Asynchronously.
    
* If the correct outcome, I receive money because It was promised.
    

### The Promise Lifecycle-

Promises work with Asynchronous operations, which means they are time-sensitive and can change over time. The cycle of a promise refers to the different states a promise can be in. In the beginning, we say that a Promise is in a **<mark>"pending"</mark>** state, which means that no value resulting from the Asynchronous task is available yet. During this time, the Asynchronous task is still working in the background.

Once the task is finished, the promise is considered "settled". There are two types of settled promises - **"fulfilled"** and **"rejected"** promises. A fulfilled promise means that the Asynchronous task is completed successfully, and the promise returns the resulting value. On the other hand, a rejected promise means that something went wrong during the Asynchronous task, and the promise returns an error instead of the resulting value. Understanding the different states of a promise is important in writing code that handles promises correctly.

So, a fulfilled Promise is a promise that has successfully resulted in a value just as we accept.

On the other hand, a rejected Promise means that there has been an error during the Asynchronous task.

These different states are very important to understand because when we use Promises in our code we will be able to handle these different states to do something as a result of either a successful Promise or a rejected one.

**<mark>Note</mark>: *A Promise is only settled once, And from there the state will remain unchanged forever. So, the promise will either be fulfilled or rejected*.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676866643976/46ec85a4-96af-441c-b2de-f938d8bb15a7.png align="center")

**Consuming Promises -**

```javascript
const getCountryData = function() {
    fetch('https://restcountries.com/v2/all').
        then(function(response) {
            return response.json();
        }).
        then(function(data) {
            console.log(data);
        });
};
```

the fetch statement is returning a promise and then we handled that promise using the **then** method. But then to read the data from the response, we need to call the **JSON** method on that response object. Now, this itself will also return a Promise and so if we then return that Promise from that method then basically all of this becomes a new promise itself. Since this is a promise we can again, call the **then** method on that. And so, then again we have a callback and this time, we get access to the data because the resolved value of this Promise here is going to be the data itself.

## Conclusion:

Using Asynchronous JavaScript is essential for creating contemporary, effective, and user-friendly online applications, it may be concluded. Developers can write code that can execute numerous tasks concurrently without preventing the execution of other programmes thanks to asynchronous programming. Because users may interact with the UI while the JavaScript code is running in the background, this makes web pages faster and more responsive.

That's all I've got, guys. Meet you in my next blog, where we will discuss how to handle rejected promises, async/await, error handling, running promises in parallel, and many other topics.

[Here is the last and ending part of my sequel. Happy reading🙂](https://manish-d-art-blogs.hashnode.dev/mastering-asynchronous-javascript-with-promises-asyncawait-and-ajax-a-guide-to-building-fast-and-efficient-web-applications-1)