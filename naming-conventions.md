# 🏷️ มาตรฐานการตั้งชื่อ (Naming Conventions)

การตั้งชื่อที่สื่อความหมายและเป็นระบบช่วยให้โค้ด "เล่าเรื่องด้วยตัวเองได้" (Self-documenting code) ลดเวลาในการอ่านคอมเมนต์ และทำให้การบำรุงรักษาโค้ดทำได้รวดเร็วขึ้น

---

## 1. กฎการจัดรูปแบบตัวอักษร (Casing)

เรายึดตามมาตรฐานสากลของ .NET เพื่อความเป็นเอกภาพทั่วทั้งโปรเจ็กต์

| รูปแบบ | การใช้งาน | ตัวอย่าง |
| :--- | :--- | :--- |
| **PascalCase** | Class, Interface, Method, Property, Enum, Struct | `UserProvider`, `CalculateTotal()` |
| **camelCase** | Local Variable, Method Parameter | `totalAmount`, `userId` |
| **_camelCase** | Private Field (ตัวแปรภายใน Class) | `_userRepository`, `_logger` |

---

## 2. หลักการใช้เอกพจน์ และ พหูพจน์ (Singular vs Plural)

การระบุจำนวนผ่านชื่อตัวแปรช่วยให้เราทราบถึง "ขนาดข้อมูล" ได้ทันทีโดยไม่ต้องดู Declaration

### 🟢 เอกพจน์ (Singular)
ใช้กับวัตถุที่มีชิ้นเดียว หรือเป็นตัวแทนของประเภทข้อมูลนั้นๆ
* **Class Name:** ใช้คำนามเอกพจน์เสมอ เช่น `User`, `Order`, `Product`
* **Method (Return ค่าเดียว):** `GetUserById(int id)`, `GetLatestOrder()`
* **Variable:** `var currentUser = new User();`

### 🔵 พหูพจน์ (Plural)
ใช้กับตัวแปรกลุ่มข้อมูล (Collection, List, Array, IEnumerable)
* **Collections:** ใช้คำนามพหูพจน์ เช่น `users`, `activeOrders`, `roles`
* **Method (Return หลายค่า):** `GetActiveUsers()`, `FetchRecentOrders()`
* **Naming Tip:** หากต้องการเน้นว่าเป็นรายการสรุป สามารถใช้คำขยายได้ เช่น `orderList` หรือ `productSelection` แต่โดยทั่วไปการเติม **"s"** ท้ายคำนามจะเรียบง่ายที่สุด

---

## 3. มาตรฐานเฉพาะทางสำหรับ C#

### 🧩 Interfaces
ต้องขึ้นต้นด้วยตัว **I** ใหญ่เสมอ เพื่อแยกแยะระหว่าง "ความสามารถ" (Interface) กับ "สิ่งที่ทำได้จริง" (Concrete Class)
* **✅ ตัวอย่าง:** `IUserRepository`, `IFileService`, `IDisposable`

### ⚡ Asynchronous Methods
Method ที่ทำงานเบื้องหลัง (Async) **ต้อง** ลงท้ายด้วยคำว่า **Async** เพื่อสื่อสารให้ผู้เรียกใช้ทราบว่าต้องมีการ `await`
* **✅ ตัวอย่าง:** `Task SaveDataAsync()`, `Task<User> FindUserAsync(int id)`

### 🚩 Boolean (ตัวแปรตรรกะ)
ควรตั้งชื่อในลักษณะ **"คำถาม"** หรือ **"การบอกสถานะ"** เพื่อให้อ่านใน `if` statement ได้ลื่นไหล
* **Prefixes ที่แนะนำ:** `is`, `has`, `can`, `should`
* **ตัวอย่าง:** `isActive`, `hasPermission`, `canDelete`, `shouldRetry`

### 🔢 Enums
* **ชื่อ Enum:** เป็นเอกพจน์เสมอ เช่น `OrderStatus`
* **สมาชิกภายใน:** ใช้ PascalCase เช่น `Pending`, `Shipped`, `Cancelled`

---

## 4. ข้อควรระวัง (Bad Practices)

* **❌ อย่าใช้ตัวย่อที่เข้าใจยาก:** เช่น `usr` (ควรเป็น `user`), `qty` (ควรเป็น `quantity`)
* **❌ ไม่ต้องระบุประเภทข้อมูลในชื่อ:** เช่น `userList`, `idString` (เพราะ IDE บอกเราอยู่แล้ว ให้ใช้ `users`, `id` แทน)
* **❌ หลีกเลี่ยงคำคลุมเครือ:** เช่นคำว่า `Data`, `Info`, `Manager` หากเป็นไปได้ให้เปลี่ยนเป็นคำที่เจาะจงกว่า เช่น `AccountDetails`, `FileProcessor`
* **❌ อย่าใช้ภาษาอื่นนอกจากอังกฤษ:** เพื่อให้โค้ดเป็นมาตรฐานสากลและทำงานร่วมกับ Tool ต่างๆ ได้ดีที่สุด

---

## 5. Generic Types
ใช้ตัวอักษร **T** นำหน้าเสมอเพื่อบ่งบอกว่าเป็น Type Parameter
* **ตัวเดียว:** `List<T>`
* **หลายตัว:** `IRepository<TEntity, TKey>`
