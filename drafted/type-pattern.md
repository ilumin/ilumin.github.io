---
title: Type Pattern
layout: post
date: 2024-07-**
description: ทำ type pattern ด้วย TS
tags: typescript
---

```ts
type AllElements = HTMLElementTagNameMap & 
  {
    [elm in `${string}-${string}`]: HTMLElement
  }

const a = createElement('a')
const c = createElement('new-element')
const d = createElement('thisWillError')
//                       ^
// Argument of type 'thisWillError' is not assignable
// to parameter of type `${string}-${string}` keyof HTMLElementTagNameMap
```

```ts
type EventName = `on${string}`
```

เค้าเรียกว่า String Literal Type 