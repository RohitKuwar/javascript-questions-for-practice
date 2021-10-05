1. What's the output?
```
let c = { greeting: 'Hey!' };
let d;

d = c;
c.greeting = 'Hello';
console.log(d.greeting);
```
**Ans:** Hello \
In JavaScript, all objects interact by reference when setting them equal to each other. First, variable c holds a value to an object. Later, we assign d with the same reference that c has to the object. When you change one object, you change all of them.

2. What happens when we do this?
```
function bark() {
  console.log('Woof!');
}

bark.animal = 'dog';
```
**Ans:** Nothing, this is totally fine!\
This is possible in JavaScript, because functions are objects! (Everything besides primitive types are objects). A function is a special type of object. The code you write yourself isn't the actual function. The function is an object with properties. This property is invocable.

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
**Ans:** TypeError\
In JavaScript, functions are objects, and therefore, the method getFullName gets added to the constructor function object itself. For that reason, we can call Person.getFullName(), but member.getFullName throws a TypeError.
If you want a method to be available to all object instances, you have to add it to the prototype property:
```
Person.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};
```

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
**Ans:** `Person {firstName: "Lydia", lastName: "Hallie"}` and `undefined`\
For `sarah`, we didn't use the `new` keyword. When using `new`, `this` refers to the new empty object we create. However, if you don't add `new`, `this` refers to the **global object!**
We said that `this.firstName` equals `"Sarah"` and `this.lastName` equals `"Smith"`. What we actually did, is defining `global.firstName = 'Sarah'` and `global.lastName = 'Smith'`. `sarah` itself is left `undefined`, since we don't return a value from the `Person` function.