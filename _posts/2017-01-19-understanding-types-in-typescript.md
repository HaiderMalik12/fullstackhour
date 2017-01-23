---
layout: dark-post
title: "Understanding types in TypeScript"
description: "Basic types in TypeScript"
tags: [TypeScript]
comments: true
image:
    feature: ts-logo.jpg
categories: [TypeScript]
share: true
---


### Basic Syntax

- First keyword would be var, let or const
- Second would be your variable name
- then annotate with :
- fourth is your data type
- fifth is assignment and then value

### string

```ts
 let firstName : string = 'Haider';
```

### number

```ts
let age : number = 23;
```

### boolean

```ts
let isApplied : boolean = true;
```

### array

```ts
let shirts : string[] =['Levis','Outfiters','Cross Road'];
```

You can create an array of multiple data types by using `any` data type

```ts
let myArr : any[] =['Hello',1,false];
```

### tuples

If you want to represent an array of values as a pair string and number

```ts
let statuses : [string,number] = ['SENT',1,'LIVE',3,'OUTBOX',4];
console.log(statuses[0]);
console.log(statuses[1]);

```

`Output`

```bash

SENT
1

```

It is just a simple array But you can insert only string data type value
and number data type value

### enum

```ts
enum Status {
    SENT,   // 0
    OUTBOX, // 1
    DRAFT,  // 2
    LIVE,   // 3
    FAILED // 4
}

console.log(Status.OUTBOX);
console.log(Status.DRAFT);
console.log(Status.FAILED);

```

`Output`

```bash
1
2
4
```
You could also create a new status from this enum Status

```ts
let sent: Status = Status.SENT
```

`enum` will map your values to numeric values, by default it starts from
index 0 .

You can also assign your own numeric value

```ts
enum Status {

    SENT = 100,
    LIVE = 101,
    DRAFT= 102
}

console.log(Status.SENT);
```

`Output`

```bash
100
```

Here is a compiled javascript for enum

```javascript
var Status;
(function (Status) {
    Status[Status["SENT"] = 0] = "SENT";
    Status[Status["OUTBOX"] = 1] = "OUTBOX";
    Status[Status["DRAFT"] = 2] = "DRAFT";
    Status[Status["LIVE"] = 3] = "LIVE";
    Status[Status["FAILED"] = 777] = "FAILED";
})(Status || (Status = {}));

console.log(Status.OUTBOX);
console.log(Status.DRAFT);
console.log(Status.FAILED);
var sentStatus = Status.SENT;
console.log(sentStatus);

```

If you print Status in console. You will get this Output.

```js
Object {
    0: "SENT",
    1: "OUTBOX",
    2: "DRAFT",
    3: "LIVE",
    4: "FAILED",
    SENT: 0,
    OUTBOX: 1,
    DRAFT: 2,
    LIVE: 3,
    FAILED: 4}
```

### any

`any` data type allows to you use any data type. You could you change your data
type dynamically.

```ts
let person : any = 'Haider Malik';
 console.log(person);

 person = {
   firstName:'Haider',
   lastName:'Malik'
 }

console.log(person);
```

`output`

```bash
Haider Malik
{
firstName :'Haider',
lastName : 'Malik'
}
```

### types with function

```ts
function getName() : string {
    return 'Yellow Man'
}

```

- First keyword would be function
- Second would be the name of your function
- annotate with return type

This `getName()` must return the string value.If you will return any
other data type value number or boolean then TypeScript will give you
error.

### void

If you have a function that returns nothing. You can specify void
return type of that function

```ts
function greeting() : void {
  console.log('Hello Haider');
}
```

### types with function arguments

You can also set type for function arguments or parameters

```ts
function multiply(value:number, value2:number) :number {

   return value * value2;
}

console.log(multiply(2,3));

```

### function types

You can also set type of function.

```ts

function add(val1 : number, val2: number) : number {
  return val1 + val2;
}

let sum = (val1 : number ,val2 : number) => number;

sum= add;

console.log(sum(1,2));
```

I have set a function type for `sum()` .This function will accept
two number values and return only number value;

### Objects and types

You can also create an type for object literal. Let me explain it with example

```ts

 let user: {name : string , age: number} ={
   name:'Haider',
   age:23
 };

user ={
  name:'Jan',
  age:24
};

```
 We have set the type for this `user` object. This user only accepts
`name` property and `age` property. `name` must be string. `age` must
be number.

If you would like to add optional property , you can do this by using
`?` symbol

```ts
let user : { name: string , age: number, cninc?: string} = {
  name:'Haider',
  age:12
};

user ={
  name:'Jan',
  age:24
};

```
Now `cninc` is an optional property.

### example

```ts
let person : { marks:number[] , totalMarks: (includeAvg:boolean) => number} =  {
    marks :[],
    totalMarks:(includeAvg:boolean) => 0
};

person.marks = [80,50,60,70,70];

person.totalMarks= function(includeAvg:boolean) {
    return includeAvg ? 88.0 : 90.0;
};

console.log(person.totalMarks(true));

```

This `person` object will have `marks` property and `totalMarks()` function.we also defined types for `totalMarks()`.


### Custom type

If you want to create multiple objects for same type. You can create
your own custom type by using `type` keyword.

```ts
type Employee = {
  name : string,
  age: number
};

let manager : Employee = {
  name:'Haider',
  age: 23
};

let salesMan : Employee = {
  name :'Jane',
  age :22
};

```

### union

If you know the different data types of same variable you can declare the
variable using `|` operator.

```ts
let age : string | number = 27;
age ='27';
```

We can assign number value and string value to age variable.


### never

The `never` type is used in TypeScript to denote this bottom type. Cases when it occurs naturally:

- A function never returns (e.g. if the `function body has while(true){})`
- A function always throws (e.g. in `function foo(){throw new Error('Not Implemented')}` the return type of foo is never)

```ts
function neverReturns () : never {
    throw  new Error('An Error');
}

```


 {% include disqus.html %}
