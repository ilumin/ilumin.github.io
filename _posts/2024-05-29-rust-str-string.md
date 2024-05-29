---
title: Rust str and String
layout: post
date: 2024-05-29
description: What's the difference between str and String
tags: rust
categories: etc
---

บันทึกเกี่ยวกับความเข้าใจ type str และ String ของ Rust

> Rust has two types of strings, which can be a source of confusion for new Rust programmers. The first type is `str`. These types are generally used as string *literals*, which are strings entered in the source code and generally unchanging. The second type is the `String`. Strings are dynamic because they store a location, length, and capacity. You can append Strings and edit them.

- `str` เป็นข้อมูลที่เป็น input และโดยปกติจะไม่มีการเปลี่ยนแปลง
- `String` เป็นข้อมูลที่จะถูกเปลี่ยนแปลงและแก้ไขตลอด

ดังนั้นหมายความว่าอะไรก็ตามที่เราได้จาก external ควรใช้ `str` และของที่ใช้ใน internal ควรใช้ `String`
