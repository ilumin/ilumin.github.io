---
layout: post
title: เราจะเลือก complexity แบบไหน
date: 2024-05-13
description: เอาแบบไหนระหว่าง ยากฝั่งเรา หรือ ยากฝั่งลูกค้า
tags: ddd
categories: solution-architecture
# featured: true
---

สำหรับอาชีพที่เกี่ยวข้องกับการเขียนโปรแกรม ไม่ว่าจะเป็น software engineer หรือ software architecture เราคงหลีกเลี่ยงไม่ได้หรอก ที่จะต้องเจอกับปัญหา ก็เราต้องแก้ปัญหาให้ลูกค้านี่นา แก้ปัญหาด้วยเทคโนโลยีเพื่อให้เค้าสามารถทำงานได้สะดวก

แน่นอนว่าการแก้ไขมันก็หลีกเลี่ยงไม่ได้ ว่าจะมีความซับซ้อน หรือ complexity อยู่ในนั้นด้วย

complexity ที่ว่าเนี่ย มีคนจำแนกมันออกมาได้หลายประเภทมากๆ แต่ตัวที่เราควรจะต้องสนใจมีอยู่ 2 ประเภทคือ 

1. complexity ที่ทำให้คนใช้งาน ใช้งานได้ยาก
2. complexity ที่ทำให้คนเขียนระบบ เขียนได้ยาก

โดยปกติแล้ว 2 ตัวนี้เป็นสิ่งที่ trade off กัน หรือ ได้อย่างก็ต้องเสียอย่าง

แล้วเราควรจะเลือกสร้าง complexity แบบไหน? ถ้าตอบสั้นๆคือแบบแรกเถอะ คนใช้งานจะได้ happy

---

เราลองมาดูตัวอย่าง code เพื่อแยกแยะ complexity ทั้ง 2 ตัวนี้ดีกว่า

Code A
```ts
class A {
  b: B;
  c: C;

  constructor(b: B, c: C) {
    this.b = b;
    this.c = c;
  }
}
```

Code B
```ts 
class A {
  b: B;
  c: C;

  constructor(a) {
    this.b = new B(a/2);
    this.c = new C(a/3);
  }
}
```

code ทั้ง 2 ตัวนี้ให้ผลัพธ์เดียวกันคือเป็น `class A` แต่แตกต่างกันที่ ชุกแรกจะ inject object ของ class C และ class B ไปใน construct ส่วนชุดที่ 2 นั้นจะใช้วิธีการสร้าง object ใน construct แทน

- Code A
  - ใช้วิธี inject object ลง constructor
  - ความซับซ้อนอยู่ที่ฝั่ง client หรือคนที่ต้องการใช้งาน class A ที่ต้องรู้ว่าจะสร้าง class B และ C อย่างไร
  - แบบนี้คือ การสร้างความซับซ้อนที่ฝั่งผู้ใช้งาน
- Code B
  - ใช้วิธีสร้าง object ใน constructor
  - ความซับซ้อนอยู่ที่ฝั่งคนเขียน ที่ต้องรู้ว่า class B และ C สร้างอย่างไร (ซึ่งต้องรู้อยู่แล้ว)
  - แบบนี้คือ การสร้างความซับซ้อนที่ฝั่งคนเขียน

ลองคิดดู ว่าแบบไหนจะเกิดบั๊คง่ายกว่ากัน ... มันก็ต้องแบบแรกใช่ไหม เพราะนอกจากไม่ต้องให้คนใช้งานรู้รายละเอียดบางอย่าง เรายังสามารถจัด logic ให้อยู่ในที่ๆเดียวได้ด้วย

---

แต่ถ้าการสร้าง object ของ class B และ C ไม่ได้มีความซับซ้อนอะไร เราก็สามารถใช้แบบแรกได้นะ ก็มันไม่เกิด complexity ไม่ต้องมี logic พิเศษ แล้วเราจะไปเพิ่มความซับซ้อนในฝั่งเราทำไม