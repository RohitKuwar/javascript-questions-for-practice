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
This is possible in JavaScript, because functions are objects! (Everything besides primitive types are objects). A function is a special type of object. The code you write yourself isn't the actual function. The function is an object with properties. This property is invocable.git add REA