# Project Guideline

ทั้งนี้ทั้งนั้น การจัดวาง Structure นั้น ตามจริงแล้วสามารถยืดหยุ่นได้
ไม่มีถูกผิดซะทีเดียว ซึ่งมันแล้วแต่คน หรือสำคัญกว่านั้น ขึ้นอยู่กับทีมหรือ
แนวทาง/Convention ของแต่ละบริษัท แต่ละที่
สำคัญคือพยายามทำให้เป็นแบบเดียวกันทั้งโปรเจกต์
เพื่อลดอาการงงงวยให้กับคนอื่นและตัวเองในอนาคต

## Overview

```txt
|--- src/
      |--- Main.jsx
      |--- router.jsx                                       -- จัด Route ตรงนี้
      |--- styles/
              |--- global.css                               -- ของเว็บเรา
              |--- index.css                                -- ของ shadcn/ui
      |--- pages/
              |--- Home/                                    -- ตัวอย่างหน้าหลัก
                      |--- index.js                         -- Export แค่ Home.jsx อื่น ๆ ไม่ต้อง
                      |--- Home.jsx
                      |--- Home.module.css                  -- Optional: ใช้ได้แค่ในไฟล์ที่ Import
                      |--- hooks/                           -- Optional: ใช้แค่ที่ Home.jsx, components/*
                      |--- components/
                              |--- index.js
                              |--- Card/                    -- ตัวอย่างจัดเต็ม
                                      |--- Card.jsx
                                      |--- Card.module.css  -- Optional: ใช้ได้แค่ในไฟล์ที่ Import
                                      |--- index.js
                              |--- Button.jsx               -- ตัวอย่างแบบ Minimal
      |--- components/
              |--- ui/
              |--- customs/                                 -- Component ใช้ซ้ำ
              |--- layouts/                                 -- ในไฟล์มี <Outlet /> ของ React Router

      -- ตั้งแต่ตรงนี้ไม่ได้สร้างเอาไว้ให้ตอนแรก ถ้าเรียกใช้หลายที่ ก็มาสร้างที่ระดับนี้ได้
      |--- hooks/                                           -- ใช้มากกว่า 1 หน้า
```

## Detail Explanation

### ชั้นบนสุด

- **router.jsx**: จัดการ Route ต่าง ๆ ตรงนี้ มีการ Import ทั้ง Component
  ที่เป็นหน้าเว็บนั้น ๆ แต่ละ Widget (Header, Card, ฯลฯ), หรือ ไฟล์ Layout
  (`Default.jsx`, `Minimal.jsx`, ฯลฯ)

### ชั้นที่ 2 `style/`

- **global.css**: CSS สำหรับแอพของเราเลย คือ ปล่อย `index.css` ให้เป็นที่ของ
  shadcn/ui ไป

### ชั้นที่ 2 `components/`

เราจะสร้างของต่างที่เราสร้างมือใน `customs/` ส่วน `ui/` เราปล่อยให้เป็น
shadcn/ui เขาจัดการ

- **customs/**: โฟล์เดอร์สำหรับสร้าง Component พวก Widget ที่มีการใช้ซ้ำหลาย ๆ
  ที่ ผมคิดว่าแค่เริ่มใช้ 2 ที่ขึ้นไปก็สร้างไว้ตรงนี้ได้แล้ว

- **layouts/**: ไฟล์โครงสร้างหน้าเว็บ ส่วนใหญ่จะมีแค่ Component จาก
  `src/components/customs/*` ที่ถูก Import มาใช้ตรง ๆ ที่นี้ เช่น `Header.jsx`,
  `Footer.jsx`, `Sidebar.jsx`, ฯลฯ

### ชั้นที่ 3 Component หน้าเว็บ ในโฟลเดอร์ `pages/`

เดี๋ยวผมลองยกตัวอย่างเป็นหน้า Dashboard สมมติว่าในโฟลเดอร์ `Dashboard/` มี

```txt
|--- Dashboard/
        |--- hooks/                                 -- Hooks ของ Dashboard
        |--- components/                            -- ถ้าเราจะแชร์กันแต่ละหน้าย่อย
                |--- ...
                |--- index.js
        |--- MyAccount/
                |--- hooks/                         -- Hooks ของหน้าย่อยของ Dashboard
                |--- components/                    -- ถ้าใช้แค่หน้านั้นหน้าเดียว
                        |--- ProfileImage.jsx       -- แบบปกติ ไฟล์เดียวจบ
                        |--- ProfileForm/           -- ถ้ามันซับซ้อน หรือเราจะจัดเต็ม
                                |--- ProfileForm.jsx
                                |--- ProfileForm.module.css
                                |--- index.js       -- ไฟล์ประจำโฟลเดอร์ย่อยแต่ละอัน
                |--- index.js
        |--- ...
```

เพราะหน้า Dashboard มีหลายหน้าย่อยเราก็จะสร้างโฟลเดอร์ย่อย ๆ ในนั้นอีก

```jsx
// ใน Card.jsx
export function Card() {
  //...
}

// ใน index.js
export * from './Card'; // Export ทุกอย่าง (*) จากไฟล์นั้น ๆ

// ใน Home.jsx
import { Card } from './components';

// สามารถใช้ได้ถ้าไม่ใช้ `index.js` // แต่จะยาวและไม่สวยเวลามีหลายไฟล์ใน
import { Card } from './components/Card';
```

> [!NOTE]
>
> `index.js` ในที่นี้ คือไฟล์สำหรับเขียนให้ Export ไฟล์อื่น ๆ ในโฟล์เดอร์นั้น
> ทำให้เวลาเรียกใช้ที่อื่น เราเขียนสั้นลง และ Clean ขึ้น

สมมติว่าในโฟลเดอร์ `components/` มี

```txt
|--- Home.jsx
|--- components/
            |--- Card.jsx
            |--- index.js
```

```jsx
// ใน Card.jsx
export function Card() { //... }

// ใน index.js
export * from './Card' // Export ทุกอย่าง (*) จากไฟล์นั้น ๆ

// ใน Home.jsx
import { Card } from './components'

// สามารถใช้ได้ถ้าไม่ใช้ `index.js` // แต่จะยาวและไม่สวยเวลามีหลายไฟล์ใน
import { Card } from './components/Card'
```
