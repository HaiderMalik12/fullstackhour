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

#### string

```ts
 let firstName : string = 'Haider';
```

#### number

```ts
let age : number = 23;
```

#### boolean

```ts
let isApplied : boolean = true;
```

#### array

```ts
let shirts : string[] =['Levis','Outfiters','Cross Road'];
```

You can create an array of multiple data types by using `any` data type

```ts
let myArr : any[] =['Hello',1,false];
```

#### tuples

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

#### enum

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

enum will map your values to numeric values, by default it starts from
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

 {% include disqus.html %}
