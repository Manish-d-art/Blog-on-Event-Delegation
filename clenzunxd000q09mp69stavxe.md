# "Mastering Asynchronous JavaScript with Promises, Async/Await and AJAX: A Guide to Building Fast and Efficient Web Applications"

Hey there!🙋‍♂️ Thanks for joining me for the sequel of my blog. If you missed my previous post, no worries at all! You can simply visit this link to catch up before we continue on our journey together. I'm excited to have you here, so let's dive right in!

[Here's the link to the first part of our sequel, so you can easily find it and catch up before we move forward together. Happy reading :)](https://manish-d-art-blogs.hashnode.dev/mastering-asynchronous-javascript-with-promises-asyncawait-and-ajax-a-guide-to-building-fast-and-efficient-web-applications)

let's continue our Asynchronous JavaScript💥

## Handling rejected Promises:-

So, when a user loses their internet connection this is the only way in which fetch Promise rejects. And that error we will handle here.

Alright, let's put our plan into action and see what happens! I'm excited to see how everything plays out. Let's get started!

Let's try something out - first, we'll simulate the page loading up completely. After that, we'll mimic a user trying to request without an internet connection, and then we'll see the error that occurs. Are you ready to give it a try?

Imagine we have a button on our page, that the user can click on to request some data.

```javascript
const btn = document.querySelector('.btn);

const getCountryData = function() {
    fetch('https://restcountires.com/v2/all').
        then(response => response.json()).
        then(data => { console.log(data);
       });
}

btn.addEventListener('click', getCountryData);
```

Awesome! So, when you clicked the button, everything worked smoothly, and the data was displayed without any hiccups. That's great! It's always a relief when things work as expected👏.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677474555138/78776030-df6e-4924-b512-3775f210b307.png align="center")

But now watch what happens when we set ourselves offline 👇

<mark>press F12 --&gt; network --&gt; online --&gt; offline</mark>

let's go to the console and now when we do the request, then we get these errors 👇

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677474959273/154efd01-bf79-4b16-8894-cda91c5dc006.png align="center")

Oh no, it looks like we have an **uncaught Promise**. The reason for this is that we attempted to fetch some data, but unfortunately, it wasn't successful. This means that the Promise that was returned from the fetch function was rejected. But don't worry - we can figure out what went wrong and make the necessary adjustments to handle it properly.

### **There are two ways of handling rejections:-**

**and the first one is to pass a second callback function into the then method**. So, the first callback function is always gonna be called for the **fulfilled Promise**(for a successful one) But we can also pass a second callback function which will be called when the promise was **rejected**. So, let's do that

```javascript
const btn = document.querySelector('.btn);

const getCountryData = function() {
    fetch('https://restcountires.com/v2/all').
        then( response => response.json(),
        err => console.log(err)
        ).
        then(data => { console.log(data);
       });
}

btn.addEventListener('click', getCountryData);
```

now, reload the page and again lose the connection and do the request.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677476825250/d65d46cd-36ec-4ee1-b8a3-956321667281.png align="center")

\*\*Great job!\*\*👏 You successfully handled the error by using an alert function to notify the user about the issue. As a result, the error message that was previously displayed in the console is no longer there because you caught the error using the **alert**.

**<mark>note:-</mark> we can chain the Promises and so we will need more no. of callback functions for the handling of errors.**

In programming terms, handling an error is the same as catching an error. It means that you have implemented a solution to prevent the error from causing problems in the program.

**the second one and the better way of handling errors globally just in one central place.**

So, instead of callback functions just having one callback in the **then** and then instead we can handle all the errors, no matter where they appear in the chain, right at the end of the chain by adding a **catch** method.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677477814361/ab8b767f-30a4-426a-acce-82b968fa444e.png align="center")

All right, So this **catch** method here at the end of the chain will catch any errors that occur in any place in this Promise. So, the error will propagate down the chain until they are caught.

**<mark>note</mark>:- In a real application with a user interface, it's important to provide a good user experience by displaying error messages instead of just logging them to the console. Therefore, instead of only logging errors, you should create a method that can display error messages to the user. This method could take a string parameter containing the error message and present it in a way that's easy for the user to understand. By doing so, you can ensure that users are informed about any issues that may occur and can take appropriate action.**

and that is how we handle errors there is one more quick method that I want to show and that is also available on all promises besides then and catch there is also a "**finally**" method. So, let's add the "**finally**" method here, And this callback function will always be called whatever happens with the Promises so, no matter if the Promise is fulfilled or rejected this "**finally**" method is always gonna be called.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677482951261/4acc5270-20d0-4903-a4ba-224251f28fe5.png align="center")

`finally()` is a great way to perform some cleanup or finalization logic, such as closing a database connection or releasing a resource. So, don't forget to use it when working with promises!

## Throwing Error Manually:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677483332828/4f1f32c0-9cbc-46e2-99d5-0e1e9a4dd6fc.png align="center")

Now we can see that We've encountered a **404 error** while making a fetch call to our API for retrieving countries. This error occurs when the server cannot find the requested resource.

But still, even though there is a big problem with this request, the `fetch()` function did not **reject** the Promise as expected. This behavior has confused many developers, including myself, who believe that the Promise should be rejected automatically in this case. But it doesn't and so we will have to do it manually.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677483949572/a34fbb8a-b3fd-4587-8232-df660ab3a167.png align="center")

Now in the above picture, you can see that the **<mark>"ok"</mark>** property is set to **<mark>false</mark>** and the reason for that is the s\*\*<mark>tatus code "404"</mark>\*\*. But when a request goes well, the **<mark>"ok"</mark>** is **<mark>true</mark>** and the **<mark>status code is "200.</mark>**

And now, we can reject Promise manually when the "ok" property is false.

```javascript
const btn = document.querySelector('.btn');

const getCountryData = function() {
    fetch('https://restcountries.com/v2/all12').
        then(response =>{
          console.log(response);
          if(!response.ok) throw new Error(`something went wrong      (${response.status})`);
          return response.json();
        }).
        then(data => { console.log(data);
       }).catch(err => alert(err));
}

btn.addEventListener('click', getCountryData);
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677485112178/e58ce503-7e87-46ef-aa48-e26cc021e294.png align="center")

throwing an error in any of these **"then"** methods will result in rejected Promise. So the Promise returned by this then the handler will be rejected Promises👇

`.then(response => {`

`console.log(response);`

`if(!response.ok) throw new Error('something went wrong (${reponse.status}));`

`return response.json();`

`});`

And that rejection will propagate down to **catch** the handler which we already have set up there.

## The Event Loop(Asynchronous behind the scenes):-

Now let's about the **event loop**, The **event loop** is a crucial part of how JavaScript works. It enables JavaScript to execute asynchronous tasks, like fetching data from a server or waiting for user input, without halting the main thread.

<mark>Here's how it works</mark>: the event loop monitors the call stack and message queue constantly. Whenever the call stack becomes empty, the event loop checks the message queue for any pending messages or events, like a timer expiring or an HTTP request completing. If there are any messages in the queue, the event loop pushes them onto the call stack for execution. This process keeps running indefinitely, allowing JavaScript to handle asynchronous tasks in a non-blocking manner.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677488623700/ce80a273-c1be-465c-a8a9-d1f17f85ba29.gif align="center")

**there are two types of queues** one is a <mark>callback queue</mark> and the other one is a <mark>microtask queue</mark>.

The **microtask queue** is given higher priority than the event queue, which means that any tasks in the microtask queue will be executed before the next task from the event queue is picked up. This ensures that critical tasks, such as updating the UI after a user interaction or handling errors in Promises, are executed as soon as possible. It can also starve the callback Queue.

```javascript
console.log('Test start');
setTimeout(() => console.log('0 sec timer'), 0);
Promise.resolve('resolved Promise 1').then (
    res => console.log(res)
)
Promise.resolve('resolved Promise 2').then (
  res => {
    for (let i = 0; i < 10000; i++) {}
    console.log(res);
  }
)
console.log('Test End');
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677489809392/fceda074-aacf-43aa-96e7-0495f3b7cf81.png align="center")

**In this example**, the synchronous code is executed first and after that Asynchronous code, due to the priority of the microtask Queue over the callback queue the priority queue is executed first and after that the callback Queue.

## Building Promises from scratch:-

We've only talked about consuming Promises so far, but we've never actually built our own. So let's get started 👍.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Do some asynchronous operation
  let result = Math.random() * 100;
  
  // Simulate a delay
  setTimeout(() => {
    if (result < 50) {
      reject('Error: Result is less than 50');
    } else {
      resolve(`Success: Result is ${result}`);
    }
  }, 2000);
});

myPromise
  .then((result) => console.log(result))
  .catch((error) => console.log(error));
```

We use the `new Promise()` constructor to create a Promise, which represents an asynchronous operation that will produce a result sometime in the future. We pass a function to this constructor that takes two arguments: `resolve` and `reject`.

Inside this function, we simulate the Asynchronous operation, which generates a random number and returns a success message if the number is greater than or equal to 50, or an error message if it is less than 50.

We use the `resolve` and `reject` functions to signal the outcome of the operation. If everything went well, we call `resolve` with the result. If there was an error, we call `reject` with an error message.

After creating the Promise, we use the `.then()` method to specify what should happen if the Promise is resolved successfully. We pass a function to this method that will be called with the result of the operation. In this example, we log the result to the console.

We also use the `.catch()` method to specify what should happen if the Promise is rejected. We pass a function to this method that will be called with the error message. In this example, we log the error to the console.

So basically, we use the `.then()` and `.catch()` methods to handle the result of the Promise once it's finished. If the Promise is resolved successfully, we execute the function passed to `.then()`. If it's rejected, we execute the function passed to `.catch()`.

**Now finally there is also a way to create a very easily <mark>fulfilled or a rejected Promise</mark> immediately:-**

We can create a Promise that is already fulfilled or already rejected using two static methods: `Promise.resolve()` and `Promise.reject()`.

We've actually already used this feature in the previous example! In that example, we simulated an asynchronous operation using a delay and a random number generator, but we could have also used `Promise.resolve()` and `Promise.reject()` to create a Promise that is immediately fulfilled or rejected.

To create an immediately fulfilled Promise, we can call `Promise.resolve()` with the result we want to pass. To create an immediately rejected Promise, we can call `Promise.reject()` with the error message we want to pass.

So basically, we can use `Promise.resolve()` and `Promise.reject()` to create a Promise that is already resolved or rejected without having to simulate an asynchronous operation.

```javascript
//resolving Promise
Promise.resolve('resolved').then( res => console.log(res));

//rejecting Promise
Promise.reject(new Error('rejected')).catch( err => console.log(err));
```

## Consuming Promises with async and await:-

Async/ await, introduced in **ES 2017**, is a newer, better, and simpler approach to consuming promises.

To work with <mark>async/awai</mark>t we need to create a special kind of function and that is the async function and which is very easy to create we simply just have to write async just before the function. And this function is now an Asynchronous function.

here is a sample loop👇

`const getCountryData = async function() {}`

And inside the async function, we can have more than one await statement.

here is a look of the await statement👇

`const res = await fetch('API_URL');`

And this statement is going to return a Promise. one more thing is that the "**await**" keyword in this statement is waiting for the result of this Promise. And so basically await will stop execution at this point of the function until the Promise is fulfilled. <mark>Now coming to your question isn't stopping the code</mark>, blocking the execution? And the answer is **NO** because stopping execution in an async function is not a problem because the function is running in the background Asynchronously and this is the reason it's not blocking the main thread of execution. And so it's not blocking the call stack.

This is the special feature of await, which makes our code appear to be typical synchronous code even if everything is actually synchronous in the background.

Now as soon as the Promise is resolved then the value of this whole await expression that we have here is going to be the resolved value of the Promise. So, we can store it in a variable.

`const res = await fetch('API_URL');`

previously we had to return this Promise and then chain another then handler but now all we have to do is to await this and then we can store the results directly into the data.

`const data = await res.json();`

```javascript
const getCountryData = async function() {
    const res = await fetch('https://restcountries.com/v2/all');
    const data = await res.json();
    console.log(data);
}
```

And so now we have all of this in one nice async function that runs behind the scenes until everything is finished. Also, **async/awai**t is actually used a lot more than traditional **then** methods of consuming Promises.

## Error Handling in async/await with try and catch:-

In async/await we don't have catch method like we have been using instead we have something called **try/catch.** It's been in the language since the very beginning. So, **try/catch** has nothing to do with the async/await. But still, we can use it to catch errors in async functions.

So, we can put our whole code in the **try** block and it will be executed like the normal code. On the other hand, we have a **catch** block that will have access to whatever error occurred in the try block. And now, whatever you can do with this error whether you want to display or alert it.

```javascript
const getCountryData = async function() {
try {
    const res = await fetch('https://restcountries.com/v2/all');
    const data = await res.json();
    console.log(data);
    } catch(err) {
        alert(err);
    }
}
```

Now, Actually I don't think that I need to explain more about error handling here because we have previously discussed it very well. So, there is advice for you that never ignore handling errors in Asynchronous code especially.

**<mark>Note:-</mark>**

**i)** Async function always returns a Promise and again you have to handle this Promise with **then** handler.

**ii)** If there is an error in the async function, the Promise that the async function will returns is still fulfilled and not rejected. So, we can add a **catch** handler after the **then** method. So, that we can handle the **error**.

## Multiple Promises in parallel with Promise.all() method:-

This **Promise.all()** method takes an array of promises and returns a new Promise that resolves when all the **Promises** in the array have resolved. The resolved value of the new Promise is an array of the resolved values of the original array. All the Promises will run at the same time.

```javascript
const getJSON = function (url, errorMsg = 'Something went wrong') {
  return fetch(url).then(response => {
    if (!response.ok) throw new Error(`${errorMsg} (${response.status})`);

    return response.json();
  });
};

const get3Countries = async function (c1, c2, c3) {
  try {
    const data = await Promise.all([
      getJSON(`https://restcountries.com/v2/name/${c1}`),
      getJSON(`https://restcountries.com/v2/name/${c2}`),
      getJSON(`https://restcountries.com/v2/name/${c3}`),
    ]);
    console.log(data.map(d => d[0].capital));
  } catch (err) {
    console.error(err);
  }
};
get3Countries('portugal', 'canada', 'tanzania');
```

But whenever any one of the Promises rejects, then the whole Promises get rejected as well. It can also be said that Promise.all short circuits when any Promise rejects. You can also use \`then\` and catch with Promise.all

You can use this **Promise.all** whenever you need multiple Asynchronous operations without depending on each other **APIs.**

## Using Promise.race() :-

Now, let's continue heading toward Promise.race(), In the `Promise.all()` method, you will receive an array of results from all the promises when all of them get resolved successfully. So you can process all the results at once.

On the other hand, the `Promise.race()` method works differently. It returns a new Promise that settles as soon as any of the promises passed to it settles, regardless of whether the Promise was fulfilled or rejected. This means that if any Promise resolves or rejects before the others, it will be returned as the result of the `Promise.race()` method. So, you can use `Promise.race()` when you only need the result from the first resolved Promise and want to skip the others.

And this is clear that the first settled Promise wins the race.

```javascript
const getJSON = function (url, errorMsg = 'Something went wrong') {
  return fetch(url).then(response => {
    if (!response.ok) throw new Error(`${errorMsg} (${response.status})`);

    return response.json();
});

(async function () {
  const res = await Promise.race([
    getJSON(`https://restcountries.com/v2/name/egypt`),
    getJSON(`https://restcountries.com/v2/name/italy`),
    getJSON(`https://restcountries.com/v2/name/mexico`),
  ]);
  console.log(res[0]);
})();
```

So, In this, we get only one result not an array of the results. And the Promise that gets rejected can also win the race and so we can say that Promise.race short circuits whenever one of the Promises gets settled. And that means no matter if fulfilled or rejected.

## Using Promise.allSettled():-

The `Promise.allSettled()` method is similar to `Promise.all()`, but with a key difference: it waits for all the promises to settle, regardless of whether they are resolved or rejected. This means that even if some of the promises fail, you will still get results for all the promises.

Here's an example of how to use `Promise.allSettled()`:

```javascript
const promises = [
  Promise.resolve('Success!'),
  Promise.reject('Oops!'),
  Promise.resolve('Another success!')
];

Promise.allSettled(promises)
  .then(results => {
    results.forEach(result => {
      if (result.status === 'fulfilled') {
        console.log(`Promise resolved with result: ${result.value}`);
      } else {
        console.error(`Promise rejected with error: ${result.reason}`);
      }
    });
  });
```

In this example, we have an array of three promises: one that resolves successfully, one that rejects with an error, and another that also resolves successfully. We pass this array of promises to `Promise.allSettled()`, which returns a new Promise that resolves with an array of objects. Each object represents the result of one of the input promises and includes a `status` property indicating whether the Promise was fulfilled or rejected, and a `value` or `reason` property with the result or error, respectively.

In the `then()` method, we loop through the array of results and check the `status` property of each object to determine whether the Promise was fulfilled or rejected. We then log the result or error accordingly.

## Using Promise.any:-

The `Promise.any()` method is a new addition to JavaScript, and it's pretty cool. It allows you to pass an array of promises to it and returns the result of the first resolved Promise, whether it was fulfilled or rejected. This is different from `Promise.race()`, which returns the result of the first Promise that settles, regardless of whether it was fulfilled or rejected.

Here's an example of how to use `Promise.any()`:

```javascript
const promises = [
  Promise.reject('Oops!'),
  Promise.resolve('Success!'),
  Promise.reject('Another oops!')
];

Promise.any(promises)
  .then(result => {
    console.log(`The first Promise to resolve was: ${result}`);
  })
  .catch(error => {
    console.error(`All Promises were rejected with errors: ${error}`);
  });
```

In this example, we have an array of three Promises: one that rejects with an error, one that resolves successfully, and another that also rejects with an error. We pass this array of Promises to `Promise.any()`, which returns a new Promise that resolves with the result of the first resolved Promise. In this case, that is the second Promise that resolves with "Success!".

In the `then()` method, we log the result of the first resolved Promise. If all the Promises in the array are rejected, the `catch()` method will be called with an error, which we log in this case.

## Conclusion:-

In conclusion, asynchronous JavaScript is a powerful tool for building web applications that are both responsive and efficient. By allowing certain operations to run in the background while another code executes, asynchronous programming can help prevent delays and keep web pages feeling snappy and responsive.

There are several ways to implement asynchronous programming in JavaScript, including callbacks, promises, and async/await functions. Each of these techniques has its strengths and weaknesses, and the best approach will depend on the specific needs of your application.

One important thing to keep in mind when working with asynchronous JavaScript is that it can be easy to introduce bugs and errors if you're not careful. Asynchronous operations can introduce race conditions, which can cause unpredictable behavior if not handled properly.

Overall, mastering asynchronous JavaScript is an important skill for any web developer and can help you create more responsive, efficient, and user-friendly web applications.

*<mark>I hope you enjoyed reading this article as much as I enjoyed writing it✒️. Thanks for sticking around until the end🙂. You're awesome!💥 take care and happy reading!</mark>*