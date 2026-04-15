# 🪵 มาตรฐานการบันทึก Log (Logging Standards)

การทำ Logging ที่ดีไม่ใช่แค่การพิมพ์ข้อความออกมา แต่คือการบันทึก "ร่องรอย" ที่ช่วยให้เราวิเคราะห์ปัญหาได้แม่นยำและรวดเร็ว โดยเฉพาะเมื่อระบบทำงานอยู่บน Server ที่เราไม่สามารถเข้าไป Debug ได้

---

## 1. การบันทึกแบบ Structured Logging (สำคัญที่สุด)

ใน C# เราจะไม่ใช้การต่อสตริง (String Interpolation) ใน Log แต่จะใช้ **Message Templates** เพื่อให้ระบบเก็บ Log (เช่น Seq, Elasticsearch) สามารถค้นหาข้อมูลตาม Property ได้

* **❌ ไม่แนะนำ (Search ยาก):**
  `_logger.LogInformation($"User {userId} bought product {productId}");`
* **✅ ถูกต้อง (Structured):**
  `_logger.LogInformation("User {UserId} bought product {ProductId}", userId, productId);`

> **เหตุผล:** ระบบเก็บ Log จะแยก `UserId` และ `ProductId` เป็นฟิลด์ข้อมูลให้เรากรอง (Filter) ได้ทันที

---

## 2. ลำดับความสำคัญของ Log (Log Levels)

เลือกใช้ Level ให้เหมาะสมเพื่อให้เราสามารถตั้งค่าการแจ้งเตือน (Alert) ได้ถูกต้อง

| Level | การใช้งาน | สถานการณ์ตัวอย่าง |
| :--- | :--- | :--- |
| **Trace** | รายละเอียดลึกที่สุด | ดูขั้นตอนการทำงานภายใน Logic ที่ซับซ้อน |
| **Debug** | ข้อมูลสำหรับการพัฒนา | พิมพ์ค่าตัวแปรระหว่าง Develop |
| **Information** | เหตุการณ์ปกติที่สำคัญ | "User logged in", "Order #123 created" |
| **Warning** | สิ่งผิดปกติที่ยังทำงานต่อได้ | "Database connection retry 1/3", "Slow response" |
| **Error** | ข้อผิดพลาดใน Request นั้นๆ | "Cannot upload file", "Validation failed" |
| **Critical** | ระบบล่ม หรือทำงานต่อไม่ได้ | "Database connection failed", "Out of memory" |

---

## 3. การบันทึก Exception

เมื่อเกิด Error ห้ามบันทึกแค่ `ex.Message` เพราะเราจะเสียข้อมูล Stack Trace ที่บอกว่าบรรทัดไหนพัง

* **❌ ไม่แนะนำ:**
  `_logger.LogError(ex.Message);`
* **✅ ถูกต้อง:**
  `_logger.LogError(ex, "เกิดข้อผิดพลาดขณะประมวลผลคำสั่งซื้อ {OrderId}", orderId);`

---

## 4. ข้อควรระวังและกฎเหล็ก (Do's & Don'ts)

### ✅ สิ่งที่ควรทำ (Do)
- **Contextual Info:** ใส่ข้อมูลที่ช่วยระบุตัวตนของรายการนั้นๆ เสมอ เช่น `OrderId`, `UserId`, `CorrelationId`
- **Meaningful Messages:** เขียนข้อความให้อ่านแล้วเข้าใจทันทีว่าเกิดอะไรขึ้นที่ไหน
- **Asynchronous:** ใช้การบันทึก Log แบบ Non-blocking (ซึ่ง Library มาตรฐานของ .NET ทำให้อยู่แล้ว)

### ❌ สิ่งที่ไม่ควรทำ (Don't)
- **PII Data:** ห้ามบันทึกข้อมูลส่วนบุคคลที่ละเอียดอ่อน เช่น **รหัสผ่าน (Passwords), เลขบัตรเครดิต, หรือข้อมูลสุขภาพ** ลงใน Log เด็ดขาด
- **Logging in Loops:** หลีกเลี่ยงการใส่ Log ระดับ Information ใน Loop ที่ทำงานหนักๆ เพราะจะทำให้ไฟล์ Log บวมและระบบช้าลง
- **Generic Messages:** อย่าใส่ข้อความกว้างๆ เช่น "Error occurred" หรือ "Success" โดยไม่มีข้อมูลประกอบ

---

## 5. ตัวอย่างการใช้งานใน Code

public class PaymentService
{
    private readonly ILogger<PaymentService> _logger;

    public PaymentService(ILogger<PaymentService> logger)
    {
        _logger = logger;
    }

    public void ProcessPayment(int userId, decimal amount)
    {
        // เริ่มต้นการทำงาน
        _logger.LogInformation("Processing payment for User: {UserId}, Amount: {Amount}", userId, amount);

        try 
        {
            // Payment Logic...
        }
        catch (Exception ex)
        {
            // บันทึก Error พร้อมวัตถุ Exception
            _logger.LogError(ex, "Payment failed for User: {UserId}", userId);
            throw;
        }
    }
}
