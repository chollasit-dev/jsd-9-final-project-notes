# Project Structure

```txt
|--- .editorconfig
|--- .gitignore
|--- .prettierrc
|--- components.json
|--- eslint.config.js
|--- index.html
|--- jsconfig.json
|--- package-lock.json
|--- package.json
|--- vercel.json
|--- vite.config.js
|--- public/
      |--- images/
              |--- logos/
                      |--- favicon.{ico,png}
              |--- products/
                      |--- ...
|--- src/
      |--- Main.jsx
      |--- router.jsx
      |--- styles/
              |--- global.css                                 -- ของเว็บเรา
              |--- index.css                                  -- ของ shadcn/ui
      |--- pages/
              |--- Home/                                      -- ของแต่ละหน้า: components, hooks, etc.
                      |--- hooks/
                              |--- useSampleHook.jsx
                              |--- ...
                              |--- index.js
                      |--- components/
                              |--- Button.jsx                 -- ถ้าแค่ไฟล์เดียวพอ ไม่ต้องสร้าง Directory เพิ่ม
                              |--- ...
                              |--- Card/
                                      |--- Card.jsx
                                      |--- Card.module.css    -- สำหรับ Component นั้น ๆ ที่ Import ไปใช้
                                      |--- index.js
                              |--- .../
                              |--- index.js
              |--- Checkout/
              |--- Payment/
              |--- Login/
              |--- Register/
              |--- Dashboard/
                      |--- MyAccount/
                      |--- OrderHistory/
                      |--- MyWishlist/
      |--- components/
              |--- ui/                                        -- ของ shadcn/ui
              |--- layouts/
              |--- customs/
                      |--- Footer.jsx
                      |--- Header.jsx
                      |--- Sidebar.jsx
                      |--- ...
      |--- lib/
              |--- utils.ts                                   -- ของ shadcn/ui
              |--- data.js                                    -- Mock Data
```

- Style Solution: [shadcn/ui](https://ui.shadcn.com/)
- Icon Libraries:
  - [Lucide (มาพร้อมกับ shadcn/ui)](https://lucide.dev/)
  - [React Icons](https://react-icons.github.io/react-icons/)
