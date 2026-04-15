# 🧩 Object-Oriented Programming (OOP)

การโปรแกรมเชิงวัตถุ (OOP) คือหัวใจหลักของการพัฒนาซอฟต์แวร์ด้วย C# ซึ่งเป็นการออกแบบโดยจำลองวัตถุจากโลกแห่งความเป็นจริง (Objects) มาอยู่ในรูปแบบของโค้ด เพื่อให้ระบบจัดการง่าย มีความปลอดภัย และนำกลับมาใช้ซ้ำได้จริง

---

## 🏗️ เสาหลัก 4 ประการของ OOP

| หลักการ | แนวคิดหลัก | ใช้เมื่อไหร่ | ประโยชน์ |
|--------|-----------|-------------|----------|
| Encapsulation | ซ่อนข้อมูลและควบคุมการเข้าถึง | ต้องการป้องกันข้อมูลถูกแก้ผิด | ปลอดภัย / ควบคุมได้ |
| Abstraction | ซ่อนรายละเอียด เหลือแค่สิ่งที่ใช้ | ต้องการลดความซับซ้อน | ใช้งานง่าย / ลด coupling |
| Inheritance | สืบทอดคุณสมบัติจาก class เดิม | มี object ที่คล้ายกัน | ลด code ซ้ำ |
| Polymorphism | พฤติกรรมเดียวกัน แต่ทำงานต่างกัน | รองรับหลาย type | ยืดหยุ่น / ขยายง่าย |

---

### 1. การห่อหุ้มข้อมูล (Encapsulation)

คือการรวบรวมข้อมูล (Fields) และพฤติกรรม (Methods) ไว้ภายใน Class และจำกัดการเข้าถึงจากภายนอก เพื่อปกป้องสถานะของวัตถุไม่ให้ถูกแก้ไขอย่างไม่ถูกต้อง

- **แนวทางปฏิบัติ:** ใช้ Access Modifiers เช่น `private` เพื่อซ่อนข้อมูล และเปิดให้เข้าถึงผ่าน **Properties** เท่านั้น  
- **ประโยชน์:** ช่วยให้เราสามารถเพิ่มเงื่อนไขการตรวจสอบ (Validation) ก่อนที่ข้อมูลจะถูกเปลี่ยนแปลงได้  

```csharp
public class BankAccount
{
    private decimal _balance; 
    public decimal Balance => _balance; 

    public void Deposit(decimal amount)
    {
        if (amount > 0) 
        {
            _balance += amount;
        }
    }
}
```

---

### 2. การซ่อนรายละเอียด (Abstraction)

- ใช้ `interface` หรือ `abstract class`  
- ลดความซับซ้อนของระบบ  

```csharp
public interface IMessageService
{
    void Send(string message); 
}
```

---

### 3. การสืบทอด (Inheritance)

- ใช้ความสัมพันธ์แบบ Is-A  
- ลดการเขียนซ้ำ  

```csharp
public class Vehicle
{
    public string Brand { get; set; }
}

public class Car : Vehicle 
{
    public int NumberOfDoors { get; set; }
}
```

---

### 4. การพหุสัณฐาน (Polymorphism)

- ใช้ `virtual` / `override`  
- รองรับหลาย type  

```csharp
public abstract class Shape
{
    public abstract void Draw();
}

public class Circle : Shape
{
    public override void Draw() => Console.WriteLine("Circle");
}

public class Square : Shape
{
    public override void Draw() => Console.WriteLine("Square");
}
```

---

## 💡 สรุป

- Encapsulation → ควบคุมข้อมูล  
- Abstraction → ลดความซับซ้อน  
- Inheritance → ใช้ซ้ำ  
- Polymorphism → ยืดหยุ่น  
