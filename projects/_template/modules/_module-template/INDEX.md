---
module: <ชื่อ module>
updated: YYYY-MM-DD
status: draft
depends_on: []
---

# <ชื่อ module> (สารบัญ module)

เป้าหมาย: <1 บรรทัด>

## ไฟล์ (อ่านเฉพาะที่งานต้องใช้)

| ไฟล์ | อ่านเมื่อ |
|---|---|
| requirements.md | ต้องรู้ว่าต้องทำอะไร (R#, กฎ, edge case) |
| oq.md | ต้องรู้ว่ามีอะไรยังไม่ตัดสิน |
| feasibility.md | ตรวจ logic / ดูเงื่อนไขจาก role 2 |
| design/ | แก้หรือตรวจ design (เลือกไฟล์ D# จากตาราง Design) |
| review.md | ดูผลตรวจ |
| handoff.md | ส่งต่อ dev (มีเมื่อทำ handoff แล้ว) |

## Canvas

สร้าง canvas: session หลักเท่านั้น · ไม่มี C# ที่ใช้ได้ → ถามผู้ใช้ก่อนเริ่มงานทุกครั้ง (กฎ "ไม่มี canvas" ใน CLAUDE.md) · สิทธิ์: private / shared (shared ต้องได้รับอนุมัติก่อน publish)

| ID | ชื่อ | ลิงก์ | สิทธิ์ | ใช้กับ |
|---|---|---|---|---|

## ติดตาม R → D → OQ

| Req | สรุป | Design | OQ |
|---|---|---|---|

## Design

| ID | ครอบคลุม | ไฟล์ | Canvas | Artboard | Publish | อัปเดต |
|---|---|---|---|---|---|---|

## สถานะ
- Feasibility: ยังไม่ได้ทำ
- OQ ที่ยังเปิด: -
- Review: ยังไม่ได้ทำ
- ข้ามขั้น: -
