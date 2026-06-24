# 🧱 SOLID Principles (หลักการออกแบบซอฟต์แวร์)

SOLID คือหลักการออกแบบซอฟต์แวร์ 5 ข้อ ที่ช่วยให้โค้ดอ่านง่าย ยืดหยุ่น แก้ไขง่าย และขยายระบบได้ดีในระยะยาว การยึดถือหลักการนี้จะช่วยลดความซับซ้อนเมื่อโปรเจ็กต์มีขนาดใหญ่ขึ้น

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

## 1️⃣ Single Responsibility Principle (SRP)
**"1 Class ควรมีหน้าที่เพียงอย่างเดียวและมีเหตุผลเดียวในการเปลี่ยนแปลง"**

หากคลาสหนึ่งต้องรับผิดชอบหลายอย่าง เมื่อมีการแก้ไขลอจิกส่วนใดส่วนหนึ่ง อาจส่งผลกระทบต่อการทำงานส่วนอื่นได้ง่าย

**❌ ไม่แนะนำ:** คลาสทำงานหลายอย่างพร้อมกัน เช่น จัดการเอกสาร PDF และส่งอีเมลแจ้งเตือน
```csharp
public class DocumentProcessor
{
    public void ProtectPdf(string filePath, string password)
    {
        // ลอจิกการเพิ่มความปลอดภัยให้ PDF
    }

    public void SendEmailNotification(string email)
    {
        // ลอจิกการส่งอีเมล
    }
}

✅ แนะนำ: แยก class ตามหน้าที่เดียว  

public class PorschePdfProtector
{
    public void ApplySecurity(string filePath, string password)
    {
        // ลอจิกการเพิ่มความปลอดภัยให้ PDF โดยเฉพาะ
    }
}

public class EmailNotifier
{
    public void Send(string email, string message)
    {
        // ลอจิกการส่งอีเมล
    }
}

2️⃣ Open/Closed Principle (OCP)"เปิดรับการขยายความสามารถ แต่ปิดการแก้ไขโค้ดเดิม"  เราควรเพิ่ม feature ได้โดยไม่แก้โค้ดเดิมที่เคยเขียนและทดสอบผ่านไปแล้ว  ❌ ไม่แนะนำ: ต้องเข้าไปแก้โค้ดเดิม (เพิ่ม else if) ทุกครั้งที่มีการประมวลผลเอกสารประเภทใหม่

public class DocumentAutomator
{
    public void Process(string docType)
    {
        if (docType == "PDF") { /* ลอจิกจัดการ PDF */ }
        else if (docType == "Word") { /* ลอจิกจัดการ Word */ }
    }
}

✅ แนะนำ: ใช้ Interface เพื่อเปิดรับการขยายการทำงาน
public interface IDocumentProcessor
{
    void Process();
}

public class PdfProcessor : IDocumentProcessor { /* ลอจิกจัดการ PDF */ }
public class WordProcessor : IDocumentProcessor { /* ลอจิกจัดการ Word */ }

public class DocumentAutomator
{
    public void Execute(IDocumentProcessor processor)
    {
        processor.Process();
    }
}
3️⃣ Liskov Substitution Principle (LSP)"ลูกต้องแทนพ่อได้"  หากมีการสืบทอด (Inheritance) คลาสลูกต้องไม่ยกเลิกหรือเปลี่ยนแปลงพฤติกรรมหลักที่คลาสแม่ได้กำหนดไว้❌ ไม่แนะนำ: คลาสลูก Throw Exception ใน Method ที่สืบทอดมา
public class Document
{
    public virtual void Edit() { /* ลอจิกการแก้ไข */ }
}

public class ReadOnlyDocument : Document
{
    public override void Edit()
    {
        throw new NotSupportedException("เอกสารนี้อ่านได้อย่างเดียว ไม่สามารถแก้ไขได้");
    }
}
public class Document
{
    public virtual void Edit() { /* ลอจิกการแก้ไข */ }
}

public class ReadOnlyDocument : Document
{
    public override void Edit()
    {
        throw new NotSupportedException("เอกสารนี้อ่านได้อย่างเดียว ไม่สามารถแก้ไขได้");
    }
}
✅ แนะนำ: แยก Interface ตามความสามารถที่ทำได้จริง

public interface IReadable { void Read(); }
public interface IEditable { void Edit(); }

public class StandardDocument : IReadable, IEditable { /* ... */ }
public class ReadOnlyDocument : IReadable { /* ... */ }

4️⃣ Interface Segregation Principle (ISP)"interface ต้องเล็ก ใช้เท่าที่จำเป็น"  การมี Interface ขนาดใหญ่ (Fat Interface) ทำให้คลาสที่นำไปใช้ต้องเขียนโค้ดเปล่าๆ หรือทิ้ง Exception ไว้ใน Method ที่ไม่ต้องการ❌ ไม่แนะนำ: Interface ที่รวมทุกอย่างไว้ด้วยกัน

public interface IAutomatedDocument
{
    void Read();
    void ApplyWatermark();
    void Encrypt();
}

✅ แนะนำ: แตก Interface ให้เล็กและเฉพาะเจาะจง

public interface IFileReader { void Read(); }
public interface IWatermarker { void ApplyWatermark(); }
public interface IDocumentSecurity { void Encrypt(); }

5️⃣ Dependency Inversion Principle (DIP)
"พึ่ง abstraction ไม่พึ่ง implementation"[cite: 8]

หลีกเลี่ยงการสร้าง Object ข้ามเลเยอร์ด้วยตนเอง เพื่อลดการผูกมัด (Tight Coupling)

❌ ไม่แนะนำ: new อ็อบเจ็กต์ของคลาสอื่นโดยตรง

public class LexusDocumentPipeline
{
    private readonly PorschePdfProtector _pdfProtector;

    public LexusDocumentPipeline()
    {
        // ผิดหลัก DIP เพราะผูกติดกับ Implementation โดยตรง
        _pdfProtector = new PorschePdfProtector(); 
    }
}
✅ แนะนำ: ใช้ interface และฉีด Dependency ผ่าน Constructor (Dependency Injection)[cite: 8]

public interface IPdfSecurityProvider
{
    void ApplySecurity(string filePath);
}

public class LexusDocumentPipeline
{
    private readonly IPdfSecurityProvider _securityProvider;

    // ระบบ DI จะจัดการส่ง instance ที่ถูกต้องเข้ามาให้เอง
    public LexusDocumentPipeline(IPdfSecurityProvider securityProvider)
    {
        _securityProvider = securityProvider;
    }

    public void RunPipeline(string filePath)
    {
        _securityProvider.ApplySecurity(filePath);
    }
}
💡 สรุป
S → แยกหน้าที่[cite: 8]

O → เพิ่มได้ ไม่แก้ของเดิม[cite: 8]

L → ใช้แทนกันได้[cite: 8]

I → เล็กและเฉพาะ[cite: 8]

D → ใช้ interface[cite: 8]
