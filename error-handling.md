# การจัดการ Error (Global Exception Handling)

## หลักการสำคัญ
1. **Don't Overuse Try-Catch:** หลีกเลี่ยงการเขียน try-catch ครอบทุกจุด ให้ปล่อย Exception ไหลไปยัง Middleware
2. **Global Middleware:** ใช้ Middleware กลางในการดักจับ Exception และแปลงเป็น Problem Details (RFC 7807)
3. **Custom Exceptions:** สร้าง Exception เฉพาะทางสำหรับ Business Logic เช่น `DomainException`

## รูปแบบการส่ง Response เมื่อเกิด Error
```json
{
  "type": "[https://tools.ietf.org/html/rfc7231#section-6.5.4](https://tools.ietf.org/html/rfc7231#section-6.5.4)",
  "title": "Not Found",
  "status": 404,
  "detail": "User with ID 123 was not found."
}
