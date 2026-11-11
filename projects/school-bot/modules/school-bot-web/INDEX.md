---
module: school-bot-web
updated: 2026-11-11
status: draft
depends_on: [quiz, block-lab, app-shell]
---

# เว็บ School Bot (สารบัญ module · เดิม teacher-web "เว็บครู" · เปลี่ยนชื่อ 2026-11-11)

เป้าหมาย: ครูในโรงเรียนลูกค้า SchoolBright ใช้เว็บ (แยกจากแอป) ดูความคืบหน้าและคะแนน Quiz รายเทอม/รายปี จัดตามห้อง · ตั้งค่า · แก้ปัญหาหุ่น · ไม่ใช้มาสคอต · ไม่แสดงงาน Arm/Block

**เพิ่ม 2026-11-11:** ครูและนักเรียน login เห็นเนื้อหาตามบทบาท · เมนู Guideline (Block · Sensor 33 บท 3D · Innovation 4 ตัวอย่าง · phase 1 เฉพาะ Block Lab) · ไม่ใช้มาสคอตเฉพาะส่วนของครู · พึ่งพา block-lab (หมวดบล็อก R18, `sensor-list.md`) และ app-shell (บัญชีนักเรียน)

**sketchbook เป็นแหล่งความจริงแล้ว** (นำเข้าจากระบบเก่า 2026-10-21) · บริบทร่วม: `../../context.md` · brand: `../../brand.md`

## ไฟล์ (อ่านเฉพาะที่งานต้องใช้)

| ไฟล์ | อ่านเมื่อ |
|---|---|
| requirements.md | ต้องรู้ว่าต้องทำอะไร (R#, กฎ, edge case) |
| oq.md | ต้องรู้ว่ามีอะไรยังไม่ตัดสิน |
| feasibility.md | ตรวจ logic / ดูเงื่อนไขจาก role 2 (สารบัญ + ทั่วไป) |
| feasibility/R1.md–R15.md | รายละเอียดราย R# (R1, R8–R15 + ส่วนบนของ R2 = ผล ruler 2026-11-11 · R3–R7 = ข้อมูลอ้างอิง Architect เดิม) |
| design/ | แก้หรือตรวจ design (ยังว่าง) |
| review.md | ดูผลตรวจ |
| handoff.md | ส่งต่อ dev (ยังไม่มี) |

## Canvas

สร้าง canvas: session หลักเท่านั้น · ไม่มี C# ที่ใช้ได้ → ถามผู้ใช้ก่อนเริ่มงานทุกครั้ง (กฎ "ไม่มี canvas" ใน CLAUDE.md) · สิทธิ์: private / shared (shared ต้องได้รับอนุมัติก่อน publish)

| ID | ชื่อ | ลิงก์ | สิทธิ์ | ใช้กับ |
|---|---|---|---|---|

ยังไม่มี C# ที่ลงทะเบียนสำหรับ module นี้ → ถามผู้ใช้ก่อนเริ่มงาน canvas

## Canvas และ frame ที่พบในระบบเก่า (ยังไม่ใช่ C#/D#)

| FRM เดิม | ชื่อ frame / ไฟล์ | artifact | สถานะในระบบเก่า | หมายเหตุ |
|---|---|---|---|---|
| FRM-20 | login เว็บครู (SCR-21) | Canvas D "School Bot Studio — เว็บครู" ยังไม่สร้าง | ยังไม่สร้าง | Tweaks: ST-07, ST-08 (ลิงก์ไป SchoolBright) · ขนาดงาน เล็ก |
| FRM-21 | ภาพรวมห้อง (SCR-22) | Canvas D (ยังไม่สร้าง) | ยังไม่สร้าง · Assume (DEV-Q01) | Tweaks ST-35/36/37 · 40+ คน · ตัวกรอง ปี → เทอม/ทั้งปี → ห้อง · ขนาดงาน กลาง |
| FRM-22 | รายละเอียดนักเรียน (SCR-23) | Canvas D (ยังไม่สร้าง) | ยังไม่สร้าง · Assume | Tweaks ST-35/36 · ตารางผลรายด่าน + สถานะส่ง SchoolBright |
| FRM-23 | ตั้งค่า (SCR-24) | Canvas D (ยังไม่สร้าง) | ยังไม่สร้าง | Tweak ST-38 · ขนาดงาน กลาง |
| FRM-24 | แก้ปัญหาหุ่น (SCR-25) | Canvas D (ยังไม่สร้าง) | ยังไม่สร้าง | Tweaks ST-35, ไม่มีรายงานสถานะ |

ไม่มี canvas เดิมที่ใช้กับ module นี้ · ออกแบบที่ 1280px ขึ้นไป + Tweak 1024px (DSG-01)

## ติดตาม R → D → OQ

| Req | สรุป | Design | OQ |
|---|---|---|---|
| R1 | login 2 บทบาท: ครู (SchoolBright) + นักเรียน (บัญชีแอป) · เมนูตามบทบาท | - | OQ1, OQ2, OQ3, OQ8, OQ15, OQ18, OQ31, OQ44, OQ46 |
| R2 | ตัวกรอง ปี → เทอม/ทั้งปี → ห้อง บนสุดทุกหน้า | - | OQ1, OQ9, OQ34 |
| R3 | ภาพรวมห้อง ค้นหา เรียง กรอง | - | OQ1, OQ10, OQ11 |
| R4 | รายละเอียดนักเรียนรายด่าน + สถานะส่งคะแนน | - | OQ1 |
| R5 | ตั้งค่า: เปิด/ปิดหน่วย เวลาเปิดด่าน เครื่องและหุ่น | - | OQ6, OQ7, OQ8 |
| R6 | แก้ปัญหาหุ่น: คู่มือ + สถานะหุ่น | - | OQ13, OQ14 |
| R7 | สิทธิ์ ข้อมูลเด็ก (ห้องที่สอน, ไม่มีหน้ายินยอม) | - | OQ4, OQ5 |
| R8 | แพลตฟอร์ม 1280/1024, 3 ภาษา, ไม่ใช้มาสคอตเฉพาะส่วนครู (Guideline ใช้ได้) | - | OQ12, OQ23, OQ30, OQ33, OQ44, OQ46 |
| R9 | เมนู Guideline 3 หัวข้อ · phase 1 เฉพาะ Block Lab · ยังไม่เก็บความคืบหน้า | - | OQ15, OQ23, OQ24, OQ26, OQ34, OQ35, OQ46 |
| R10 | Block: Basic/Advanced → หมวด → การ์ดบล็อก + ตัวอย่างการต่อ + animation | - | OQ20, OQ27, OQ29, OQ39, OQ40, OQ46 |
| R11 | Sensor: บท 3D 33 รายการ · การ์ดชี้ · 4 tab · ผังวงจร · รายการบท | - | OQ16, OQ17, OQ25, OQ36, OQ42, OQ43, OQ45, OQ46 |
| R12 | ต่อสายทีละเส้นเป็นขั้น | - | OQ19, OQ35, OQ37, OQ46 |
| R13 | Try it yourself: C++ อ่านอย่างเดียว · รัน · ไฮไลต์บรรทัด · แถบปรับค่า · Serial | - | OQ17, OQ25, OQ32, OQ36, OQ37, OQ38, OQ42, OQ46 |
| R14 | Innovation 4 ตัวอย่าง | - | OQ21, OQ26, OQ35, OQ38, OQ41, OQ46 |
| R15 | เนื้อหา Claude ร่าง ทีมตรวจ | - | OQ22, OQ28, OQ33, OQ42, OQ43, OQ45, OQ46 |

## Design

| ID | ครอบคลุม | ไฟล์ | Canvas | Artboard | Publish | อัปเดต |
|---|---|---|---|---|---|---|

## ขั้นถัดไปที่ระบบเก่าวางไว้
- สร้าง Canvas D "School Bot Studio — เว็บครู" แล้วออกแบบ FRM-20–24 (ตามลำดับ 20 → 24)
- เจ้าของ design system บันทึก DSG-01 เป็น D ใหม่ใน DECISIONS.md (เว็บครู 1280 หลัก รองรับ 1024)
- รอ DEV-Q01 (API SchoolBright) ก่อนส่ง dev สำหรับ SCR-22, SCR-23

## สถานะ
- **Feasibility 2026-11-11 (`ruler`): ทำได้มีเงื่อนไข** · ขอบเขต R1, R8, R9–R15 + R2 เฉพาะผลกระทบ R1/R9 (R3–R7 ยังไม่ได้ตรวจโดย ruler) · **ต้องตัดสินก่อน `approved`:** OQ26, OQ34, OQ35 · OQ เปิดใหม่จาก feasibility: OQ34–OQ46 (ถามผู้ใช้ด้วย AskUserQuestion ไม่ได้ในรอบ ruler ให้ session หลักถาม) · OQ ที่ยังเปิดทั้งหมด: OQ1, OQ5, OQ7–OQ11, OQ14, OQ24–OQ46 · DS gap: OQ46 (`feasibility.md`) · `status` ยังเป็น `draft` (session หลักเป็นผู้เปลี่ยน)
- **2026-11-11 (ก่อน ruler):** เพิ่ม R9–R15 (Guideline) + แก้ R1, R8 · ยังไม่ผ่าน `ruler` · OQ เปิดใหม่: OQ24–OQ33 · answered ใหม่: OQ15–OQ23 · feasibility/R1.md–R8.md ยังเป็นผลก่อนแก้ R1/R8
- R3–R7: ยังไม่ได้ตรวจโดย `ruler` (มีข้อมูลอ้างอิงจาก Architect เดิม: GO WITH CONDITIONS ดู feasibility.md)
- OQ เดิมที่ยังเปิด: OQ1 (DEV-Q01 · block ส่ง dev ไม่ block ออกแบบ), OQ5, OQ7, OQ8, OQ9, OQ10, OQ11, OQ14 · answered: OQ2, OQ3, OQ4, OQ6, OQ12, OQ13, OQ15–OQ23
- Review: ยังไม่ได้ทำ (Auditor เดิมไม่มี finding ของเว็บครู)
- ข้ามขั้น: -
