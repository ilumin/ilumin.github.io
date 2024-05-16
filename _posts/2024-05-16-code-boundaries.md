---
layout: post
title: code boundaries
date: 2024-05-16
description: code boundaries ไม่ใช้ friend zone
tags: ddd, clean code
categories: solution-architecture
# featured: true
---

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="https://www.youtube.com/embed/DNIDBbjqFCo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

ทุกสิ่งอย่างล้วนอยู่มีขอบเขต การทำอะไรที่อยู่นอกขอบเขต ล้วนทำให้เกิดความลำบากและอาจจะเจ็บปวด เหมือน friend zone นั่นแหละ

แต่สำหรับการเชียนโปรแกรมแล้ว มีคนนิยามเรื่องขอบเขต (boundaries) ไว้เยอะเหมือนกัน ซึ่งใน clean code เค้าจะแบ่งมันเป็น 

- external boundary: code ที่เราไม่ได้เขียน อาจจะเป็น external API, package อื่น หรือแม้แต่ code ที่ทีมอื่นมาเขียน
- internal boundary: แนกำ ที่เราหรือทีมเราเขียนเอง

ที่เค้าแบ่งเป็นแบบนี้เนี่ย เพื่อที่ให้เราออกแบบ code ของเราให้พยายามอย่าไปรู้หรือเอารายละเอียดของ external boundary มาใส่ใน internal boundary เพราะมันเทสยาก ควบคุมยาก และจะทำให้เกิด dependency กับ external ซึ่งจะทำให้เราลำบากถ้าเค้าแก้ไข หรือที่แย่สุดคือเกิด bug จาก external boundary (ความผิดของเราคือ ไว้ใจเค้า)

ในหนังสือ Learning Domain-Driven Design มีแบ่งขอบเขตออกเป็น 

- logical boundary: แบ่งขอบเขตของ code ออกจากกันด้วย module 
- physical boundary: แบ่งขอบเขตของ code ออกจากกันด้วย service (service จริงๆ เช่น server, container)

เค้าแบ่งอย่างนี้เพื่อที่จะได้แบ่งงาน แบ่งหน้าที่ความรับผิดชอบในแต่ละ bounded context และ subdomain ให้ชัดเจน ซึ่งการจะเอา code ที่อยู่คนละ boundary มาใช้งานในที่เดียวกัน มักจะทำให้เกิดความซับซ้อน และสร้างความลำบากในการดูแลรักษา

---

คำถาม: แล้ว code ที่อยู่ภายใต้ Git repository เดียวกัน แต่มี code บางส่วนที่อยู่ใน Git submodule ที่อีกทีมเค้าทำล่ะ 

ถ้าเป็นแบบนี้ เราถือว่า code ที่อยู่ใน Git submodule อยู่คนละ physical boundary กัน ก็มันอยู่คนละ Git repository กันเลยน่ะ จะมาถือว่ามันเป็น logical boundary ได้ยังงัยกัน

การทำแบบนี้ก็จะสร้างปัญหาในการสื่อสารระหว่างทีม เพราะการแก้ไขของ code ใน Git submodule จะเกิดผลกระทบโดยที่อีกทีมอาจจะไม่รู้ตัว

ทางเลือกอื่นนอกเหนือจากการทำ Git submodule คือ 
- monorepo: เอา code มาไว้ใน repository เดียวกันเลย และให้ monorepo ช่วยจัดการการเอา code ไปใช้ข้าม package ซึ่งจะไม่ทำให้เราต้องเขียน duplicate code มากนัก
- publish package: ก็ publish เป็น package ไปให้ทีมอื่นใช้เลยสิ อย่างน้อยจะสามารถควบคุมเวอร์ชั่นได้ด้วย

---

ถ้าการออกนอกขอบเขต มันไม่ได้ทำให้เราสมหวัง ... ก็อยู่ภายในขอบเขตดีกว่านะ
