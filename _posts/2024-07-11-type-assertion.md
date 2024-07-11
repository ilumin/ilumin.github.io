---
title: Type Assertion
layout: post
date: 2024-07-11
description: ทำ type assertion ด้วย TS
tags: typescript
---

โดยปกติในจักรวาล JS เราจะทำแบบนี้

```js
function assertNumber(value) {
  if (typeof value !== "number") 
    throw Error("Expected value to be number")
}
```

ในจักรวาล TS เราก็ใช้ implementation code คล้ายๆกันแหละ แต่ปัญหาคือ type ของ function จะเป็นอะไร

```ts
function assertNumber(val: any): asserts val is number {
  if (typeof value !== "number") 
    throw Error("Expected value to be number")
}
```
