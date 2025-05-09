# Utility Classes/Functions

ปัจจุบันมี Class สำหรับใช้สร้าง

- Response `res.json(<ใส่ Object ที่จะส่งกลับตรงนี้>)`
- Error `next(<ใส่ Error ตรงนี้>)`

## Response

ResponseConstructor มีทั้งหมด 2 ค่าที่ต้องใส่ ตอน `new ResponseConstructor()`

- message: "ข้อความที่จะ Return กลับไป"
- data: ใส่อะไรก็ได้ครับ โดยปกติจะใส่ Object ที่จะส่งกลับไป `{ ... }`

```js
// บนสุดของไฟล์
import { ResponseConstructor } from '<Path ไปหา response.js>';

/** @type {import('express').RequestHandler} */
const fooController = (req, res) => {
  let data = {
    foo: 'ข้อมูลที่ 1 ใน Object',
    bar: 'ข้อมูลที่ 2 ใน Object',
  };

  return res.json(
    new ResponseConstructor('<ข้อความที่จะส่งกลับไปหา Client>', data),
  );
};
```

เป็นการสร้าง Object จากแม่พิมพ์ (Class) แทนที่จะเขียนมือโดยตรง จะได้เป็น Pattern
เดียวกัน

## Error

เวลามี Error ถ้าเป็นไปได้ ให้ส่งผ่าน `next(...)`

> [!IMPORTANT]
>
> อย่างลืมใส่ `next` ตรง Parameter ของ Controller Function ที่จะใช้ด้วย

```js
// บนสุดของไฟล์
import { BadRequestError } from '<Path ไปหา error.js>';

// กรณีสัก Function ด้านนอก เช่น mongoose มีการ Throw Error
const hasErrorController = async (req, res, next) => {
  try {
    await User.findOne();
  } catch (error) {
    next(
      new InternalServerError(
        'ข้อความแจ้ง Error ที่จะส่งกลับไปถ้าไม่ใช้ default ที่กำหนดใน error.js',
      ),
    );
  }
};

// กรณีเราตั้งใจส่ง Error เอง
const hasErrorController = (req, res, next) => {
  return next(
    new BadRequestError(
      'ข้อความแจ้ง Error ที่จะส่งกลับไปถ้าไม่ใช้ default ที่กำหนดใน error.js',
    ),
  );
};
```

ปัจจุบันมี Error ตาม Status Code อยู่ 2 อัน คือ **400** `BadRequestError` กับ
**500** `InternalServerError` ถ้ามีเพิ่มก็สร้างในไฟล์ `src/utils/error.js`
ตามความเหมาะสมได้เลย เช่น **409** `ConflictError`
