---
title: Rust str and String
layout: post
date: 2024-05-30
description: What's the difference between str and String
tags: rust
categories: etc
---

บันทึกเกี่ยวกับความเข้าใจ type str และ String ของ Rust

> Rust has two types of strings, which can be a source of confusion for new Rust programmers. The first type is `str`. These types are generally used as string *literals*, which are strings entered in the source code and generally unchanging. The second type is the `String`. Strings are dynamic because they store a location, length, and capacity. You can append Strings and edit them.

- `str` เป็นข้อมูลที่จะไม่มีการเปลี่ยนแปลง
- `String` เป็นข้อมูลที่จะถูกเปลี่ยนแปลงและแก้ไขตลอด

ดังนั้นอะไรที่เราคิดว่าจะไม่เปลี่ยนแปลง เช่น config หรือ constant เราควรใช้ `str` ส่วนอะไรที่จะเปลี่ยนแปลงควรใช้ `String`

ตัวอย่างจาก [[2024-05-29-basic-rust]] การรับชื่อมาจาก `read_line` ซึ่งมันจะถูกเอามาทำ trim ในเคสนี้เราควรใช้ `String`
