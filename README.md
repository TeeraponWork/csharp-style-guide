# 📘 C# Professional Coding Standard (GitBook)

ยินดีต้อนรับเข้าสู่โปรเจ็กต์ **C# Style Guide** แหล่งรวมมาตรฐานการเขียนโค้ด (Best Practices) ที่ออกแบบมาเพื่อสร้างระเบียบวินัยในการพัฒนาซอฟต์แวร์ด้วยภาษา C# ให้มีความเป็นเอกภาพ อ่านง่าย และพร้อมสำหรับระบบงานระดับ Enterprise

> **"Code is read much more often than it is written."** — เป้าหมายของเราคือการทำให้โค้ดอ่านง่ายเสมือนอ่านบทความภาษาอังกฤษ

## 🎯 วัตถุประสงค์
1.  **Uniformity:** เพื่อให้โค้ดทั้งโปรเจ็กต์มีหน้าตาเหมือนกัน ไม่ว่าจะเขียนโดยคนหรือ AI
2.  **AI Compatibility:** ใช้เป็น Reference สำหรับ AI Assistant (เช่น ChatGPT, Claude, Gemini) เพื่อลดข้อผิดพลาดในการ Generate โค้ด
3.  **Maintainability:** ลดหนี้ทางเทคนิค (Technical Debt) ด้วยโครงสร้าง Clean Architecture และ SOLID Principles

## 🤖 วิธีใช้งานร่วมกับ AI (The Secret Sauce) 🚀

เพื่อให้คุณได้โค้ดที่มีคุณภาพสูงสุดและตรงตามมาตรฐานนี้ ให้คัดลอกข้อความด้านล่างนี้ไปสั่ง AI เมื่อเริ่มโปรเจ็กต์ใหม่:

> **Prompt:** "กรุณาทำหน้าที่เป็น C# Expert และเขียนโค้ดโดยอ้างอิงมาตรฐานจาก Style Guide ของฉันที่นี่: https://teeraponwork.github.io/csharp-style-guide/logging-standards.html
> โดยเน้นย้ำเรื่อง:
> 1. การตั้งชื่อ Private Field ต้องมี `_` นำหน้า
> 2. Method ที่เป็น Async ต้องลงท้ายด้วย `Async`
> 3. ใช้ Dependency Injection แทนการ `new` object ใน Service"

## 🤝 การปรับปรุงเนื้อหา (Contribution)

หากคุณมีแนวทางปฏิบัติ (Best Practices) อื่นๆ ที่น่าสนใจ เช่น **Unit Testing** หรือ **Performance Tuning** สามารถเปิด **Pull Request** หรือสร้าง **Issue** เพื่อร่วมพัฒนากูรูเล่มนี้ให้สมบูรณ์ยิ่งขึ้นครับ

---
**Maintained by:** Teerapon Boonthong 
**Collaborator:** คู่หูเขียนโค้ด (Gemini AI)
