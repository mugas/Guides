  <h1>Object Oriented Programming</h1>

It´s a programming model based around the idea of objects.
These objects are constructed from what are called <strong>"classes"</strong>.This objects created from classes are called <strong>"instances"</strong>.

We use a function as a constructor. By convention, the function name is Capitalized.

```javascript
function Playersbyteam(football, baseball, voleyball) {
  this.football = football;
  this.baseball = baseball;
  this.voleyball = voleyball;
}
```

So to construct a object, we use the keyword `new`.

```javascript
var benfica = new PlayerbyTeam(28, 0, 24);
benfica.football; // 28
benfica.baseball; //0
benfica.voleyball; //24
```

So what the keyword `new`does?

<ol>
    <li>Creates a empty object</li>
    <li>Sets the keyword `this` to the empty object</li>
    <li>Adds the line `return this`to the end of the function</li>
    <li>Adds a property onto the empty object called `_proto_`</li>
</ol>

```javascript
function Dog(name, age) {
  this.name = name;
  this.age = age;
  this.bark = function() {
    console.log(this.name + " just barked");
  };
}

var rusty = new Dog("rusty", 5);
var fido = new Dog("fido", 2);
rusty.bark(); // rusty just barked
```

As we can see, we also can put methods inside a object constructor.

<h2>Multiple Constructors</h2>

```javascript
function Person(name, yearOfBirth, job, calculateAge) {
  this.name = name;
  this.yearOfBirth = yearOfBirts;
  this.job = job;
  this.calculateAge = calculateAge;
}

function Atlete(olympics, olympicsMedals, allowedOlympics) {
  this.olympics = olympics;
  this.olympicsMedals = olympicsMedals;
  this.allowedOlympics = allowedOlympics;
}
```

The `Athele`function Constructor can get `inheritance`from the `Person`one and gain same of the same elements.`Inheritance`works by `Prototype`

```javascript
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
  this.numWheels = 4;
}

/* function Motorcycle(make,model,year){
    Car.call(this,make,model,year)
    this.numWheels = 2;
} */

/* function Motorcycle(make,model,year){
    Car.apply(this, [make,model,year])
    this.numWheels = 2;
}
 */
function Motorcycle(make, model, year) {
  Car.apply(this, arguments);
  this.numWheels = 2;
}

var honda = new Motorcycle(2.1, "turbo", 1980);
```

<h2>Prototypes</h2>

Every constructor function has a property on it called `prototype` which is an object, that can have methods and properties attached too.
This methods and properties are shared and acessible by any object that is created from that constructor when the `new` keyword is used.
The prototype has a property on it called "constructor", which points back to the constructor function.
Anytime an object is created using the `new` keyword, a property called `_proto_` gets created, linking the object and the prototype property of the constructor function.

```javascript
function Person(name) {
  this.name = name;
}
```

If we see it on the console, we can see that there is already a property on the function called prototype.

So let´s create 2 objects:

```javascript
var ellie = new Person("Ellie");
var john = new Person("John);

ellie._proto_ === Person.prototype
```

The `Person.prototype` object has also a property called `constructor` which points back to the function.

```javascript
Person.prototype.constructor === Person;
```

Where to use it?
Imagine we have this function constructor:

```javascript
function Person(name) {
  this.name = name;
  this.sayHi = function() {
    return "Hi" + this.name;
  };
}
```

So every time we create a new person we have to create the the function for it. With the `prototype`we can access the function with object created.

```javascript
function Person(name) {
  this.name = name;
}
Person.prototype.sayHi = function() {
  return "Hi" + this.name;
};
```

<ul>Every JS object has a prototype property, which makes inheritance possible in JS</ul>
<ul>The prototype of an object is where we put methods and properties that we want other objects to inherit</ul>
<ul>The Constructor's prototype property is not the prototype of the Constructor itself, it's the prototype of All instances that are created through it</ul>
<ul>When a certain method is called, the search starts in the object itself, and if it cannot be found, the search moves on to the object's prototype. This continues until the method is found:<strong>prototype chain</strong></ul>

circle = function
square = object

So analysing in the console we can see that:

```javascript
john
Person {name: "john", yearofBirth: 1990, job: "teacher"}
job: "teacher"
name: "john"
yearofBirth: 1990
__proto__:
calculateAge: ƒ ()
arguments: null
caller: null
length: 0
name: ""
prototype: {constructor: ƒ}
__proto__: ƒ ()
[[FunctionLocation]]: app.js:14
[[Scopes]]: Scopes[1]
constructor: ƒ (name, yearofBirth, job)
__proto__:
constructor: ƒ Object()
hasOwnProperty: ƒ hasOwnProperty()
isPrototypeOf: ƒ isPrototypeOf()
propertyIsEnumerable: ƒ propertyIsEnumerable()
toLocaleString: ƒ toLocaleString()
toString: ƒ toString()
valueOf: ƒ valueOf()
__defineGetter__: ƒ __defineGetter__()
__defineSetter__: ƒ __defineSetter__()
__lookupGetter__: ƒ __lookupGetter__()
__lookupSetter__: ƒ __lookupSetter__()
get __proto__: ƒ __proto__()
set __proto__: ƒ __proto__()
```

<h2>Object.create</h2>

We first define the object that works as a `prototype` and then create a new `object` based on that `prototype`.

```javascript
var personProto = {
  calculateAge: function() {
    console.log(2016 - this.yearOfBirth);
  }
};

var john = Object.create(personProto);
john.name = "john";
john.yearOfBirth = 1990;
john.job = "teacher";

var jane = Object.create(personProto, {
  name: { value: "Jane" },
  yearOfBirth: { value: 1969 },
  job: { value: "designer" }
});
```

Object.create builds an object that inherates directly from the one that we pass from the first argument
