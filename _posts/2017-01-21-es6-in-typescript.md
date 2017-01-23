---
layout: dark-post
title: "ES6 in TypeScript"
description: "Learn Es6 in TypeScript"
tags: [TypeScript,Es6]
comments: true
image:
    feature: ts-logo.jpg
categories: [TypeScript,Es6]
share: true
---

### let

when you declare a variable using `let` keyword ,it uses block scoping


```typescript

 function greet() :void {

   let message = "Hello";

   if(message) {

     let greetMessage = "Welcome!!";

     console.log(greetMessage);
   }

   console.log(greetMessage); // won't work
 }

```
We are trying to log `greetMessage` at the end of function body .It will not
work because you can access this `greetMessage` variable inside only if block.

### const

`const` is similar to let but you can not change the value of const variable

```ts
const PI = 3.14;
PI = 3.15  //won't work

```

### Arrow function

```ts
 const sum = (num1 : number , num2 : number ) : number => num1 * num2;
 console.log(sum(5,5));

```
If you have a one line in function body you do not need to write a
`return` statement.


### Default parameters

You can also set default parameters in function.

```ts
const sum = (num1 : number =10 , num2 : number =10 ) : number => num1 * num2;
console.log(sum());

```
If you will not pass any arguments to `sum()` .It will take default parameters value `num1 = 10` and `num2 = 10`

### spread operator

Spread operator spreads out array into single values. You do not need to
write complicated loop. It also spreads out array into another array. It can
also spreads out object into another object.

```ts

function add(x:number, y:number, z:number) : void {
        console.log(x,y,z);
    }
    let nums : number[] = [0, 1, 2];

 //bad way
 add(nums[0] , nums[1], nums[3]);

 //good way
 (<any>add)(...nums);
```

In Es5 `add()` will call in this way `add.apply(void 0, args);`

```ts
const fruits = ['apples','oranges','bananas'];
const food = ['burger','fish',...fruits];
console.log(food);
```
`output`

```bash
["burger", "fish", "apples", "oranges", "bananas"]
```

### Rest operator

Rest operator is an opposite of spread operator. It represents infinite number of arguments into array.

```ts
    const sum = (...args: number []) : number => {
        let total = 0;
        args.forEach(num => {
            total + = num
        });
        return total;
    };
    console.log(sum(1,2,3));
    console.log(sum(12,3,4,45));
```

You can pass any number of arguments. In first call we are calculating
the sum of three numbers. In second call we are calculating the sum of four numbers.

### Array destructuring

```ts
const skills:string[] = ['javascript','typescript','node.js','angular2'];

    //bad way
    const skill1:string = skills[0];
    const skill2:string = skills[1];
    console.log(skill1 + " " + skill2);

    //Good way
    const [_skill1, _skill2]= skills;
    console.log(_skill1,_skill2);

```
This creates two new variables `_skill1` and `_skill2`.

### Object destructuring

```ts
let customer :{ name : string , age: number, address: {street:string, zipCode:string}} = {
        name : 'Haider',
        age:24,
        address :{
            street:'5A',
            zipCode:'38000'
        }
    };

    let {name,age,address} = customer;
    console.log(name);
    console.log(age);
    console.log(address);
```
This creates new variables `name`, `age`,`address` from `customer.name` ,`customer.age` and `customer.address`

if you want different keys you can use alias while destructuring properties

` let {name:myName, age:myAge ,address:myAddress} = customer;`

### Template literals

If you want to write complex or multiline string you have to use template
literal

```ts
const userName:string ="Haider";

   //bad way
   const greetMsg: string = "Hello I,m " + userName;
   console.log(greetMsg);

   //good way
   const _greetMsg:string = `
   Hi ${userName}
   Welcome to FullStackHour `;
   console.log(_greetMsg);

```
 {% include disqus.html %}
