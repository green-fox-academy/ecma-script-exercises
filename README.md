# EcmaScript exercises
This repo contains exercises that focus on the new ES features.

### Arrow function

Write a function call in the commented area with an old anonym function and an arrow function.  Both anonym functions functions should take a number parameter and return it's square value.
```javascript
function multiPurposeFunction(action){
    if (action){
        console.log(action(3));        
    }
}

function exampleNonAnonymFunction(param){
    return param*param;
}

function frameFunction(){
    // this function call shows an example,
    // but it is not using anonym functions
    multiPurposeFunction(exampleNonAnonymFunction());
    // write your code here
}

frameFunction();
```

In the next exercise write two anonym functions again.
This time the returned value is conditional.<br/>
If the first parameter is an empty string, it should return the second parameter. If not, it should return the two parameters joined by a single space. 
```javascript
function multiPurposeFunction(action){
    if (action){
        console.log(action('John', 'Smith'));
        console.log(action('', 'Bond'));        
    }
}

function frameFunction(){
    ////Write your code here
}

frameFunction();
```

### Classes

In ES6 classes became available. Before that you had to use prototype to create OO patterned code. For example if you need a class named Apple with type, color and in info function, you could write this code in ES5:
```javascript
function Apple (type) {
    this.type = type;
    this.color = "red";
}
 
Apple.prototype.getInfo = function() {
    return this.color + ' ' + this.type + ' apple';
};
```
The same in ES6 would look like this:
```javascript
class Apple{
    constructor(type){
        this.type = type;
        this.color = "red";
    }
    getInfo(){
        return this.color + ' ' + this.type + ' apple';
    }
}
```

Please write with both technologies a class that's named Garden, has width and length as variables and the following functions: area(), circumference() and efficiency(). The function called efficiency should return the result of area()/circumference().

### Literals
ES6 made creating objects also easier. If you look at the code below you can see how attributes were assigned in newly created objects. With ES6 you can use dynamic properties in creation, not just after it, and if the property name is the same as the variable name, then you can shorthand those variables. 
```javascript
var type = 'regular';
var color = 'blue';
var height = 40;
var propName = 'height';

// before ES6
var lamp = {
    type: type,
    color: color
};
lamp[propName]= height;

// with and after ES6 
var newLamp = {
    type,
    color,
    [propName]: height
};
```
Based on this please finish the function below in two ways. Once without the ES6 features and once with the ES6 features.
```javascript
function carWrapper(model, color, year, doors, specPropName, specPropValue){
    // the function should create and return an object with assigning the model, color year and doors to properties with the same name as the variable and it should assign to the specPropName named property the specPropValue
    
}

console.log(JSON.stringify(carWrapper('Benz','black',1886,0,'historical',true)));
// expected output: {"model":"Benz","color":"black","year":1886,"doors":0,"historical":true}
```

### Destructoring
ES6 didn't just make the creation of objects easier but also property extraction. Take a look on the two codes below:
```javascript
var lamp = {
   type: 'spooky',
   color: 'orange',
   fresh: true,
   details: {
       brightness: 'various'
   }
};

// before ES6
var type = lamp.type;
var color = lamp.color;
var fresh = lamp.fresh;
var lampBrightness = lamp.details.brightness;

// from ES6
var {type, color, fresh, details:{brightness: lampBrightness}} = lamp;
```
Your next task is to get the object properties with and without ES6 destructoring from the following objects.
```javascript
var car = {
    model:'Benz',
    color:'black',
    year:1886,
    doors:0,
    historical:true
};
var computer = {
    type: 'PC',
    monitor: {
        color: 'black',
        size: '16\"',
        HDMI: true,
        VGA: true
    },
    tower:{
        color: 'grey',
        CPU: 4.7,
        memory: 16,
        SSD: 128
    }
}
```

### Template strings

ES6 gives a new way to create strings.
```javascript
var name = 'Bob';
var old = 'Hello '+name+'!\nHow are you today?'; // this is the old  way of creating a dynamic string.
var updated = `Hello ${name}!
How are you today?`; 
```

Please write a log(timestamp, username, action) function that will create and return a string based on this template:
```javascript
"INFO - {timestamp}
{username} : {action}"
```

### Default

ES6 provides new features to process function parameters and to provide them.
```javascript
// default values before ES6
function foo(x,y){
    if (y === undefined){ y = 12; }
    return x + y;
}

// with ES6
function foo(x, y=12) {
    // y is 12 if not passed (or passed as undefined)
    return x + y;
}
```
Please write a function that returns a string. Possible values are "coffee", "coffee with sugar", "coffee with milk", "coffee with sugar and with milk". The function should take two parameters, "sugar" and "milk", with default "false" boolean value.
### Rest
You can also take unknown amount of arguments more easily.
```javascript
function foo(){
    var rest = Array.from(arguments);
    var x = rest.shift();
    // at this point we have rest with the content we want
    return x * rest.length;
}

function foo(x, ...rest) {
  return x * rest.length;
}

foo(4,3,2,1)
```
Please write a function that takes at least 3 parameters, all of them numbers. The function should return a matrix and the first two parameters should specify it's size. The first parameter is the number of rows, the second is the number of columns. The rest of the numbers is the content of the matrix line-by-line. If the matrix can't be created because of insufficient parameters the function should return null. 
### Spread
You can also spread the elements of an array into function parameters.
```javascript
function foo(x, y, z) {
  return x + y + z;
}

// before ES6
foo.apply(null,[1,2,3]);

// with ES6
foo(...[1,2,3]);
```
The following function takes three numbers and decides whether it could be a triangle or not. The next array contains number arrays with possible triangle sides. Please create a new array that holds boolean values that are created with the isTriangle function and the number arrays.
```javascript
function isTriangle(a,b,c){
    if (a <= 0 || b <= 0 || c <= 0){return false;}
    if (a+b <= c){return false;}
    if (a+c <= b){return false;}
    if (b+c <= a){return false;}
    return true;
}
var possibleTriangles = [
    [1,1,1],
    [3,4,5],
    [1,2,3],
    [5,12,13],
    [-1,-1,-1]
];
```

### Let + Const vs. Var
In ES6 the use of "var" is discouraged. The main difference is that the two new keywords will explicitly allow or forbid you the change of variables. Creating constants with "var" needs closures. Also in some cases variables declared with "var" will remain live beyond their intended use.
```javascript
// without ES6
function example(valueToFix){
    var fixValue = function(){
        var hidden = valueToFix;
        return function(){return hidden;}
    };
    if (true){
        var changeable = 2;
    }
    changeable = fixValue()();
}

// with ES6
function example(valueToFix){
    const fixValue = valueToFix;
    if (true){
        let changeable = 2;
        changeable = 3;
    }
    // changeable doesn't exist here so it can't be used
    let changeable = fixValue; // but it can be redeclared
}
```
Please write a function that takes a number array and returns the average of the numbers. In the function store the length of the parameter in a const variable.
### For ... of
Before ES6 for cycles that aimed to cycle through a list of elements could only be designed with an iterator variable used as an index. With ES6 you can use the for...of syntax to work with the array items.
```javascript
const arr = [1,2,3,4];

// before ES6
for (let ind = 0; ind < arr.length; ind++){
    console.log(arr[ind]);
}

// with ES6
for (let item of arr){
    console.log(item);
}
```
Please write a function that finds the maximum value in an array.
```javascript
const data = [5,1,2,9,7,3,8];
```
### Set
Without ES6 if you wanted to have a list with unique items you had to create it on your own. ES6 introduced Set as a built in solution.
```javascript
// ES6 solution
const setEntity = new Set();
setEntity.add(1).add(2).add(1);
for (let item of setEntity){
    console.log(item);
}
```
Please write a solution that uses no ES6 functionality but provides set-like behaviour. It's enough to store and read data, you don't have to implement every feature of the ES6 Set class.<br>
Please write a short code that presents your code's features.