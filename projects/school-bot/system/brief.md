---
project: school-bot
updated: 2026-11-03
---

# Brief: ปรับทั้งระบบ School Bot Studio (รอบความสมบูรณ์ + consistency)

## Goal (ผู้ใช้ 2026-11-03 · Confirmed)
หน้าตาทั้งระบบมีครบแล้วแต่ยังไม่สมบูรณ์และไม่ consistent · phase นี้ต้องการ **ความสมบูรณ์แบบ** และ **ความ consistency ทั้งระบบ** · ขอบเขตแก้ได้ตั้งแต่ Site Map, ของกลางที่เชื่อมทุกหน้า (เช่น nav bar, focus) ไปจนถึงรายละเอียดเล็กในหน้า · auditor ต้องเสนอจุดที่ควรปรับเพิ่มนอกจาก comment ของผู้ใช้ด้วย

## เกณฑ์ "สมบูรณ์" (ผู้ใช้เลือก 2026-11-03)
1. ไม่มี req ให้แก้เพิ่มจากผู้ใช้แล้ว (ทุก comment ปิดครบ)
2. Quiz: มีรูปภาพ ชื่อด่าน เนื้อหาด้านใน และ content ครบทั้ง 6 level
3. ฟังก์ชันพื้นฐานที่โปรแกรมประเภทนี้ควรมีครบ และใช้งานได้จริง
4. State ครบทุกหน้า (empty / loading / error / offline / หุ่นหลุด ตามที่เกี่ยวข้อง)
5. Flow ไม่ขาด: ทุกปุ่ม/ลิงก์ไปหน้าที่มีจริง ไม่มีทางตัน
6. Keyboard / focus / a11y: focus แบบเดียวกันทั้งระบบ ผ่าน WCAG AA
7. Copy / ชื่อเรียก: ชื่อหน้า ปุ่ม คำศัพท์เหมือนกันทั้งระบบ ตาม voice ใน brand.md

## ความหมายของแต่ละหน้า (ผู้ใช้ 2026-11-03)

| หน้า | คืออะไร | ใครเห็น | เข้าจาก / แสดงเมื่อ | module |
|---|---|---|---|---|
| Home | หน้าแรกหลัง login (SCR-05) | นักเรียน + ครู | หลัง login | app-shell |
| File | หน้าเดียวกับ my-work / งานของฉัน (SCR-09) | นักเรียน + ครู | จาก Home | my-work |
| Quiz Map | แผนที่เลือกด่าน | นักเรียน + ครู | หลังเลือก level | quiz |
| Workspace | ตัวแก้ไขของ Arm Lab / Block Lab | นักเรียน + ครู | เปิดงานจาก my-work, กดงานใหม่ หรือจาก Home | arm-lab, block-lab |
| Connected Page | หน้าเชื่อมต่อหุ่น (เลือกพอร์ต/อุปกรณ์ + สถานะ) | นักเรียน + ครู | ก่อนเข้า Workspace ทุกครั้ง · หุ่นหลุด → popup เปลี่ยนหุ่น | app-shell |

ครูใช้แอปเดียวกับนักเรียน หน้าตาเหมือนกัน (ผู้ใช้ 2026-11-03)

```
Login → Home → File (my-work) ─┐
           └→ งานใหม่ ──────────┼→ Connected Page → Workspace (Arm Lab / Block Lab)
                                    ↑ หุ่นหลุด → popup เปลี่ยนหุ่น
Home → Quiz → เลือก level → Quiz Map → (ด่าน → ? ให้ auditor ดูจาก canvas แล้วเสนอ)
```

## ข้อขัดกับเอกสารเดิม (ต้องแก้ตามกฎการเปลี่ยน requirement ใน Phase spec)
- **ครูในแอป:** context.md DEC-14 ระบุว่าแอปเป็นของนักเรียน ยกเว้นโหมดครูใน Arm Lab · คำตอบใหม่: ครูเห็นทุกหน้า หน้าตาเหมือนกัน
- **Connected Page:** frame ConnectV3 (FRM-06) ลงไว้ที่ arm-lab · คำตอบใหม่: เป็นของ app-shell ใช้ร่วม Arm Lab และ Block Lab
- **ชื่อ File vs งานของฉัน:** หน้าเดียวกันแต่เรียกต่างกัน

## Canvas ที่ใช้

| canvas | ลิงก์ | หน้า | ลงทะเบียนแล้วที่ |
|---|---|---|---|
| Canvas A (ใช้ร่วม) | https://claude.ai/artifact/AnEWv6UNbgcNvUXS1sfHQd | Home, File, Quiz, Quiz Map, Arm Lab, Connected | arm-lab C1, quiz C1, app-shell C1, my-work C1 (2026-11-03) |
| Block Lab | https://claude.ai/artifact/YYgSHL2aCtVbkDTgBQBzTV | Block Lab Workspace | block-lab C1 |

## ขั้นแรก: CI กลาง (ผู้ใช้ 2026-11-03 · ทำก่อน comment)
- **ปัญหา:** ไม่มีแหล่ง component เดียว · 2 canvas ต่างคนต่างมี component ของตัวเอง (เช่น WindowBarV1 vs WindowBarA2 และ WindowBar สำเนาอีก 3 ไฟล์ใน Block Lab) แก้ที่หนึ่งอีกที่ไม่ตาม
- **ทางแก้ที่เลือก:** สร้าง **Design System artifact แยก** (type "Design System") เป็นแหล่งกลางของ tokens + component + asset ของทั้ง 2 canvas · `brand.md` §1–11 ยังเป็นกฎ · ข้อจำกัด: canvas ไม่ update เอง แก้ DS แล้วต้อง sync เข้าทั้ง 2 canvas
- **สถานะ 2026-11-03:** สแกนเสร็จ (`system/ci-audit.md`) · ผู้ใช้ตัดสินครบ · brand.md §11 แก้แล้ว · สร้าง DS artifact แล้ว https://claude.ai/artifact/DgwzCEnxThrSoxnE5ZrNoy (ยังว่าง → crayon เติม)
- **ลำดับ:** auditor สแกน component ทั้ง 2 canvas เทียบ `brand.md` §11 ก่อน → `system/ci-audit.md` → ผู้ใช้ตัดสินแบบที่ขัดกัน → session หลักสร้าง DS artifact → เติม component → sync เข้า canvas

## งานที่รวมเข้ารอบนี้
- Block Lab: เชื่อม R21 context menu เข้า Main-A2 / BlocksPaneA2 (งานค้าง) ทำหลังกำหนดของกลาง (ระดับ B)

## Comment ของผู้ใช้
(รอผู้ใช้พิมพ์ในแชทครั้งเดียว → session หลักจัดหมวด A/B/C แล้วบันทึกที่นี่เป็น U1, U2, ...)
