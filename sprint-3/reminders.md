# Note สรุปประชุม 2025-05-11 ตอน 3 ทุ่ม

## Reminder

- สรุปใช้เป็น Named Export นะครับ

```js
import { foo } from './foo.js';
import { foo as newImportName } from './foo.js';
import * as aliasName from './foo.js';

foo();
newImportName();
aliasName.foo();

export { foo };
export { foo as newExportName };
```

- Request และ Response แต่ละค่าเราใช้เป็น snake_case นะครับ

```js
res.json({
  user_id: 99999
  user_money: 9
})
```

- ส่วนตรง Param เราใช้เป็น camelCase นะครับ

```js
router.get('/user/:userId', (req, res) => {
  const id = req.params.userId;
  // ...
});
```

- ใช้ `ResponseConstructor` ใน `src/utils/response.js` กับ Error Classes ใน
  `src/utils/error.js` ด้วยนะครับ
- อย่าลืมไปตามเอา Comment โค้ดที่ไม่ใช้ออกนะครับ
- [x] ทำ Task นั้น ๆ เสร็จแล้ว

  - เปิด Pull Request รอผม Merge สักครู่
  - ถ้าผมมีอะไรให้แก้ไข ให้แก้ก่อน เสร็จแล้วก็ Push ขึ้นมาใหม่ รอ Merge
  - Merge สำเร็จแล้วให้ลบ Branch นั้นทิ้งเลยทั้ง Local
    `git branch -d <branch_name>` และบน GitHub
    `git push -d origin <branch_name>`
