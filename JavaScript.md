# JavaScript

## Quick Notes

* chrome development console can be used to write Javascript

  ```javascript
  alert("Hello World!")
  ```

* JS is **<u>dynamically typed</u>** - the primitive type (integer, string, float, boolean, etc.) does not have to be explicitly (strict/strong) **typed**

## 1. Fundamentals - Intro and Refresher

### What is JavaScript?

* high-level, object-oriented, multi-paradigm programming language
  * high-level - don't have to worry about complex things like memory management
  * multi-paradigm - can use different styles like imperative and declarative style programming

### What role does JS serve in Web Development

* it is one of the 3 pillars of Web Development
  * HTML - used to add components to a Web Page
  * CSS - presentation, styling the Web Page
  * JavaScript - coding, making the Web Page dynamic and capable of building Web Applications

### Node.js

* It allows web applications on the browser, but it can also be run outside of the browser, such as on a Web Server using Node.js
* This allows to create backend-apps which can be used for Databases

### Libraries and Frameworks

* Popular libraries and frameworks are: React, Angular, and Vue

* These are tools that help develop Javascript faster

* This allows to create front-end apps on the browser

* Native mobile and desktop applications can be created with Javascript using React Native and  Ionic for mobile, and Electron for Desktop

  

### Variables

#### Creating Variables

```javascript
let year = 1991;
```

* the keyword `let` creates a variable

* the single `=` assigns a value to the variable

* variables are dynamically-typed (i.e. the primitive type does not need to be declared)

  * this can be viewed as a difficult part of using JS since variables are strongly typed

* variables can be reassigned its type to it (the key is NOT using the `let` keyword again)

  * ```javascript
    let year = 1991;
    Console.log(year);  //Console displays: 1991
    year = 'nineteen ninety-one';
    Console.log(year);  //Console displays: nineteen ninety-one
    ```

  * ```javascript
    const mark = {weight:76, height:1.69, bmi: 0};
    mark.bmi = BMI(mark.weight, mark.height); 
    const john = {weight:90, height:1.95, bmi: 0};
    john.bmi = BMI(john.weight, john.height); 
    
    function BMI(mass, height){
      return mass / (height ** 2);
    }
    
    console.log('Mark\'s weight: '+mark.weight+'kg, height: '+mark.height+'m, BMI: '+mark.bmi);
    console.log('John\'s weight: '+john.weight+'kg, height: '+john.height+'m, BMI: '+john.bmi);
    
    markHigherBMI = Boolean(mark.bmi > john.bmi);
    if (markHigherBMI) {
      console.log('Mark has higher BMI than John');
    } else {
      console.log('John has higher BMI than Mark');
    };
    ```

    


### Strings

* Template Literals
  * uses back ticks (`)  around the complete string, and (${})  for string interpolation
  * new lines can be done by just going to the next line, no special character needed 

```javascript
console.log('Mark\'s weight: '+mark.weight+'kg, height: '+mark.height+'m, BMI: '+mark.bmi);

console.log(`Mark's weight: ${mark.weight}kg, height:${mark.height}m, BMI:${+mark.bmi}`);
```



### Equality Operators

* there are two equality operators `==` and `===`
  * `==` does Type Coercion, thus can convert a type into another
    * `'18' == 18 //true`
  * `===` does NOT do Type Coercion
    * `'18' === 18 //false`

### Ternary Operators

* ```javascript
  const age = 18;
  let s = '';
  age >= 21 ? s = 'Old enough to drink' : s = 'Too young to drink';
  console.log(s);
  ```

  * `?` is the ternary operator that acts acts like "if"

    * If the statement preceding `?` is true that expression1, else expression 2

### Statements vs Expressions

#### Expressions

* Produces a value
  * 1991
  * 2007 - 1991
  * true && 1991

### Statements

* Perform Actions
  * If Statement, etc



## 2. Fundamentals - Additional

### Strict Mode

* `'use strict';`
  * needs to come at the very beginning of the .JS file
  * Restricts to do certain things
  * Makes certain errors visible
  * Helpful in displaying errors in code that otherwise may run silent such as
    * undefined variables - variables that are mistyped without strict mode would just not display
    * restrict use of reserved words such as interface

### Functions

#### Function Declaration v. Function Expression

* Function Declaration is your standard type of Function

  * it can be called before/after the initialization of the function

* Function Expression is storing a Function in a variable/constant

  * it can NOT by called before its initialization (i.e. can't assign a variable to a function expression until the function expression is defined)

* ```javascript
  //function declaration
  function calcAge1(birthYear){
      return 2022 - birthYear;
  }
  
  const age1 = calcAge1(1984);
  
  //function expression
  const calcAge2 = function calcAge2(birthYear){
      return 2022 - birthYear;
  }
  
  const age2 = calcAge2(1984);
  
  console.log(`Age 1: ${age1}, Age 2: ${age2}`);
  ```

#### Arrow Functions

* is a shorthand way of writing a Function Expression

  ```javascript
  //arrow function
  const calcAge3 = birthYear => 2022 - birthYear;
  const age3 = calcAge3(1984);
  console.log(`Age 3: ${age3}`);
  ```

  * `birthYear => 2022 - birthYear` 
    * one-line function
    * no return key word
    * `birthYear` parameter of function
    * `2022 - birthYear` - returning value

* can also include more lines of code

  * ```javascript
    const yearsUntilRetirement = birthYear => {
        const age = 2022 - birthYear;
        const retirement = 65 - age;
        return retirement;
    }
    
    const age4 = yearsUntilRetirement(1984);
    console.log(`Years until retirment is: ${age4}`);
    ```

* can also include multiple parameters

  * ```javascript
    //arrow function - multiple parameters
    const yearsUntilRetireAge = (birthYear, retireAge) => {
        const age = 2022 - birthYear;
        const retirement = retireAge - age;
        return {retirement, retireAge};
    }
    
    let retire = yearsUntilRetireAge(1984, 67);
    console.log(`Years until retirment is: ${retire.retirement}, at age ${retire.retireAge}`); 
    //Years until retirment is: 29, at age 67
    ```

    * `(birthYear, retireAge)` - multiple parameters that need to have parentheses 

    * `{retirement, retireAge}` - can have multiple values returned (need to use curly brackets)

    * `let retire` - single variable assignment

      * `retire.retirement` and `retire.retireAge` both used to supply the multiple values that were returned

        

## 3. Arrays

* An array is a data structure that holds multiple values

* Example

  ```javascript
  constant years = [1984, 2002, 2013];
  const book = ['Ernest Hemingway', 70, 'author', years]  //book is an array with different datatypes
  ```

### Basic Methods

#### Add Elements

* push - adds to the end of an array

  ```javascript
  const friends = ['Steve', 'Bob'];
  friends.push('Jay');  // friends = ['Steve', 'Bob', 'Jay']
  ```

* unshift - adds to beginning of an array

  ```javascript
  const friends = ['Steve', 'Bob'];
  friends.unshift('Jay');  // friends = ['Jay', 'Steve', 'Bob']
  ```

  

#### Remove Elements

* pop - removes from the end of an array

  ```javascript
  const friends = ['Steve', 'Bob', 'Jay'];
  friends.pop();  // friends = ['Steve', 'Bob']
  ```

* unshift - removes from the beginning of an array

  ```javascript
  const friends = ['Steve', 'Bob', 'Jay'];
  friends.unshift();  // friends = ['Bob', 'Jay']
  ```

#### Index of Elements

* indexOf - returns the index number of the given element

  ```javascript
  const friends = ['Steve', 'Bob', 'Jay'];
  friends.indexOf('Bob'); // 1
  ```

#### Include

* include - returns boolean if element is found

  ```javascript
  const friends = ['Steve', 'Bob', 'Jay'];
  friends.include('Bob'); //true
  friends.include('Peter'); //false
  ```



## 4. Intro to Objects

* data structure has Key-Value pairs

* example

  ```javascript
  const Jonas = {
    firstName: 'Jonas',
    lastName: 'Smith',
    age: 2022 - 1991,
    job: 'teacher',
    friends: ['Amy', 'Bob', 'Chris']
  };
  ```

  * there are different ways to create objects in JS.  This is the most simple, using curly braces.  This is known as Object Literal Syntax.

* A noteworthy difference between Objects and Arrays is that Arrays are ordered (i.e. need to know the order of the data to access a value), whereas Objects are unordered - can access the value through the property name.

### Dot vs Bracket Notation

* two ways of retrieving object values

#### Dot

* `Jonas.firstName` 

#### Bracket

* `Jonas['firstName']`

* The bracket notations is useful if you need to retrieve an Object's value through a variable

* ```javascript
  const Jonas = {
    firstName: 'Jonas',
    lastName: 'Smith',
    age: 2022 - 1991,
    job: 'teacher',
    friends: ['Amy', 'Bob', 'Chris']
  };
  
  const interestedIn = prompt('What do you want to know about Jonas?  Choose between firstName, lastName, age, job, friends.');
  console.log(Jonas[interestedIn]);
  ```

### Object Methods

```javascript
const Jonas = {
  firstName: 'Jonas',
  lastName: 'Smith',
  birthYear: 1984,
  job: 'teacher',
  friends: ['Amy', 'Bob', 'Chris'],

  calcAge: function(){
    this.age = (new Date().getFullYear()) - this.birthYear;
    return this.age;
  }
};

console.log(Jonas.calcAge());
```



## 5. Looping

### Continue and Break

`continue` keyword breaks from one loop iteration (skips over)

```javascript
for (let i = 0; i < JonasArray.length; i++)
{
  if (typeof JonasArray[i] !== 'string') continue;  //array element that's not a string gets skipped
  console.log(JonasArray[i]);
}
```

`break` keyword breaks out of entire loop (exits loop)