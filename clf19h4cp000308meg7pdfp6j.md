---
title: "Destructuring in JavaScript: "Simplifying Access to Object and Array Values""
datePublished: Thu Mar 09 2023 15:26:02 GMT+0000 (Coordinated Universal Time)
cuid: clf19h4cp000308meg7pdfp6j
slug: destructuring-in-javascript-simplifying-access-to-object-and-array-values
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678358396680/77dd68dc-330c-4809-82a7-bc64791ca384.jpeg
tags: javascript, frontend-development, object-destructing, array-destructuring

---

Hey there!👋 Destructuring objects and arrays in JavaScript is a cool feature that lets you grab specific values from them and assign them to variables easily. It's like reaching into a bag of goodies and pulling out just what you need! This feature helps make your code shorter and more readable because you don't have to write as much code to get the values you want.

Destructuring also makes working with nested objects and arrays less of a headache. Before this feature was available, getting values from nested data structures was a real pain, but now it's a breeze! Plus, it simplifies function arguments by letting you pass in an object and grab the values you need inside the function.

So, in short, destructuring in JavaScript is a handy tool that makes your life as a developer easier. It saves time and makes your code easier to read, which is always a good thing!👏

## <mark>Destructuring in Arrays:-</mark>

```javascript
const arr = [1, 2, 3];

//retrieving without destructuring
const x = arr[0];
const y = arr[1];
const z = arr[2];

//retrieving with destructuring
const [a, b, c] = arr;
console.log(a, b, c); // 1  2  3
```

So in both ways, we can retrieve the values of the array and we should go for destructuring rather than repeating the same lines.

And with destructuring, we can declare all the variables that we gonna need. On the left side, we have used square brackets and these brackets are used in destructuring arrays. In it the elements of the order matter. So in `const [a, b, c] = arr;` a is 1, b is 2 and c is 3.

And yeah! it is looking like an array but actually, it's not. When **JS** sees this destructuring sign on the left side then it knows it should do destructuring.

**Note:-** Original array is not destroyed in this process

### Destructuring also follows the order:-

When using array destructuring, the variables are assigned values based on their position in the array. For example

```javascript
const arr: [1, 2, 3, 4];
const [x, y] = arr;
console.log(x, y); // 1  2
```

Now we want to retrieve the first and the third element of the array

```javascript
const arr = [1, 2, 3, 4];
const [x, , y] = arr;
console.log(x, y); // 1  3
```

so you just have to put an extra comma for skipping the element.

### Swapping array elements using destructuring

```javascript
let x = 1;
let y = 2;

let temp = x;
x = y;
y = temp;
console.log(x, y) // 2 1
```

Earlier we used to do swapping like this and also requires a temporary variable and many lines of code. But thanks to the destructures with destructuring we can do this in a line.

```javascript
let x = 1;
let y = 2;
[x, y] = [y, x]
console.log(x, y) // 2  1
```

we don't need to declare the variable again for `[x, y] = [y, x]` because it has been already declared.

### Creating immediate variables returned by a function

```javascript
const name = function(fname, lname) {
  const firstname = fname;
  const lastname = lname;
  return [firstname, lastname];
}

console.log(name('manish', 'mandal')); // [ 'manish', 'mandal' ]

const [x, y] = name('manish', 'mandal');
console.log(x, y); // manish mandal
```

For creating immediate variables make sure the function should return the values in the array so that we can destructure it. Also, it is a very handy way of immediately creating variables.

### Working with nested array

```javascript
const nestedArr = [1, 2, [3, 4]];
const [x, , y] = nestedArr;
console.log(x, y); // 1  [3, 4]
```

So, you can see that it is working the same as a simple array. Now, what if we wanted the individual values of a nested array? then we have to do destructuring inside of destructuring. However, it is sounding complicated but actually, it is not.

```javascript
const nestedArr = [1, 2, [3, 4]];
const [x, , [y, z]] = nestedArr;
console.log(x, y, z); // 1 3 4
```

that is how nested array works in destructuring.

### Default value

let's assume we don't know the length of the array and we want to retrieve each element.

```javascript
const arr = [1, 2, 3];
const [x, y, z, q] = arr;
console.log(x, y, z, q) // 1 2 3 undefined
```

so, we got undefined for the value of **q** and that is because our arr has only 3 elements and **q** is retrieving the 4th element which is not possible.

So, to get rid of this **undefined** we can set the default value of the variable and the default value will be applicable when no element is referring to its index.

```javascript
const [x, y, z, q = 99] = arr;
console.log(x, y, z, q); // 1 2 3 99
```

and that is how default value works.

## <mark>Destructuring Objects:-</mark>

Let us discuss destructuring in objects. so we use curly braces to destructure objects and we need to write the exact property name that is in the object to extract values. Also, the order of elements does not matter in objects so we don't manually need to skip the elements as we have done in Arrays.

`const person = { name: "Manish", country: "India", hobby: "coding", }`

So, earlier we used to do like this 👇

`const name = person.name;`

`const country = person.country;`

`const hobby = person.hobby;`

that was taking too much time repeatedly doing the same thing. So, to avoid this let's now use destructuring.

```javascript
const person = {
  name: "Manish",
  country: "India",
  hobby: "coding",
}
const {name, country, hobby} = person;
console.log(name, country, hobby);  // Manish India coding
```

did you see how easy it is, and yeah also we got our desired output. So, this was the fundamental of destructuring objects

**<mark>Application:</mark>** when we deal with the result of an API call to get data from another web application because their data are in objects and that is why destructuring objects will be helpful here.

### Variable names for the properties

Now, we want variables for properties so how can we do that? Let's see

```javascript
const person = {
  name: "Manish",
  country: "India",
  hobby: "coding",
}

const {name: NAME, country: COUNTRY, hobby: HOBBY} = person;
console.log(NAME, COUNTRY, HOBBY); // Manish India coding
```

here NAME, COUNTRY and HOBBY are the variable names and name, country and hobby are the properties basically on the left is the property and on the right, it is the variable name.

### Default value

Let us assume some properties are not there and we are trying to retrieve them and we got undefined. So, to get rid of this we can set a default value for that property just as we did in the array.

```javascript
const person = {
  name: "Manish",
  country: "India",
  hobby: "coding",
}

const {name, country, hobby, college={}} = person;
console.log(name, country, hobby, college); //Manish India coding {}
```

So, the college property is not in the person object which is why we got an empty **{}** this empty **{}** we got because we have set a default value for the college and we can also combine like this `name: NAME={}`

### Mutating Variables

```javascript
let a = 1;
let b = 2;
const obj = {a: 99, b: 77, c: 14};
console.log(a, b); // 1  2
```

Now we want that **a, b** should override the value of **a, b** in **obj** for that we need to do destructuring inside parenthesis. If no then it is going to give an error.

```javascript
let a = 1;
let b = 2;
const obj = {a: 99, b: 77, c: 14};
({a, b} = obj);
console.log(a, b); // 99  77
```

### Nested Objects

```javascript
const obj = {
  name: "manish",
  hobbies: {
    games: "cricket",
    moreGames: {a: "hockey", b: "volleyball"},
  },
  country: "India",
}

const {name, hobbies, hobbies: {games}, hobbies: {moreGames}, hobbies:{moreGames:{a, b}}, country} = obj;
console.log(name);  //manish
console.log(hobbies) //{ games: 'cricket', moreGames: { a: 'hockey', b: 'volleyball' } }
console.log(games);  //cricket
console.log(moreGames); //{ a: 'hockey', b: 'volleyball' }
console.log(a, b);  //hockey volleyball
console.log(country); //India
```

And this is how nested objects work. Let us understand, so, in **obj** we have hobbies as object and in it **moreGames** is also an object and you can see how we have destructured it. Till now I guess you must have got ideas about how to destructure objects.

### Default Value

working with default values is same as in Arrays. I don't think we need to discuss again how default values work. So, without wasting time let's put our thought into action.

```javascript
const obj = {
  name: "manish",
  hobbies: {
    games: "cricket",
  },
  country: "India",
}

const {name, hobbies:{games} = {}, country, petName = {}} = obj;
console.log(name); // manish
console.log(petName) // {}
console.log(games); // cricket
console.log(country); // India
```

### Passing object into function destructure it

Sometimes we have to deal with functions with lots of parameters and it can be hard to know the order of parameters for someone using this function. And so instead of defining the parameters manually, we are going to just pass an object into the function as an argument and the function will then immediately destructure that object. You can also use here default value concept to get rid of undefined.

```javascript
const obj = {
  name: "manish",
  hobbies: {
    games: "cricket",
  },
  country: "India",
}

const func = function({name, hobbies:{games = {}} = {}, country, petName = "mani"}) {
console.log(name);  // manish
console.log(petName); // mani
console.log(games); // cricket
console.log(country); // India

}

func(obj)
```

Here in the object obj, there are no property names **petName** and we have set a default value for it.

### conclusion:

So there you have it, folks!✨ Destructuring in JavaScript is a pretty cool trick that can make your code simpler and easier to read. It lets you pull out values from arrays and objects and assign them to variables all in one shot. This saves you time and effort and makes your code look neater. So next time you're coding in JavaScript, give destructuring a shot and see how much easier your life can be!