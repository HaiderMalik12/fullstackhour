---
layout: dark-post
title: "NameSpaces and Modules in TypeScript"
description: "Understanding NameSpaces and Modules"
tags: [TypeScript]
comments: true
image:
    feature: ts-logo.jpg
categories: [TypeScript]
share: true
---

### NameSpaces

Namespaces are simply named JavaScript objects in the global namespace. This is commonly used in javascript for making sure that stuff does not leak into global namespace.

```ts
namespace  Util {
    export  function log(msg: string){
        console.log(msg);
    }
    export function error(msg:string){
        console.error(msg);
    }
}

Util.log('Hello World');
Util.error('May Be!!');

console.log(Util);

```
Here is complied javascript version of typescript namespace.

```js
var Util;
(function (Util) {
    function log(msg) {
        console.log(msg);
    }
    Util.log = log;
    function error(msg) {
        console.error(msg);
    }
    Util.error = error;
})(Util || (Util = {}));
//Usage
Util.log('Hello World');
Util.error('May Be!!');
console.log(Util);

```

You can also embed namespace inside another namespace.

```ts
namespace  Util {
    export  function log(msg: string){
        console.log(msg);
    }
    export function error(msg:string){
        console.error(msg);
    }
    export namespace Validator {
        export function isValidString(value:string) {
            return value;
       }
    }
}
console.log(Util.Validator.isValidString('Hello WOrld'));
```

Modules

You can organize a large project code into modules.

```ts
//math/circle.ts
export const PI = 3.14;
export function getDiameter(diameter : number) : number {
    return diameter * PI;
}
```

```ts
//math/rectangle.ts
export function calRectangle (width : number , length :number ){
    return width * length;
}

```

```ts
//app.ts
import {calRectangle} from './math/rectangle';
import {getDiameter} from './math/circle';

console.log(calRectangle(20,4));
console.log(getDiameter(3000));
```


 {% include disqus.html %}
