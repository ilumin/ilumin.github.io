---
title: Tauri Frameless
layout: post
date: 2024-07-14
description: ทำ frameless window บน Tauri
tags: react, rust, tauri
---

# ทำ frameless window บน Tauri

> note: ใช้ Tauri v1

เราสามารถทำได้ 2 ท่า คือ 

1. ซ่อน title bar ไปเลย
2. ทำ overlay title bar หรือ เอา layout มาวางทัย title bar ซะ

แต่ไม่ว่าจะแบบไหน ต้องแก้ 2 จุด คือ 

- Tauri config
- Frontend (สร้าง component ที่จะมารองรับ title bar behavior)

## ซ่อน title bar 

แก้ `src-tauri/tauri.conf.json` 

```json
{
  "tauri": {
    "allowList": {
      "window": {
        "all": true
      }
    },
    "windows": [
      {
        "decorations": false,
      }
    ]
  }
}
```

อธฺบายสิ่งที่เกิดขึ้น

- `tauri.allowList.window.all` คือ การปรับให้สามารถใช้ window behavior ได้ที่ฝั่ง frontend
- `tauri.windows.decorations` คือ การบอกให้ซ่อน title bar ซะ

เมื่อแก้ config นี้ไปแล้ว tauri จะ reload และเปิดหน้าต่างใหม่ ซึ่งจะไม่มี title bar ให้เห็น

เราจะต้องไปเพิ่ม component และจัด layout เพื่อสร้าง title bar เอง

```ts
const TitleBar = () => {
  return <div data-tauri-drag-region className="title-bar" />
}
```

อันนี้คือการเพิ่ม component สำหรับ title bar ซึ่งจะสำคัญที่ต้องมี `data-tauri-drag-region` ด้วย ไม่งั้นไม่สามารถลาก window ได้

ซึ่งการซ่อน title bar เนี่ย จะติดปัญหาที่ window จะกลายเป็นเหลี่ยมๆทันที และเราจะไม่สามารถทำ rounded corner ได้

ดังนั้นถ้าอยากได้ rounded window น่าจะต้องใช้ท่าต่อไป คือ 

## overlay title bar 

คือแทนที่จะซ่อน title bar ก็ทำให้ app วางทัยบน title bar ซะเลย ซึ่งจะพิเศษตรงที่ พวกปุ่ม maximize, minimize และ close ยังอยู่เหมือนเดิม รวมทั้ง window ก็ยัง rounded เหมือนเดิม (เป็นค่า default ของแต่ละ OS)

ซึ่งการแก้ไขจะแตกต่างจากการซ่อน title bar แค่ที่ `tauri.conf.json`

```json
{
  "tauri": {
    "allowlist": {
        "all": true,
    },
    "window": [
      {
        "titleBarStlye": "Overlay",
        "hiddenTitle": true
      }
    ]
  }
}
```
