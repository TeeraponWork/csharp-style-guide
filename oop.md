# 🧩 Object-Oriented Programming (OOP)

การโปรแกรมเชิงวัตถุ (OOP) คือหัวใจหลักของการพัฒนาซอฟต์แวร์ด้วย C# ซึ่งเป็นการออกแบบโดยจำลองวัตถุจากโลกแห่งความเป็นจริง (Objects) มาอยู่ในรูปแบบของโค้ด เพื่อให้ระบบจัดการง่าย มีความปลอดภัย และนำกลับมาใช้ซ้ำได้จริง

## 🏗️ เสาหลัก 4 ประการของ OOP

### 1. การห่อหุ้มข้อมูล (Encapsulation)
คือการรวบรวมข้อมูล (Fields) และพฤติกรรม (Methods) ไว้ภายใน Class และจำกัดการเข้าถึงจากภายนอก เพื่อปกป้องสถานะของวัตถุไม่ให้ถูกแก้ไขอย่างไม่ถูกต้อง

* **แนวทางปฏิบัติ:** ใช้ Access Modifiers เช่น `private` เพื่อซ่อนข้อมูล และเปิดให้เข้าถึงผ่าน **Properties** เท่านั้น
* **ประโยชน์:** ช่วยให้เราสามารถเพิ่มเงื่อนไขการตรวจสอบ (Validation) ก่อนที่ข้อมูลจะถูกเปลี่ยนแปลงได้

public class BankAccount
{
    // ซ่อนยอดเงินไว้เป็นส่วนตัว (Private Field)
    private decimal _balance; 

    // เปิดให้ภายนอกอ่านยอดเงินได้เท่านั้น (Read-only Property)
    public decimal Balance => _balance; 

    public void Deposit(decimal amount)
    {
        // มีการตรวจสอบเงื่อนไขก่อนแก้ไขข้อมูลภายใน (Encapsulation)
        if (amount > 0) 
        {
            _balance += amount;
        }
    }
}

2. การซ่อนรายละเอียด (Abstraction)
คือการนำเสนอเฉพาะ "สิ่งที่วัตถุทำได้" (Interface) โดยซ่อน "วิธีการทำงานที่ซับซ้อนไว้ภายใน" เพื่อให้ผู้ที่นำไปใช้งานโฟกัสแค่การสั่งงานโดยไม่ต้องรู้รายละเอียดเชิงลึก

แนวทางปฏิบัติ: ใช้ interface หรือ abstract class

ประโยชน์: ลดความซับซ้อนในการเชื่อมต่อระหว่างส่วนต่างๆ ของโปรแกรม (Decoupling)

public interface IMessageService
{
    // ผู้ใช้รู้แค่ว่าสั่งส่งข้อความได้ แต่ไม่ต้องรู้ว่าระบบส่งผ่าน Email หรือ SMS
    void Send(string message); 
}

3. การสืบทอด (Inheritance)
คือการสร้าง Class ใหม่โดยนำคุณสมบัติจาก Class เดิมที่มีอยู่แล้วมาใช้งานต่อ เพื่อลดการเขียนโค้ดซ้ำซ้อนและสร้างโครงสร้างข้อมูลที่ชัดเจน

แนวทางปฏิบัติ: ใช้ความสัมพันธ์แบบ "Is-A" (เป็นหนึ่งใน...) เช่น Car Is-A Vehicle
ประโยชน์: จัดการโค้ดส่วนกลางไว้ที่เดียว (Base Class) ทำให้ง่ายต่อการแก้ไขในอนาคต

public class Vehicle
{
    public string Brand { get; set; }
    public void StartEngine() => Console.WriteLine("Engine started.");
}

// Car สืบทอดความสามารถทั้งหมดจาก Vehicle และเพิ่มคุณสมบัติเฉพาะของตัวเอง
public class Car : Vehicle 
{
    public int NumberOfDoors { get; set; }
}

4. การพหุสัณฐาน (Polymorphism)
คือความสามารถของวัตถุที่มีโครงสร้างพื้นฐานเดียวกัน แต่สามารถแสดงพฤติกรรมออกมาต่างกันได้ตามประเภทของมันเอง

แนวทางปฏิบัติ: การทำ Method Overriding (ใช้คำสำคัญ virtual และ override)

ประโยชน์: ช่วยให้เราเขียนโค้ดที่รองรับวัตถุหลายประเภทได้โดยใช้ชื่อคำสั่งเดียวกัน

public abstract class Shape
{
    public abstract void Draw();
}

public class Circle : Shape
{
    public override void Draw() => Console.WriteLine("Drawing a Circle ⭕");
}

public class Square : Shape
{
    public override void Draw() => Console.WriteLine("Drawing a Square ⬜");
}

// การใช้งาน: แม้จะเป็น Shape เหมือนกัน แต่พฤติกรรมจะต่างกันตามประเภทจริง
List<Shape> shapes = new List<Shape> { new Circle(), new Square() };
foreach (var shape in shapes) 
{ 
    shape.Draw(); 
}
💡 สรุปหลักการสำหรับทีม
Encapsulation: เน้นความปลอดภัยและการควบคุมข้อมูล

Abstraction: เน้นความง่ายในการนำไปใช้งาน (ลดความซับซ้อน)

Inheritance: เน้นการใช้ซ้ำและการจัดกลุ่มข้อมูล

Polymorphism: เน้นความยืดหยุ่นและการขยายระบบในอนาคต
