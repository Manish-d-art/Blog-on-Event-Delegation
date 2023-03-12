---
title: "Spread and Rest operators in JavaScript: "Unlocking power of JavaScript""
datePublished: Sun Mar 12 2023 18:18:54 GMT+0000 (Coordinated Universal Time)
cuid: clf5pyz9q00010amh2jn7c1pc
slug: spread-and-rest-operators-in-javascript-unlocking-power-of-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678644873602/fc4dd679-fbb3-43f7-9653-7cfe00246560.png
tags: javascript, frontend-development, rest-operator, spread-operator

---

Hello fellow developers!👋 In this blog post, we're going to explore two powerful operators in JavaScript that you may have heard of: the spread operator and the rest operator.

As developers, we're always looking for ways to write cleaner, more efficient code, and these operators can help us achieve just that. With the spread operator, we can easily concatenate arrays or merge objects, while the rest operator allows us to handle an arbitrary number of arguments more elegantly.

Whether you're working on a personal project or collaborating with a team, understanding how these operators work and how to use them effectively can help you write more concise and maintainable code.

So, let's dive into the world of spread and rest operators in JavaScript and see how they can help take our coding skills to the next level!

## **Working with Spread Operator in Arrays:-**

Let's say we have an Array 👇

`const arr = [9, 10, 1, 5, 6];`

Earlier we used to loop over the array and print each element. But now with the help of the Spread operator, this can be done very easily we only have to write this statement and individual elements are printed 👇

`console.log(...arr);`

output:- 0 10 1 4 6

```javascript
const arr = [9, 10, 1, 5, 6];
console.log(...arr); 

// 0 10 1 4 6
```

### Merging Arrays:-

Now we want to create a new Array based on this array with some more elements. So let's see how we can do this

```javascript
const arr = [3, 4, 5];
const newArr = [...arr, 6, 7];
console.log(newArr);

// [3, 4, 5, 5, 6, 7]
```

and this is how we can do this.

**<mark>Point to Remember:-</mark>** If you don't specify the three dots as prefixes before then the `arr` will be inside `newArr` just like this 👇

`[Array(3), 6, 7]`

### Copying elements of more than one Array into a new Array:-

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const arr3 = [7, 8, 9];
const newArr = [...arr1, ...arr2, ...arr3];
console.log(newArr);

// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

So, here we expanded all the 3 arrays into the `newArr` and that's how we can copy the array with the use of the **spread** operator.

### Working with function Argument:-

The spread operator `...` can also be used in function arguments to pass an array as separate arguments to a function.

```javascript
const add = function(a, b, c, d) {
    return a + b + c + d;
}

const arr = [1, 2, 3, 4];
const res = add(...arr);
console.log(res);

//  10
```

In this example, the spread operator is used to pass the `arr` array as separate arguments to the `add()` function. This is equivalent to calling the function with the individual elements of the array, like this:👇

`const res = add(1, 2, 3, 4)`

**<mark>Point to Remember:-</mark>** We can use the spread operator only in iterables like arrays, sets, maps, and Strings but not with objects because, In JavaScript, Objects are not iterable by default.

Let's see what happens when we try to use the spread operator in objects

```javascript
const obj = {name: "john"};
const arr = [...obj];

//  TypeError: object is not iterable
```

So, you can see as I mentioned object is not iterable, hence we can't use the spread operator in objects.

### Concatenating of Array:-

Earlier we, use to use `concat()` and this `concat()` function can take one or more arguments, each of which can be an array or a value. If the argument is an array, its elements are concatenated to the new array. If the argument is a value, it is appended to the new array as a single element.

```javascript
let arr1 = [10, 12, 21];
const arr2 = [13, 14, 15];
arr1 = arr1.concat(arr2);
```

Now we will see the same thing how we can achieve with **spread** operator

```javascript
let arr1 = [10, 12, 21];
const arr2 = [13, 14, 15];
arr1 = [...arr1, ...arr2]
console.log(arr1);

// [10, 12, 21, 13, 14, 15]
```

In this example, we first declare two arrays `arr1` and `arr2`. We then use the spread operator to concatenate these arrays into arr1. The `arr1` contains all the elements of `arr2` and also its elements.

## **Working of spread operator in Strings:-**

In JavaScript, the spread operator `...` can also be used with strings to convert them into arrays of individual characters. This can be useful when you need to manipulate the characters of a string as individual elements.

Here is an example👇

```javascript
const str = 'Manish';
const strArr = [...str];
console.log(...strArr);

// ['M', 'a', 'n', 'i', 's', 'h']
```

So, we got an array of letters of the String `str`.

You can also use the spread operator with template literals to create a string from an array of characters. Here is an example👇

```javascript
const arr = ['M', 'a', 'n', 'i', 's', 'h'];
const str = [...arr].join('');
console.log(str);

// Manish
```

In this example, we declare an array `arr` that contains the individual characters of the word **"Manish"**. We then use the spread operator to create a copy of the array and use the `join()` function to concatenate the characters into a string. The resulting string is stored in a variable called `str`, which contains the value **"Manish"**.

### **We can also print the individual letter of a String using the spread operator**

```javascript
const name = "Manish";
console.log(...name);

// M a n i s h
```

<mark>Point to remember:-</mark> we cannot do this 👇

```javascript
console.log(`${...name}`);
```

we will face a `Syntax error: unexpected token.`

## **Working of Spread operator in Objects:-**

So, since **ES 2018**, the spread operator also works on objects even though objects are not iterable.

Now we try to create a new object with some other object.

For example, you have an object `person` with properties such as `name`, and `gender`. If you want to create a new object with all the properties of `person`, you can use the spread operator as follows:

```javascript
const person = {name: "Manish", gender: "male"};
const newObj = {...person, age: 20};
console.log(newObj);

//  { name: 'Manish', gender: 'male', age: 20 }
```

In this example, the spread operator `...` is used to merge the properties and values of `person` into a new object `newObj`. The resulting object contains all the properties and values of both objects.

### **copying objects with the use of the spread operator:-**

**<mark>point to remember:- </mark>** It's important to note that the spread operator creates a shallow copy of the object, meaning that if the object has nested objects or arrays, they will be copied by reference rather than by value. If you need to create a deep copy of an object, you should use a library or function specifically designed for that purpose.

```javascript
const obj = {name: "Manish", country: "India"};
const copyObj = {...obj};
copyObj.name = "jack";
copyObj.country = "UK";

console.log(obj);
// { name: 'Manish', country: 'India' }

console.log(copyObj);
//  { name: 'jack', country: 'UK' }
```

So, this is a shallow copy as the change in `copyObj` is not reflected in the original object. That means we have successfully copied an object because we know that changing one object would then also change the other one.

## **Rest Pattern and Rest Parameters:-**

Now let's talk about Rest \`**Pattern\`** and \`**Rest\`** Parameters.

So, Rest \`**Pattern**\` and Rest parameters are a way of handling multiple values in JavaScript. They are denoted by three dots(...) and allow you work with an arbitrary no. of arguments or elements as an array. So, it's just the opposite of the Spread operator.

**<mark>point to remember:- </mark>** the spread is always on the right of `=`. while the Rest pattern is going to be used on the left of `=`.

Do you remember, that we used the Spread in building the new Array and to pass multiple values into a function in both processes we have expanded an array into individual elements also, the rest pattern uses the same syntax to collect multiple elements to form an array and that is opposite of spread.

### Working and Identification of the Rest and Spread

`const arr1 = [1, 2, ...[3, 4]];`

So, here we have used the Spread operator and this is because we have `...` on the `=` of it.

`const [a, b, ...others] = [1, 2, 3, 4, 5];`

here we have used the Rest operator because the operator `...` is on the left side of `=`. Ans also a is 1, b is 2 and rest all the elements in others in the form of an array.

**<mark>Point to remember:-</mark>** The Rest operator should always be the last element. let's try if the Rest operator is not the last element.

`const [a, b, ...others, c] = [1, 2, 3, 4, 5]`;

When you run this code you may get

`Syntax Error: Rest element should be the last element`

And this is because the `Rest` operator takes all the rest elements and forms an array and in the above code we are retrieving the value of **c** but there is no element left which is why there syntax Error. So, there can be only one Rest operator in destructuring Assignment please keep this in mind.

### Working with functions using Rest Parameter

```javascript
function func(a, b, ...rest) {
    console.log(a);
    console.log(b);
    console.log(rest);
}

func(1, 2, 3, 4, 5, 6);

// 1
// 2
// [3, 4, 5, 6]
```

the last parameter prefixed with `...`, which will cause all remaining parameters to the placed within an array.

**<mark>Point to remember:-</mark>**

`` `function func(...rest1, ...rest2) {}` // wrong way ``

`` `function func(...rest1, a, b) {}` wrong way ``

A function definition can only have one last **Rest** parameter, and the Rest parameter must be the last in the function definition Otherwise there will be a syntax Error.

**What if only one argument is passed**

```javascript
function func(a, b, ...rest) {
    console.log(a);
    console.log(b);
    console.log(rest);
}

func(1);

// 1
// undefined
// []
```

So, `b` gets the undefined default value and the `rest` is an empty array.

### **Finding the length of the arguments**

```javascript
function findLength(...rest) {
    console.log(rest.length);
}

findLength()  // 0
findLength(1); // 1
findLength(1, 2, 3, 4);  // 4
```

Here in this way, we can also find the length of the arguments.

## Conclusion:-

In conclusion, if you're looking to level up your JavaScript skills, you should definitely take some time to learn about rest and spread operators. They might seem a little intimidating at first, but once you get the hang of them, they'll become your new best friends when it comes to manipulating arrays and objects.

Just remember that these operators can be used in a variety of ways and can really help you write cleaner, more efficient code. So don't be afraid to experiment with them and see how they can improve your JavaScript projects. Who knows, you might just end up surprising yourself with what you're able to accomplish!

*That's all for now, folks! I🙂 hope you found this blog helpful and informative. If you have any questions or comments, feel free to leave them below.*

*Remember, rest and spread operators are just one tool in your JavaScript toolbox, but they can be a game changer when it comes to working with complex data structures. So don't be afraid to give them a try and see how they can make your code more efficient and readable.*

*Thanks for reading🤩, and happy coding!✨*