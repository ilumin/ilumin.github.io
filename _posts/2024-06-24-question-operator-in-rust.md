---
title: The ? Operator in Rust
layout: post
date: 2024-06-24
description: What the hell is it?
tags: rust
---

เวลาที่อ่าน code ของ Rust เรามักจะเจอ `?` ต่อท้ายฟังก์ชันบ่อยๆ เช่น 

```rust
fn read_file(filename: &str) -> Result<String, std::io::Error> {
    let contents = std::fs::read_to_string(filename)?; // ? used here
    Ok(contents)
}
```

`?` ที่ต่อท้ายฟังก์ชั่น คือ syntactic sugar (การสร้าง syntax สั้นๆ สำหรับงานที่ทำกันซ้ำๆ เช่นของ JS จะมี `[...array]`)

ซึ่งถ้าไม่ใช้ `?` จะต้องเขียนแบบนี้

```rust 
fn read_file(filename: &str) -> Result<String, std::io::Error> {
    let result = std::fs::read_to_string(filename);

    match result {
        Ok(contents) => Ok(contents),  // Success: Return the file contents wrapped in Ok
        Err(err) => Err(err),          // Error: Return the error directly
    }
}
```

หมายความว่า `?` เป็นการลดรูปของ code ที่ใช้เช็คว่า result จาก function มี error ไหม
