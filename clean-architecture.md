
# 🏗️ Clean Architecture

Clean Architecture คือสถาปัตยกรรมที่เน้นการแยกความรับผิดชอบ (Separation of Concerns) โดยแบ่งโค้ดออกเป็นเลเยอร์ต่างๆ ซึ่งมีกฎเหล็กคือ **"Dependency ต้องชี้เข้าหาจุดศูนย์กลางเสมอ"** (เลเยอร์ภายในห้ามรู้จักเลเยอร์ภายนอก)

---

## 🧭 โครงสร้างของเลเยอร์ (Layers)


### 1. Domain Layer (หัวใจของระบบ)
เป็นเลเยอร์ที่อยู่ลึกที่สุด เก็บกฎทางธุรกิจพื้นฐาน (Enterprise Business Rules)
* **ประกอบด้วย:** Entities, Value Objects, Enums, และ Interfaces พื้นฐาน
* **กฎ:** **ห้ามพึ่งพา (Reference) เลเยอร์อื่นโดยเด็ดขาด**
* **ตัวอย่าง:** `User.cs`, `IUserRepository.cs`, `OrderEntity.cs`

### 2. Application Layer (กฎของแอปพลิเคชัน)
เก็บ Logic การทำงานของ Use Case ต่างๆ (Application Business Rules)
* **ประกอบด้วย:** Interfaces สำหรับ Service, DTOs (Data Transfer Objects), Mappers, Commands/Queries และ Validators
* **กฎ:** พึ่งพาได้เฉพาะ **Domain Layer** เท่านั้น
* **ตัวอย่าง:** `ICreateOrderService.cs`, `UserDto.cs`, `OrderMappingProfile.cs`

### 3. Infrastructure Layer (ส่วนติดต่อภายนอก)
จัดการเรื่องการเก็บข้อมูลและเทคโนโลยีภายนอก
* **ประกอบด้วย:** Database Context (EF Core), Repository Implementations, Logging, Email Service, และการเรียก API ภายนอก
* **กฎ:** พึ่งพา **Application Layer** เพื่อ Implement ตาม Interface ที่กำหนดไว้
* **ตัวอย่าง:** `ApplicationDbContext.cs`, `UserRepository.cs`, `SmtpEmailService.cs`

### 4. Presentation Layer (จุดเชื่อมต่อผู้ใช้)
ส่วนที่รับ Request และส่ง Response กลับไปหาผู้ใช้
* **ประกอบด้วย:** Controllers, Middlewares, Web APIs, หรือ UI Components
* **กฎ:** พึ่งพา **Application Layer** (และ Infrastructure สำหรับการทำ Dependency Injection ในตอนเริ่มโปรแกรม)
* **ตัวอย่าง:** `UsersController.cs`, `ExceptionMiddleware.cs`, `Program.cs`

---

## 📁 โครงสร้างโฟลเดอร์มาตรฐาน (Folder Structure)

```text
src/
├── MyProject.Domain/
│   ├── Entities/
│   ├── Enums/
│   └── Interfaces/
├── MyProject.Application/
│   ├── Common/
│   ├── DTOs/
│   ├── Interfaces/
│   └── Services/
├── MyProject.Infrastructure/
│   ├── Data/ (EF Core)
│   ├── Repositories/
│   └── Services/ (External API, Email)
└── MyProject.WebAPI/
    ├── Controllers/
    ├── Middlewares/
    └── Program.cs
🔑 กฎการพึ่งพา (The Dependency Rule)
เพื่อให้ระบบยืดหยุ่น เราจะใช้ Dependency Injection (DI) ในการเชื่อมต่อแต่ละเลเยอร์:

Domain ไม่รู้จักใครเลย

Application รู้จักแค่ Domain

Infrastructure รู้จัก Application เพื่อทำงานให้บรรลุผล

Presentation รู้จัก Application เพื่อส่งคำสั่งต่อ

ข้อดี: หากคุณต้องการเปลี่ยนจากฐานข้อมูล SQL Server ไปเป็น MongoDB คุณจะแก้โค้ดแค่ในเลเยอร์ Infrastructure เท่านั้น โดยที่เลเยอร์ Domain และ Application ไม่ต้องแก้ไขอะไรเลย

💡 สรุปการทำงาน (Workflow)
Request เข้ามาที่ Presentation (Controller)

Presentation ส่งข้อมูล (DTO) ให้ Application (Service)

Application ใช้ Domain (Entity) ในการคำนวณตาม Logic

Application เรียกใช้ Infrastructure (Repository) ผ่าน Interface เพื่อบันทึกข้อมูล

Response ถูกส่งกลับผ่าน Presentation
