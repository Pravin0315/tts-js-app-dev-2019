# ES6 Notes

```javascript
 //Template Literal
console.log(`Hello! I'm a string
continues on the next line`);

//Previous way
console.log("some string\n" + "string text2");
//this would move the strings to separate lines

const name = "Jimmy"
const day = "Wednesday"
const instructor = {
    name: "Chris", 
    lesson: "ES6",
    greet: function() {
        return `Hello ${this.name}, today we'll learn ${this.lesson}!`
    }
}
```
# ES5
```javascript
console.log("Hello" + name + "I hope you have a great" + day);
```
# ES6
```javascript
console.log(`Hello ${name} I hope ${day} goes well!`);
```
# interprolation
```javascript
console.log(`Hello ${instructor.name}, today we'll learn ${instructor.lesson}!`);

console.log(instructor.greet());

function foo() {    
    let x = true;
    if (x) {
        var usingVar = "i'm using var";
        console.log(usingVar)
    }
}
foo();
// using let has more benefits, have more control over variables. It binds through the laxical scope. It won't be affected by closure. 

const instructors = ["Jimmy", "Chris"]
instructors = ["Jim", "Christopher"]  
//would get a type error b/c instructors has already been defined

instructors.push("Jack", "Jill");  
//this would add these names to the instructors array

//const also accepts uppercase or lowercase

//default parameters, lets you pass default argument to your functions
function hello(name = 'Mystery Person') {
    name = name || 'Mystery Person';
    console.log(`Hello ${name} is it me your looking for`)
}
hello("Bobby");
hello();
```
# Arrow Functions
```javascript
 const teacher = {
     name: "Jimm",
     speak: function() {
         //bind a function to specific context
         let boundfunction = function() {
         console.log('later my name is ' + this.name);
         }.bind(this);
         setTimeout(boundfunction,1000);
        //bound function will always run in bound countex
    
     }
};

const teacher = {
    name: "Jimm",
    speak(){
        let boundfunction = () => {
        console.log('later my name is ' + this.name);
        };
        setTimeout(boundfunction,1000);
    }
};

teacher.speak();
```
# Lexical Binding 
```javascript
//bind to the scope of where they are defined, not where they are used

let students = [
    {name: 'Hugo'},
    {name: 'Candace'},
    {name: 'Taylor'}
];

let names = students.map((value) => value.name);
console.log(names);
same as
 let names = students.map((student) => {
     return student.name
 });
value is the argument 

 function add() {
     console.log("arugmments object:", arguments);

     var numbers = Array.prototype.slice.call(arguments);
     var sum = 0;

     numbers.forEach(function (number){
         sum += number;
     });
     return sum;
 }
 console.log(add(1,2,3,4,5,6,7,8));


//more current way to do this
 let add = (...numbers) => {
    console.log("rest parameters", numbers);

     let sum = 0;
     numbers.forEach(function (number){
         sum += number;
     });
 return sum;
 }
 console.log(add(1,2,3,4,5,6,7,8));
//Rest Parameter

//Rest example all on same line
let add = (...numbers) => numbers.reduce((sum,number) => sum += number, 0);
//reduce takes in all the arguments and returns them as an array

//combine rest parameters with multiple arguments
function addStuff (x,y,...z) {
    return (x+y) * z.length
}
console.log(addStuff(1,2, "hello", "world", true, 99));
```
# Spread
```javascript
let random = ["Hello", "World", true, 99]
let newArray = [1, 2,...random, 3];

console.log(newArray);
//[1,2,"Hello","World",true,99,3]

let spreadEx = (item) => {
    let spreadArray = [...item]
    console.log(spreadArray);
    return spreadArray
}

spreadEx("Hello World");
//[ "H", "e", "l", "l", "o", " ", "W", "o", "r", "l", "d" ]

let restEx = (...z) => {
    console.log(z)
    return z
}
restEx("hello", "world")
//[ "hello", "world" ]
```

# Array Destructors
```javascript
 var moreStudents = [`Julian`, `AJ`, `Matt`]
 var x = moreStudents[0]
 var y = moreStudents[1]
 var z = moreStudents[2]

console.log (x,y,z);

let  [x,y,z] = moreStudents
let moreStudents = ["Julian", "AJ", "Matt"];

let [x,,z]
console.log (alpha,omega)

let [x, ...rest] = moreStudents
console.log (thing, stuff)
 Julian ["AJ","Matt"]

 let completedHomework = () => {
   return ["Julian", "AJ", "Matt"];
 }

let [x,y,z] = completedHomework();

console.log(x,y,z);

//Also works with objects
let instructor = {
    name:"Jimmy",
    email: "no@no.com"
}
let {name: x, email: y} = instructor;
console.log(x);

let travel = {
    location: "New Zealand"
    
}

function something({location, time = "winter"}){
console.log(location,time);
}

something(travel);
```

# Constructor function
```javascript
function Person (name, job) {
    this.name = name;
    this.job = job;
}

Person.prototype.getName = function getName() {
    return this.name;
}

Person.prototype.getJob = function getJob() {
    return this.job;
}
var goodGuy = new Person ("Aang", "Airbender");
console.log(goodGuy.getJob())

class Person {
    constructor (name, job) {
        this.name = name
        this.job = job
    }

    getName() {
        return this.name;
    }

    getJob() {
        return this.job;
    }
}

let goodGuy = new Person('Neo', 'the one');
console.log(goodGuy);

class Person {
    constructor(name, job) {
        this.name = name;
        this.job = job;
    }
    getName() {
        return this.name;
    }
    getJob() {
        return this.job;
    }
}

class Superhero extends Person {
    constructor (name, heroName, superPower) {
        super(name);
        this.heroName = heroName;
        this.superPower = superPower;
    }
    secretIdentity() {
        return `${this.heroName} is ${this.name}!!`
    }
}

let batman = new Superhero("Bruce Wayne", "Batman")
console.log(batman.secretIdentity())

class Person {
    constructor (name) {
        this.name = name;
    }
    set name (name) {
        this._name= name;
    }
    get name() {
        return this._name
    }
}

let goodGuy = new Person ('Jim Gordon');
console.log(goodGuy.name);
//Jim Gordon

goodGuy.name = "James Gordon";
console.log(goodGuy.name);
//James Gordon

let student = {name: "A-aron"};
let status = new Map();

status.set(student.name, "A-aron");
status.set("feeling", "churlish");
console.log(status.get(student.name));
console.log(status.get("feeling"));
```
