
# 🧱 SOLID Principles

SOLID คือหลักการออกแบบซอฟต์แวร์ 5 ข้อ ที่ช่วยให้โค้ดอ่านง่าย ยืดหยุ่น แก้ไขง่าย และขยายระบบได้ดีในระยะยาว

---

## 📌 สรุปภาพรวม

| หลักการ | ชื่อเต็ม | แนวคิดหลัก | เป้าหมาย |
|--------|--------|-----------|----------|
| S | Single Responsibility | 1 class = 1 หน้าที่ | ลดผลกระทบเวลาแก้ |
| O | Open/Closed | เปิดให้ขยาย ปิดการแก้ไข | เพิ่ม feature โดยไม่แก้โค้ดเดิม |
| L | Liskov Substitution | ใช้ subclass แทน parent ได้ | ไม่ทำให้ระบบพัง |
| I | Interface Segregation | interface ต้องเล็ก | ไม่บังคับ implement เกินจำเป็น |
| D | Dependency Inversion | พึ่ง abstraction | ลด coupling |

---

## 1️⃣ SRP
แยก class ตามหน้าที่เดียว

## 2️⃣ OCP
เพิ่ม feature ได้โดยไม่แก้โค้ดเดิม

## 3️⃣ LSP
ลูกต้องแทนพ่อได้

## 4️⃣ ISP
interface ต้องเล็ก ใช้เท่าที่จำเป็น

## 5️⃣ DIP
พึ่ง abstraction ไม่พึ่ง implementation

---

## 💡 สรุป

- S → แยกหน้าที่  
- O → เพิ่มได้ ไม่แก้ของเดิม  
- L → ใช้แทนกันได้  
- I → เล็กและเฉพาะ  
- D → ใช้ interface  

