
[Object Oriented Programming](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/object-oriented-programming/)

> 感觉FCC上自己写的代码没保持，所以从这里开始记录下来

- Object Oriented Programming: Use Dot Notation to Access the Properties of an ObjectPassed

```JS
let dog = {
  name: "Spot",
  numLegs: 4
};
// Only change code below this line
console.log(dog.name);
console.log(dog.numLegs);
```

- Object Oriented Programming: Create a Method on an Object
```js
let dog = {
  name: "Spot",
  numLegs: 4,
  sayLegs:function(){
    return "This dog has "+ dog.numLegs+" legs.";
  }
};

dog.sayLegs();
```
- Object Oriented Programming: Make Code More Reusable with the this Keyword

```js
let dog = {
  name: "Spot",
  numLegs: 4,
  sayLegs: function() {return "This dog has " + this.numLegs + " legs.";}
};

dog.sayLegs();
```
- Object Oriented Programming: Define a Constructor Function

```js
function Dog(){
    this.name = "Koko";
    this.color = "black";
    this.numLegs = 4;
}
```

- Object Oriented Programming: Use a Constructor to Create Objects

```JS
function Dog() {
  this.name = "Rupert";
  this.color = "brown";
  this.numLegs = 4;
}
// Only change code below this line
let hound = new Dog(); 
```

- Object Oriented Programming: Extend Constructors to Receive Arguments

```JS
function Dog(name, color) {
    this.name = name;
    this.color = color;
    this.numLegs = 4;
}

let terrier =new Dog("Koko","black");
```

- Object Oriented Programming: Verify an Object's Constructor with instanceof

```js
function House(numBedrooms) {
  this.numBedrooms = numBedrooms;
}

// Only change code below this line
let myHouse =new House(5);
myHouse instanceof House;
```

- Object Oriented Programming: Understand Own Properties

```js
function Bird(name) {
  this.name = name;
  this.numLegs = 2;
}

let canary = new Bird("Tweety");
let ownProps = [];
// Only change code below this line
for(let property in canary){
  if(canary.hasOwnProperty(property)){
    ownProps.push(property);
  }
}

console.log(ownProps);
```

- Object Oriented Programming: Use Prototype Properties to Reduce Duplicate Code

```js
function Dog(name) {
  this.name = name;
}

Dog.prototype.numLegs =2;

// Only change code above this line
let beagle = new Dog("Snoopy");
```

- Object Oriented Programming: Iterate Over All Properties

```js
function Dog(name) {
  this.name = name;
}

Dog.prototype.numLegs = 4;

let beagle = new Dog("Snoopy");

let ownProps = [];
let prototypeProps = [];

// Only change code below this line
for (let property in beagle) {
  if(beagle.hasOwnProperty(property)) {
    ownProps.push(property);
  } else {
    prototypeProps.push(property);
  }
}

console.log(ownProps); 
console.log(prototypeProps); 
```

- Object Oriented Programming: Understand the Constructor Property

```js
function Dog(name) {
  this.name = name;
}

// Only change code below this line
function joinDogFraternity(candidate) {
  return candidate.constructor === Dog
}
```