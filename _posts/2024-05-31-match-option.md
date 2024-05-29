---
title: Note on Rust match for option
layout: post
date: 2024-05-31
description: We better use match, instead of if...else
tags: rust
categories: etc
---

บันทึกความเข้าใจเกี่ยวกับการใช้ `match` กับ `option`

```rs
use std::io::stdin;

struct Visitor {
    name: String,
    greeting: String,
}

impl Visitor {
    fn new(name: &str, greeting: &str) -> Self {
        Self {
            name: name.to_lowercase(),
            greeting: greeting.to_string(),
        }
    }

    fn greet_visitor(&self) {
        println!("{}", self.greeting);
    }
}

fn main() {
    println!("Hello, what's your name?");

    let name = what_is_your_name();
    let visitor_list = [
        Visitor::new("bert", "Hello Bert, enjoy your treehouse."),
        Visitor::new("steve", "Hi Steve. Your milk is in the fridge."),
        Visitor::new("fred", "Wow, who invited Fred?"),
    ];

    let known_visitor = visitor_list.iter().find(|visitor| visitor.name == name);

    match known_visitor {
        Some(visitor) => visitor.greet_visitor(),
        None => println!("You are not on the visitor list. Please leave."),
    }
}

fn what_is_your_name() -> String {
    let mut your_name = String::new();

    stdin()
        .read_line(&mut your_name)
        .expect("Failed to read line");

    your_name.trim().to_lowercase()
}
```

โค้ดข้างบนเป็น โค้ดที่ refactor จาก [[2024-05-29-basic-rust]] ที่จะเอา input มาเช็คว่าตรงกับรายชื่อที่อยู่ในลิสไหม

ลิสที่ว่าเนี่ย เป็นลิสของ `struct Visitor`

ในโลกของ Rust, struct ก็จะเป็นเหมือน type หรือ interface ในโลกของ Javascript และเราสามารถเพิ่ม behavior ให้มันได้ด้วยการทำ `impl Visitor` 

- `struct Visitor` มี `name` และ `greeting` เป็น property (เอ๊ะ เค้าเรียกว่า property ไหมนะ)
- และเรา `impl Visitor` ให้มี `new()` เปรียบเสมือน `construct` และ `fn greet_visitor()`

ทีนี้การจะเช็คว่า input ที่รับมาเนี่ยมีชื่อตรงกับ `visitor_list` ไหม เราทำได้หลายแบบ เราจะใช้ `for...in` ก็ได้ หรือจะใช้ `iter` (iterator) ก็ได้

แต่การใช้ `for...in` เนี่ย ไม่ค่อยเท่ห์ ต้องสร้างตัวแปรมาคอยเช็ค และทำ `if...else` ในลูปด้วย

เราควรจะใช้ `iter` ดีกว่า ซึ่ง iter ก็คือการวนลูปนั่นแหละ ซึ่งจะสามารถใช้ `find` เหมือนกับ Javascript คือทำการหา item ที่มี pattern ตามที่กำหนด

โดย pattern ที่ว่าเนี่ยจะใช้ closure function `|visitor| visitor.name == name` ถ้าเป็น Javascript มันก็คือ `(visitor) => visitor.name === name` นั่นเอง และค่าที่ได้จาก `find` ก็จะถูกใส่ลงไปใน `known_visitor`

ความพิเศษมันจะเริ่มขึ้นตรงที่ `find` จะรีเทิร์นเป็น `Option<T>` ตรงนี้หมายความว่า มันจะรีเทิร์นเป็น 2 กรณีเท่านั้นคือ 

- `Some<T>` หาเจอ
- `None` หาไม่เจอ

ซึ่งจะแตกต่างจาก Javascript ที่จะรีเทิร์นเป็น type ของ item หรือ undefined (ภาษาอื่นๆอาจจะเป็น null) 

การจะตรวจสอบ `known_visitor` ใน Rust เราจะสามารถใช้ `if...else` หรือ `match` ก็ได้ แต่ใช้ `match` จะดูอ่านง่ายกว่า ดังนั้นในโค้ดเลยเป็น 

```rs
match known_visitor {
    Some(visitor) => visitor.greet_visitor(),
    None => println!("You are not on the visitor list. Please leave."),
}
```

ซึ่งก็จะเหมือน `switch...case` แต่แตกต่างมี `match` เป็นสิ่งที่เรียกว่า pattern matching คือ เราสามารถเปรียบเทียบกับค่าที่เป็น dynamic ด้วย pattern ได้

- `Some(visitor)` ตรวจสอบว่า `known_visitor` มี pattern เหมือน `Some(visitor)` ไหม ถ้ามีก็ทำงานต่อ โดยเอา `visitor` ไปใช้งาน
- `None` ตรวจสอบว่า `known_visitor` มี pattern เหมือน `None` ไหม

ซึ่งใน `switch...case` จะใช้ได้กับ static value อย่างเดียว
