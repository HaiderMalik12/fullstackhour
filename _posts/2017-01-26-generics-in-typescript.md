---
layout: dark-post
title: "Generics in Typescript"
description: "Understanding Generics"
tags: [TypeScript]
comments: true
image:
    feature: ts-logo.jpg
categories: [TypeScript]
share: true
---

### Generics

Generics are able to create a component or function to work over a variety of
types rather than a single one.

#### How to use Generics

- Class instance members
- Class methods
- function arguments
- function return value


```typescript
 function print<T>(data : T) {
    return data;
 }
console.log(print<number>(299));
console.log(print<string>("Haider malik"));
console.log(print<Object>({name:'Haider',ag3:23}));
```

### Generics with Arrays

```typescript

const stack : Array<number> = [1,2,34,5];
stack.push(122);
stack.push(222);

const queue : Array<string> = ['haider','malik','john'];
queue.push('Zain');
queue.push('Kygo');

```

### Generics with Classes

You can also create generic class

```typescript
 class Map<T> {
        private map : { [key:string] : T } = {};
        setItem(key: string, item: T){

            this.map[key] = item;
        }

        getItem(key : string){
            return this.map[key];
        }

        clear() {
            this.map = {};
        }

        printMap(){
            for( let key in this.map){
                console.log(key);
            }
        }
    }
    const numberMap = new Map<number>();
    numberMap.setItem("Mobile",2);
    numberMap.setItem("products",10);
    console.log(numberMap.getItem("Mobile"));
    numberMap.printMap();
    numberMap.clear();
    
    const stringMap = new Map<string>();
    stringMap.setItem("Node Js ","Javscript framework");
    stringMap.printMap();
```

You can create `Map` with `string`, `number` or `any` data type.

 {% include disqus.html %}
