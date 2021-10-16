1. What's the output?
```
let c = { greeting: 'Hey!' };
let d;

d = c;
c.greeting = 'Hello';
console.log(d.greeting);
```
**Ans:** `Hello` 

In JavaScript, all objects interact by reference when setting them equal to each other. First, variable c holds a value to an object. Later, we assign d with the same reference that c has to the object. When you change one object, you change all of them.
<hr />

2. What happens when we do this?
```
function bark() {
  console.log('Woof!');
}

bark.animal = 'dog';
```
**Ans:** `Nothing, this is totally fine!`

This is possible in JavaScript, because functions are objects! (Everything besides primitive types are objects). A function is a special type of object. The code you write yourself isn't the actual function. The function is an object with properties. This property is invocable.
<hr />

3. What's the output?
```
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person('Lydia', 'Hallie');
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```
**Ans:** `TypeError`

In JavaScript, functions are objects, and therefore, the method getFullName gets added to the constructor function object itself. For that reason, we can call Person.getFullName(), but member.getFullName throws a TypeError.
If you want a method to be available to all object instances, you have to add it to the prototype property:
```
Person.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};
```
<hr />

4. What's the output?
```
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person('Lydia', 'Hallie');
const sarah = Person('Sarah', 'Smith');

console.log(lydia);
console.log(sarah);
```
**Ans:** `Person {firstName: "Lydia", lastName: "Hallie"}` and `undefined`

For `sarah`, we didn't use the `new` keyword. When using `new`, `this` refers to the new empty object we create. However, if you don't add `new`, `this` refers to the **global object!**
We said that `this.firstName` equals `"Sarah"` and `this.lastName` equals `"Smith"`. What we actually did, is defining `global.firstName = 'Sarah'` and `global.lastName = 'Smith'`. `sarah` itself is left `undefined`, since we don't return a value from the `Person` function.
<hr />

5. What's the output?
```
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log('You are an adult!');
  } else if (data == { age: 18 }) {
    console.log('You are still an adult.');
  } else {
    console.log(`Hmmm... You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```
**Ans:** `Hmmm... You don't have an age I guess`

When testing equality, primitives are compared by their value, while objects are compared by their reference. JavaScript checks if the objects have a reference to the same location in memory.
The two objects that we are comparing don't have that: the object we passed as a parameter refers to a different location in memory than the object we used in order to check equality.
This is why both `{ age: 18 } === { age: 18 }` and `{ age: 18 } == { age: 18 }` return `false`.
<hr />

6. What's the output?
```
const obj = { a: 'one', b: 'two', a: 'three' };
console.log(obj);

```
**Ans:** `{ a: "three", b: "two" }`

If you have two keys with the same name, the key will be replaced. It will still be in its first position, but with the last specified value.
<hr />

7. What's the output?
```
String.prototype.giveLydiaPizza = () => {
  return 'Just give Lydia pizza already!';
};

const name = 'Lydia';

name.giveLydiaPizza();
```
**Ans:** `"Just give Lydia pizza already!"`

`String` is a built-in constructor, which we can add properties to. I just added a method to its prototype. Primitive strings are automatically converted into a string object, generated by the string prototype function. So, all strings (string objects) have access to that method!
<hr />

8. What's the output?
```
console.log(typeof typeof 1);
```
**Ans:** `"string"`

`typeof 1` returns `"number"`. `typeof "number"` returns `"string"`
<hr />

9. What's the output?
```
function getInfo(member, year) {
  member.name = 'Lydia';
  year = '1998';
}

const person = { name: 'Sarah' };
const birthYear = '1997';

getInfo(person, birthYear);

console.log(person, birthYear);
```
**Ans:** `{ name: "Lydia" }, "1997"`

Arguments are passed by value, unless their value is an object, then they're passed by reference. `birthYear` is passed by value, since it's a string, not an object. When we pass arguments by value, a copy of that value is created.

The variable `birthYear` has a reference to the value `"1997"`. The argument `year` also has a reference to the value `"1997"`, but it's not the same value as `birthYear` has a reference to. When we update the value of `year` by setting `year` equal to `"1998"`, we are only updating the value of `year`. `birthYear` is still equal to `"1997"`.

The value of `person` is an object. The argument `member` has a (copied) reference to the same object. When we modify a property of the object `member` has a reference to, the value of `person` will also be modified, since they both have a reference to the same object. `person`'s `name` property is now equal to the value `"Lydia"`.
<hr />

10. What's the output?
```
function greeting() {
  throw 'Hello world!';
}

function sayHi() {
  try {
    const data = greeting();
    console.log('It worked!', data);
  } catch (e) {
    console.log('Oh no an error:', e);
  }
}

sayHi();
```
**Ans:** `Oh no an error: Hello world!`

With the `throw` statement, we can create custom errors. With this statement, you can throw exceptions. An exception can be a string, a number, a boolean or an object. In this case, our exception is the string `'Hello world!'`.

With the catch statement, we can specify what to do if an exception is thrown in the `try` block. An exception is thrown: the string `'Hello world!'`. `e` is now equal to that string, which we log. This results in `'Oh an error: Hello world!'`.
<hr />

11. What's the output?
```
function Car() {
  this.make = 'Lamborghini';
  return { make: 'Maserati' };
}

const myCar = new Car();
console.log(myCar.make);
```
**Ans:** `"Maserati"`

When you return a property, the value of the property is equal to the returned value, not the value set in the constructor function. We return the string `"Maserati"`, so `myCar.make` is equal to `"Maserati"`.
<hr />

12. What's the output?
```
const name = 'Lydia';
age = 21;

console.log(delete name);
console.log(delete age);
```
**Ans:** `false`, `true`

The `delete` operator returns a boolean value: `true` on a successful deletion, else it'll return `false`. However, variables declared with the `var`, `const` or `let` keyword cannot be deleted using the `delete` operator.
The `name` variable was declared with a `const` keyword, so its deletion is not successful: `false` is returned. When we set `age` equal to `21`, we actually added a property called `age` to the global object. You can successfully delete properties from objects this way, also the global object, so `delete age` returns `true`.
<hr />

13. What's the output?
```
const user = { name: 'Lydia', age: 21 };
const admin = { admin: true, ...user };

console.log(admin);
```
**Ans:** `{ admin: true, name: "Lydia", age: 21 }`

It's possible to combine objects using the spread operator `...`. It lets you create copies of the key/value pairs of one object, and add them to another object. In this case, we create copies of the `user` object, and add them to the `admin` object. The `admin` object now contains the copied key/value pairs, which results in `{ admin: true, name: "Lydia", age: 21 }`.
<hr />

14. What's the output?
```
const settings = {
  username: 'lydiahallie',
  level: 19,
  health: 90,
};

const data = JSON.stringify(settings, ['level', 'health']);
console.log(data);
```
**Ans:** `"{"level":19, "health":90}"`

The second argument of `JSON.stringify` is the replacer. The replacer can either be a function or an array, and lets you control what and how the values should be stringified.

If the replacer is an array, only the property names included in the array will be added to the JSON string. In this case, only the properties with the names `"level"` and `"health"` are included, `"username"` is excluded. `data` is now equal to `"{"level":19, "health":90}"`.

If the replacer is a function, this function gets called on every property in the object you're stringifying. The value returned from this function will be the value of the property when it's added to the JSON string. If the value is `undefined`, this property is excluded from the JSON string.
<hr />

15. What's the output?
```
[1, 2, 3, 4].reduce((x, y) => console.log(x, y));
```
**Ans:** `1` `2` and `undefined` `3` and `undefined` `4`

The first argument that the `reduce` method receives is the accumulator, `x` in this case. The second argument is the current value, `y`. With the reduce method, we execute a callback function on every element in the array, which could ultimately result in one single value.

In this example, we are not returning any values, we are simply logging the values of the accumulator and the current value.

The value of the accumulator is equal to the previously returned value of the callback function. If you don't pass the optional `initialValue` argument to the `reduce` method, the accumulator is equal to the first element on the first call.

On the first call, the accumulator (`x`) is `1`, and the current value (`y`) is `2`. We don't return from the callback function, we log the accumulator and current value: `1` and `2` get logged.

If you don't return a value from a function, it returns `undefined`. On the next call, the accumulator is `undefined`, and the current value is `3`. `undefined` and `3` get logged.

On the fourth call, we again don't return from the callback function. The accumulator is again `undefined`, and the current value is `4`. `undefined` and `4` get logged.
<hr />

16. What's the output?
```
// index.js
console.log('running index.js');
import { sum } from './sum.js';
console.log(sum(1, 2));

// sum.js
console.log('running sum.js');
export const sum = (a, b) => a + b;
```
**Ans:** `running sum.js`, `running index.js`, `3`

With the `import` keyword, all imported modules are pre-parsed. This means that the imported modules get run first, the code in the file which imports the module gets executed after.

This is a difference between `require()` in CommonJS and `import`! With `require()`, you can load dependencies on demand while the code is being run. If we would have used `require` instead of `import`, `running index.js`, `running sum.js`, `3` would have been logged to the console.
<hr />

17. What's the output?
```
async function getData() {
  return await Promise.resolve('I made it!');
}

const data = getData();
console.log(data);
```
**Ans:** `Promise {<pending>}`

An async function always returns a promise. The `await` still has to wait for the promise to resolve: a pending promise gets returned when we call `getData()` in order to set `data` equal to it.

If we wanted to get access to the resolved value `"I made it"`, we could have used the `.then()` method on `data`:

`data.then(res => console.log(res))`

This would've logged `"I made it!"`
<hr />

18. What's the output?
```
const add = () => {
  const cache = {};
  return num => {
    if (num in cache) {
      return `From cache! ${cache[num]}`;
    } else {
      const result = num + 10;
      cache[num] = result;
      return `Calculated! ${result}`;
    }
  };
};

const addFunction = add();
console.log(addFunction(10));
console.log(addFunction(10));
console.log(addFunction(5 * 2));
```
**Ans:** `Calculated! 20` `From cache! 20` `From cache! 20`

The `add` function is a memoized function. With memoization, we can cache the results of a function in order to speed up its execution. In this case, we create a `cache` object that stores the previously returned values.

If we call the `addFunction` function again with the same argument, it first checks whether it has already gotten that value in its cache. If that's the case, the caches value will be returned, which saves on execution time. Else, if it's not cached, it will calculate the value and store it afterwards.

We call the `addFunction` function three times with the same value: on the first invocation, the value of the function when num is equal to 10 isn't cached yet. The condition of the if-statement `num in cache` returns `false`, and the else block gets executed: `Calculated! 20` gets logged, and the value of the result gets added to the `cache` object. cache now looks like `{ 10: 20 }`.

The second time, the `cache` object contains the value that gets returned for `10`. The condition of the if-statement `num in cache` returns `true`, and `'From cache! 20'` gets logged.

The third time, we pass `5 * 2` to the function which gets evaluated to `10`. The `cache` object contains the value that gets returned for `10`. The condition of the if-statement `num in cache` returns `true`, and `'From cache! 20'` gets logged.
<hr />

19. What's the output?
```
const person = {
  name: 'Lydia',
  age: 21,
};

let city = person.city;
city = 'Amsterdam';

console.log(person);
```
**Ans:** `{ name: "Lydia", age: 21 }`

We set the variable `city` equal to the value of the property called `city` on the `person` object. There is no property on this object called `city`, so the variable `city` has the value of `undefined`.

Note that we are not referencing the `person` object itself! We simply set the variable `city` equal to the current value of the `city` property on the `person` object.

Then, we set `city` equal to the string `"Amsterdam"`. This doesn't change the `person` object: there is no reference to that object.

When logging the `person` object, the unmodified object gets returned.
<hr />

20. What's the output?
```
function checkAge(age) {
  if (age < 18) {
    const message = "Sorry, you're too young.";
  } else {
    const message = "Yay! You're old enough!";
  }

  return message;
}

console.log(checkAge(21));
```
**Ans:** `ReferenceError`

Variables with the `const` and `let` keyword are block-scoped. A block is anything between curly brackets (`{ }`). In this case, the curly brackets of the if/else statements. You cannot reference a variable outside of the block it's declared in, a ReferenceError gets thrown.
<hr />

21. What's the output?
```
// module.js
export default () => 'Hello world';
export const name = 'Lydia';

// index.js
import * as data from './module';

console.log(data);
```
**Ans:** `{ default: function default(), name: "Lydia" }`

With the `import * as name` syntax, we import all exports from the `module.js` file into the `index.js` file as a new object called `data` is created. In the `module.js` file, there are two exports: the default export, and a named export. The default export is a function which returns the string `"Hello World"`, and the named export is a variable called `name` which has the value of the string `"Lydia"`.

The `data` object has a `default` property for the default export, other properties have the names of the named exports and their corresponding values.
<hr />

22. What's the output?
```
function giveLydiaPizza() {
  return 'Here is pizza!';
}

const giveLydiaChocolate = () =>
  "Here's chocolate... now go hit the gym already.";

console.log(giveLydiaPizza.prototype);
console.log(giveLydiaChocolate.prototype);
```
**Ans:** `{ constructor: ...}` `undefined`

Regular functions, such as the `giveLydiaPizza` function, have a `prototype` property, which is an object (prototype object) with a `constructor` property. Arrow functions however, such as the `giveLydiaChocolate` function, do not have this `prototype` property. `undefined` gets returned when trying to access the `prototype` property using `giveLydiaChocolate.prototype`.
<hr />

23. What's the output?
```
const person = {
  name: 'Lydia',
  age: 21,
};

for (const [x, y] of Object.entries(person)) {
  console.log(x, y);
}
```
**Ans:** `name` `Lydia` and `age` `21`

`Object.entries(person)` returns an array of nested arrays, containing the keys and objects:

`[ [ 'name', 'Lydia' ], [ 'age', 21 ] ]`

Using the `for-of` loop, we can iterate over each element in the array, the subarrays in this case. We can destructure the subarrays instantly in the for-of loop, using `const [x, y]`. `x` is equal to the first element in the subarray, `y` is equal to the second element in the subarray.

The first subarray is `[ "name", "Lydia" ]`, with `x` equal to `"name"`, and `y` equal to `"Lydia"`, which get logged. The second subarray is `[ "age", 21 ]`, with `x` equal to `"age"`, and `y` equal to `21`, which get logged.
<hr />

24. What's the output?
```
function nums(a, b) {
  if (a > b) console.log('a is bigger');
  else console.log('b is bigger');
  return
  a + b;
}

console.log(nums(4, 2));
console.log(nums(1, 2));
```
**Ans:** `a is bigger`, `undefined` and `b is bigger`, `undefined`

In JavaScript, we don't have to write the semicolon (`;`) explicitly, however the JavaScript engine still adds them after statements. This is called Automatic Semicolon Insertion. A statement can for example be variables, or keywords like `throw`, `return`, `break`, etc.

Here, we wrote a `return` statement, and another value `a + b` on a new line. However, since it's a new line, the engine doesn't know that it's actually the value that we wanted to return. Instead, it automatically added a semicolon after `return`. You could see this as:
```
return;
a + b;
```
This means that `a + b` is never reached, since a function stops running after the `return` keyword. If no value gets returned, like here, the function returns `undefined`. Note that there is no automatic insertion after `if/else` statements!
<hr />

25. What's the output?
```
const myPromise = () => Promise.resolve('I have resolved!');

function firstFunction() {
  myPromise().then(res => console.log(res));
  console.log('second');
}

async function secondFunction() {
  console.log(await myPromise());
  console.log('second');
}

firstFunction();
secondFunction();
```
**Ans:** `second`, `I have resolved!` and `I have resolved!`, `second`

With a promise, we basically say _I want to execute this function, but I'll put it aside for now while it's running since this might take a while. Only when a certain value is resolved (or rejected), and when the call stack is empty, I want to use this value._

We can get this value with both `.then` and the `await` keyword in an `async` function. Although we can get a promise's value with both `.then` and `await`, they work a bit differently.

In the `firstFunction`, we (sort of) put the myPromise function aside while it was running, but continued running the other code, which is `console.log('second')` in this case. Then, the function resolved with the string `I have resolved`, which then got logged after it saw that the callstack was empty.

With the await keyword in `secondFunction`, we literally pause the execution of an async function until the value has been resolved before moving to the next line.

This means that it waited for the `myPromise` to resolve with the value `I have resolved`, and only once that happened, we moved to the next line: `second` got logged.
<hr />