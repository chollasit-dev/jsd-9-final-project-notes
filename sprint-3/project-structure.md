# Project Structure

## Overview

ที่เกี่ยวกับ Express App เราโดยตรงมีแค่ใน `/src/` ครับ หลัก ๆ ก็โฟกัสตรงนั้นพอ

```txt
|--- .editorconfig
|--- .prettierrc
|--- .gitignore
|--- nodemon.json
|--- vitest.config.js
|--- package-lock.json
|--- package.json
|--- README.md
|--- .env.example                                           -- เป็นตัว(อ)ย่าง
|--- .env                                                   -- เอาไว้โหลด NODE_ENV อย่างเดียว
|--- .env.local                                             -- ถ้าใช้ Development Environment
|--- .env.production                                        -- ถ้าใช้ Production Environment
|--- src/
      |--- app.js                                           -- รวมร่าง Middleware, Route, Error Handler
      |--- server.js                                        -- เริ่มรัน Server ตรงนี้ (Entrypoint)
      |--- configs/                                         -- เก็บพวกตั้งค่าต่าง ๆ
              |--- env.js
              |--- cors.js
              |--- ...
      |--- models/
              |--- User.js
              |--- ...
      |--- api/v1/
              |--- controllers/
                      |--- productController.js             -- **ตั้งชื่อไฟล์รูปแบบนี้**
                      |--- ...
              |--- routes/
                      |--- routes.js                        -- เอาไว้รวม Routes ทั้งหมดในโฟลเดอร์นี้ก่อน Export
                      |--- productRoutes.js                 -- **ตั้งชื่อไฟล์รูปแบบนี้**
                      |--- ...
              |--- middlewares/
                      |--- authMiddleware.js                -- **ตั้งชื่อไฟล์รูปแบบนี้**
                      |--- ...
|--- data/                                                  -- ข้อมูลสำหรับเติมใส่ Database ก่อนเฉย ๆ
|--- scripts/                                               -- แค่ใช้ Run เปล่า ๆ ไม่ Import ใช้ใน Express App
|--- tests/                                                 -- เอาไว้เขียน Test ถ้ามีเวลา 🥹
```
