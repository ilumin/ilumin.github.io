---
title: What's End-to-End Testing (E2E testing)
layout: post
date: 2024-06-14
description: E2E test คืออะไร
tags: etc
---

> End-to-end testing is a software methodology that assesses the operation of an application from beginning to end, simulating real-world user scenarios. It involves testing the entire software system, including all its components, integrations, and interfaces, to ensure that it functions as expected under realistic conditions.
> -- ChatGPT

AI เจ้าหนึ่งบอกว่ามันคือการ test software จาก**ต้นจนจบ** (from beginning to end) ด้วยการจำลองการใช้งานจริงๆของ user ซึ่งจะต้องเทสรวมไปทั้ง components, integrations, และ interface (น่าจะหมายถึง UI)

จากประโยคดังกล่าว สิ่งที่น่าสนใจมี

- เทสโดยจำลองการใช้งานจริงๆของ user
- เทสทั้งระบบ คือต้องเปิดทั้งระบบมารัน

## ประเด็นแรก "เทสโดยจำลองการใช้งานจริงๆของ user"

หรือเทสตาม user scenario หรือ use case นั่นเอง

ดังนั้นมันจึงเป็นการทดสอบแค่บางส่วนของระบบ แต่ไม่ใช่การทำงานทั้งระบบ และมันจะสมเหตุสมผลถ้าเราทดสอบการทำงานตั้งแต่เริ่มต้นจนจบ user scenario ซึ่งแน่นอนว่าเราควรจะต้องเลือกมาเฉพาะ happy case และ alternate case ที่สำคัญและน่าสนใจ

## ประเด็นที่สอง "เทสทั้งระบบ คือต้องเปิดทั้งระบบมารัน"

นี่คือสิ่งที่เป็นปัญหา และสามารถหยิบมาถกเถียง

แน่นอนว่าทดสอบทั้งระบบย่อมดีที่สุดอยู่แล้ว แต่มันขึ้นอยู่กับว่าโครงสร้างและการแบ่งงานของทีม

ในกรณีที่

### 1. ทีม fullstack

การทดสอบแบบ end-to-end อาจจะสมเหตุสมผลถ้าเราทดสอบโดนรันเทสโดยเปิดระบบขึ้นมาทดสอบ

เพราะทีมรับผิดชอบหมดทั้ง frontend และ backend 

ทั้งนั้นทั้งนี้ ขึ้นอยู่กับการแบ่งงาน ถ้าแบ่งงานกันตามปกติ คือ 1 ทีมรับผิดชอบใน 1 epic/feature/subdomain ก็น่าจะสามารถทำ E2E ได้โดยไม่มีปัญหาอะไร

แต่ถ้ามีความเพี้ยนในการจัดการ ให้ epic หรือ feature หนึ่งให้ทีมมาทำงานร่วมกัน ในแบบที่เป็น horizontal การทำ E2E ก็อาจจะลำบากหน่อยนึง เพราะหน้าที่ความรับผิดชอบมันซ้อนกัน

### 2. ทีม frontend 

การทดสอบแบบ end-to-end อาจจะสมเหตุสมผลถ้าเราทดสอบโดยการรัน frontend app ขึ้นมาจริงๆ แต่ใช้ mock API ในการทดสอบ

ด้วยเหตุผลเดียวกับกรณีแรก ก็ทีมทำแค่ frontend นี่นา 

ดังนั้นการออกแบบและจัดการงานจะต้องมีการกำหนด contract กันตั้งแต่แรกว่าจะใช้ API อะไร มี request/response หน้าตาแบบไหน

### 3. ทีม backend 

การทดสอบแบบ end-to-end อาจจะสมเหตุสมผลถ้าเราทดสอบโดยการรัน backend app ขึ้นมาจริงๆ ซึ่งโดยปกติเราจะเรียกว่า API testing 
