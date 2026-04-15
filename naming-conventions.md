# มาตรฐานการตั้งชื่อ (Naming Conventions)

## กฎทั่วไป
- **PascalCase:** ใช้กับ Class, Method, Property, Enum, Struct
- **camelCase:** ใช้กับ Local Variable, Method Parameter
- **_camelCase:** ใช้กับ Private Field (ต้องมี underscore)

## การใช้เอกพจน์ และ พหูพจน์
| ประเภท | รูปแบบ | ตัวอย่าง |
| :--- | :--- | :--- |
| Entity/Class | เอกพจน์ | `User`, `Order`, `Product` |
| Collection/List | พหูพจน์ | `users`, `orders`, `productList` |
| Method คืนค่า List | พหูพจน์ | `GetActiveUsers()`, `FetchOrders()` |
| Method คืนค่าเดี่ยว | เอกพจน์ | `GetUserById(int id)`, `GetLatestOrder()` |

> **Tip:** หากตัวแปรเป็น Boolean ให้ตั้งชื่อในลักษณะคำถามหรือสถานะ เช่น `isActive`, `hasPermission`
