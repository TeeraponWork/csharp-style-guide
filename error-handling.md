# ⚠️ Error Handling (Production Guide)

การจัดการข้อผิดพลาด (Error Handling) เป็นส่วนสำคัญที่ช่วยให้ระบบ **เสถียร (Stable), debug ง่าย (Observable), และปลอดภัย (Secure)**

---

## 📌 เป้าหมายของ Error Handling

- ป้องกันระบบล่ม (Crash)
- ให้ response ที่เหมาะสมกับ client
- เก็บ log สำหรับ debug
- ไม่เปิดเผยข้อมูลสำคัญ (Sensitive Data)

---

## 🧱 แนวคิดหลัก

| เรื่อง | แนวทาง |
|------|--------|
| Catch | จับเฉพาะที่จำเป็น |
| Log | ต้องมีเสมอ |
| User Message | ต้อง friendly |
| System Detail | เก็บใน log เท่านั้น |

---

## 1️⃣ ใช้ try-catch อย่างเหมาะสม

```csharp
try
{
    var result = await _service.ProcessAsync();
}
catch (BusinessException ex)
{
    return BadRequest(ex.Message);
}
catch (Exception ex)
{
    _logger.LogError(ex, "Unexpected error");
    return StatusCode(500, "Internal Server Error");
}
---
## 2️⃣ หลีกเลี่ยงการจับ Exception กว้างเกินไป
catch (Exception)
{
    // ❌ swallow error
}
---
## 3️⃣ Logging
_logger.LogError(ex, "Error while processing OrderId: {OrderId}", orderId);
---
## 4️⃣ Middleware
app.UseMiddleware<ExceptionMiddleware>();
---
## 5️⃣ ProblemDetails
return Problem(
    title: "Invalid Request",
    detail: "Email is required",
    statusCode: 400
);

💡 TL;DR
log ทุก error
user เห็น message ง่ายๆ
dev ดู detail จาก log
