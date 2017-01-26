---
layout: dark-post
title: "Interfaces in TypeScript"
description: "Understanding Interfaces"
tags: [TypeScript]
comments: true
image:
    feature: ts-logo.jpg
categories: [TypeScript]
share: true
---

### Interfaces

Interfaces are code contracts with your code. Interfaces are used to declare the structure of variables or function.

```ts
interface Module {

     name : string;
     providers :any[];
     bootstrap: any;
     imports: any[];
     exports : any [];
     moduleId ? : string;  //optional field
 };
 function builtModule(module : Module) : Module {
     return module;
 }
 console.log(builtModule({
     name:'Users',
     providers:['mod1','mod2'],
     bootstrap:'App.ts',
     imports:['Http','FormModule'],
     exports:['HeaderComponent']
 }));

```
 I have defined a structure for `Module` interface. Whenever you need
 to use this interface in your code. You must have all `Module` properties.
 I have passed all the required properties in `builtModule()`. `moduleId` is an optional field.

#### Methods in interface

 ```ts
 interface Module {

     name : string;
     providers :any[];
     bootstrap: any;
     imports: any[];
     exports : any [];
     isLoaded:(name : string) => boolean
 };

 const userModule : Module = {
      name :'Users',
      providers: ['Router','Services'],
      bootstrap: ['app.ts'],
      imports:['Http','FormModule'],
      exports:['MainComponent'],
      isLoaded:(name : string) :boolean => {
          return name === 'Users' ? true : false;
      }
     };

     console.log(userModule);
 ```
We can also define methods in Interfaces.

#### Interface with classes

We can also implements interface in classes.

```ts
class UserModule implements Module {
        name : string;
        providers :any[];
        bootstrap: any;
        imports: any[];
        exports : any [];
        constructor(name : string){
            this.name = name;
        }
        isLoaded(name : string){
            return true;
        }
    }
    let user = new UserModule('Users');
    console.log(user.isLoaded('Users'));
```

#### Interface Inheritance

```ts
interface BrowserModule extends Module {
    cache : any [];
    browserName : string;
};
 const myBrowser : BrowserModule = {
    name : 'Google Chrome',
    providers :['ROUTER','SERVICE'],
    bootstrap: 'AppComponent',
    imports: ['Http','Form'],
    exports : ['BrowserComponent'],
    cache: ['Anything'],
    browserName:'Chrome',
    isLoaded:(name : string) :boolean => {
        return true;
       }
};

console.log(myBrowser);
```

`BrowserModule` can access all the properties of `Module` interface. So in this way we can add more additional properties to `BrowserModule`.

 {% include disqus.html %}
