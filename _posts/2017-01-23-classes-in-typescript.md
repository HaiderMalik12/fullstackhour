---
layout: dark-post
title: "Classes in TypeScript"
description: "Learn Classes in TypeScript"
tags: [TypeScript,Es6]
comments: true
image:
    feature: ts-logo.jpg
categories: [TypeScript,Es6]
share: true
---

### Classes

```ts
class Employee {

    //can access outisde the class
    public name : string;
    //access only those objects that inherit from Employee
    protected age: number;
    //access only inside the Employee class
    private mobile : string;
    constructor(name:string ,age:number, mobile:string){
        this.name = name;
        this.age = age;
        this.mobile = mobile;
    }
    getName(){
        return this.name;
    }
    setName(name:string){
        this.name = name;
    }
    getAge(){
        return this.age;
    }
    setAge(age:number){
        this.age = age;
    }
    getMobile(mobile:string){
        this.mobile = mobile;
    }
}

let emp = new Employee('Haider',23,'04329-20930232');
emp.setName('Malik');
console.log(emp.getName());

```

### Inheritance

```ts
class Manager extends  Employee {
    constructor(name : string, age: number , mobile : string){
        super(name,age,mobile);
        this.age = 24;
    }
}
let manager = new Manager('Jane',23, '0343-23332233');
console.log(manager.getName());
console.log(manager.getAge());
```
You can access the public and protected members of Employee class

### Getters and Setters

There is a better way to define getter and setter in TypeScript.

```ts
class Actor {
    private _name : string;
    constructor(_name:string){
        this._name = _name;
    }
    set name (value: string){
        this._name = value;
    }
    get name (){
        return this._name;
    }
}
let actor = new Actor('Haider Malik');
console.log(actor.name);
//set
actor.name = 'Jane Doe';
console.log(actor.name);
```

### Static Properties and Methods

If you need some properties or methods in multiple time in your project.
You could create static method and static properties.For static properties
and methods you do not need to instantiate the Object.

```ts
class Helpers {
    static PI : number = 3.14;
    static calcCircumference(diameter: number) :number {
        return this.PI * diameter;
    }
}
console.log(2 * Helpers.PI);
console.log(Helpers.calcCircumference(44));
```

### Abstract Classes

Abstract class does not need to instantiate .It just contains the implementation details for its members.

```ts

abstract class Product {
    productName : string = "Default";
    price :number = 1000;
    abstract changeName(name: string): void;
    calcPrice(){
        return this.price;
    }
}
class Mobile extends  Product {
    changeName(name : string) : void {
        this.productName = name;
    }
}
let mobProduct = new Mobile();
console.log(mobProduct);
mobProduct.changeName("Super It Product");
console.log(mobProduct);
```

If you have made abstract method in abstract class. You must need to write implementation for abstract method in derived classes.

### Private Constructor

Private constructor is helpful to create singleton class. If you want to instantiate only one instance of a class. You can make a singleton class.

```ts
class Service {
    private static instance: Service;
    private constructor(public name : string) { }
        static getInstance()
        {
            if (!Service.instance) {
                Service.instance = new Service('SingletonService');
            }
            return Service.instance;
        }
}
// let service = new Service('Hello WOeld'); // wont work
let service = Service.getInstance();
```

### Readonly properties

```ts
class Service {
    private static instance : Service;
    public  readonly name : string;
    private constructor(name : string) {
        this.name = name;
    }
        static getInstance()
        {
            if (!Service.instance) {
                Service.instance = new Service('SingletonService');
            }
            return Service.instance;
        }
}
let service = Service.getInstance();
// service.name = 'MyService'; won't work
console.log(service.name);
```
You are not allowed to change the `name` property becuase it is `readonly`
property.

 {% include disqus.html %}
