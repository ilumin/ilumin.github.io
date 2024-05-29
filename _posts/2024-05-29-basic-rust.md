---
title: Basic Rust
layout: post
date: 2024-05-29
description: Assume that this is my first time with Rust
tags: rust
categories: etc
---

บันทึกความเข้าใจ เกี่ยวกับ Rust 

```rs
use std::io::stdin;

fn main() {
    println!("Hello, what's your name?");

    let mut your_name = String::new();

    stdin()
        .read_line(&mut your_name)
        .expect("Failed to read line");

    println!("Hello, {}", your_name);
}
```

โค้ดนี้ทำหน้าที่รับ input และปริ้น Hello, input

แล้วแต่ละส่วนทำอะไรบ้างล่ะ

```rs
let mut your_name = String::new();
```

- โดยปกติตัวแปรของ Rust เป็น immutable หรือ ไม่ยอมให้เปลี่ยนแปลงข้อมูล
- เวลาที่เราต้องการสร้างตัวแปรที่ต้องการเปลี่ยนแปลงข้อมูลได้ เราต้องเพิ่ม `mut` ไป

```rs
stdin()
    .read_line(&mut your_name)
    .expect("Failed to read line");
```

- ตรงนี้น่าจะเดาได้ `read_line()` คือฟังก์ชั่นที่ทำหน้าที่รับ input มาเก็บลงตัวแปร
- สำหรับ Rust ถึงแม้ว่าจะบอกให้ตัวแปรเป็น mutable แล้ว การเปลี่ยนแปลงค่าก็ยังต้องทำสิ่งที่เรียกว่า borrow อธิบายง่ายๆคือเราเปลี่ยนแปลงด้วย reference ไม่ได้เปลี่ยนแปลงตรงๆ
  - สามารถทำได้โดย `&mut your_name`
  - ในกรณีที่จะ read ก็จะต้องใช้ borrow ด้วย ซึ่งจะใช้ด้วย `&your_name`
