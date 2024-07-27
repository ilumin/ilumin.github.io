---
title: Why Data Structures & Algorithms Matter
layout: post
date: 2024-07-27
description: ทำไม data structures และ algorithms จึงสำคัญ
tags: general
---

ถ้าเราต้องการจะ print เลขคู่ที่น้อยกว่า 100 เราจะเขียน code อย่างไร?

option 1:
```js
function print_even() {
  let num = 0;

  while (num < 100) {
    if (num % 2 === 0) console.log(num)
    num++
  }
}
```

option 2:
```js
function print_even() {
  let num = 0;

  while (num < 100) {
    console.log(num)
    num += 2
  }
}
```

option 1 ต้องรัน 100 ลูป ส่วน option 2 รันแค่ 50 ลูป ... เท่านี้ เราน่าจะชัดเจนนะว่า data structure และ algorithm สำคัญไหม