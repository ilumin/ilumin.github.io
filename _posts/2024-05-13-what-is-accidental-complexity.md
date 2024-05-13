---
layout: post
title: Accidental Complexity คืออะไร
date: 2024-05-13
description: ความซับซ้อนโดยอุบัติเหตุงั้นเหรอ 🤔
tags: ddd
categories: solution-architecture
# featured: true
---

> ##### TLDR;
> 
> **Accidental Complexity** ไม่ได้แปลว่า ความซับซ้อนโดยอุบัติเหตุ และไม่ใช่คำศัพท์ทั่วไป มันคือคำเฉพาะในบริบทของ Domain-Driven Design (DDD) ซึ่งจะหมายถึง ความซับซ้อนเกินความจำเป็นที่ถูกใส่เข้าไปในโค้ด
{: .block-tip }

---

**Accidental Complexity** คือความซับซ้อนในโค้ด ที่เราอาจจะสร้างมันขึ้นมาโดยไม่ได้ตั้งใจ ซึ่งมันอาจจะมาจาก 

- ใช้ design pattern ที่มันซับซ้อนเกินไป 
- ทำ duplicate code
- ใช้ naming convention ที่ไม่ชัดเจน
- ฯลฯ

ซึ่งโดยปกติ สิ่งเหล่านี้จะทำให้โค้ดของเราซับซ้อน เข้าใจยาก และดูแลรักษายาก (แก้ไขยาก เทสยาก เพิ่มฟีเจอร์ยาก)

แนวทางในการลด Accidental Complexity 
- ทำอะไรง่ายๆบ้าง (keep it simple)
- ทำตาม best practice
- พยายามเขียนและออกแบบโค้ดให้มันสื่อสารอย่างตรงไปตรงมา

สำหรับใน DDD เราควรระวังการสร้าง accidental complexity ใน domain model (model หลักที่เก็บ business logic) เราควรทำให้ model simple ที่สุดเท่าที่จะเป็นไปได้ และที่สำคัญไม่ควรเอา logic อื่นๆที่ไม่เกี่ยวข้องกับ business เช่น การทำ database query เพื่อป้องกันผลกระทยจากการเปลี่ยนแปลงของ component อื่นๆจะมากระทบกับ business logic
