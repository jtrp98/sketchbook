---
module: block-lab
updated: 2026-10-21
status: designed
depends_on: [app-shell, my-work]
---

# Block Lab (สารบัญ module)

เป้าหมาย: นักเรียน ป.1–6 ต่อบล็อกสั่งบอร์ด Arduino Uno (โค้ด C++ อ่านอย่างเดียว) ทดสอบด้วยตัวจำลองบอร์ดต่อสายอิสระ + stage มาสคอต + แผงข้อความจากบอร์ด แล้วส่งลงบอร์ดจริง · พื้นที่เล่นอิสระ ไม่มีภารกิจ

นำเข้าจากระบบเก่า 2026-10-21 · **sketchbook เป็นแหล่งความจริงแล้ว** (ไม่ต้องเปิดโฟลเดอร์ `~/Documents/School Bot/`) · ป้ายหลักฐานดู `../../context.md`

## ไฟล์ (อ่านเฉพาะที่งานต้องใช้)

| ไฟล์ | อ่านเมื่อ |
|---|---|
| requirements.md | ต้องรู้ว่าต้องทำอะไร (R1–R13, ตารางหมวดบล็อก 10 หมวด, AC, edge case) |
| oq.md | ต้องรู้ว่ามีอะไรยังไม่ตัดสิน / ตัดสินแล้ว |
| feasibility.md | ตรวจ logic / ดูเงื่อนไขจาก role 2 (ผลรวม 2026-10-21) · ตารางผลรายข้อ · ข้อขัดแย้ง X1–X9 · ผลกระทบ module พึ่งพา · R12, R13 · BUG-13–20 |
| feasibility/R1.md … R11.md | §ผลตรวจ ruler ต้นไฟล์ + รายละเอียดหน้าจอ (SCR) สถานะ (ST) ข้อมูล (ENT) ประเด็น (ARC-I) DEV-Q ตาม R# (ตารางใน feasibility.md) |
| design/ | แก้หรือตรวจ design (เลือกไฟล์ D# จากตาราง Design) · D1–D5 |
| review.md | ดูผลตรวจ / รายการที่ highlighter ต้องตรวจเป็นพิเศษ |
| handoff.md | ส่งต่อ dev (ยังไม่มี) |

อ่านเพิ่มเมื่อออกแบบ: `../../brand.md` (§1–7 token, §8 มาสคอต, §9–10 ข้อตัดสินและ DSG) · `../../context.md` · module พึ่งพา: `../app-shell/` (แถบหน้าต่าง ชิปอุปกรณ์ Uno) และ `../my-work/` (งานของฉัน/บันทึก/export) เฉพาะ INDEX + requirements

## Canvas

สร้าง canvas: session หลักเท่านั้น · ไม่มี C# ที่ใช้ได้ → ถามผู้ใช้ก่อนเริ่มงานทุกครั้ง (กฎ "ไม่มี canvas" ใน CLAUDE.md) · สิทธิ์: private / shared (shared ต้องได้รับอนุมัติก่อน publish)

| ID | ชื่อ | ลิงก์ | สิทธิ์ | ใช้กับ |
|---|---|---|---|---|
| C1 | School Bot – Block Lab | https://claude.ai/artifact/YYgSHL2aCtVbkDTgBQBzTV | private | D1–D5 (สร้างใหม่ 2026-10-21 ตามที่ผู้ใช้เลือก · version 6 · 14 ไฟล์: 6 หน้า + 8 ชิ้นส่วน) |

artifact เดิมด้านล่างใช้ไม่ได้ถ้าผู้ใช้ไม่ยืนยันและ `read` ไม่ได้ก่อนลงทะเบียน

## Canvas และ frame ที่พบในระบบเก่า (ยังไม่ใช่ C#/D#)

| FRM เดิม | ชื่อ frame / ไฟล์ | artifact | สถานะในระบบเก่า | หมายเหตุ |
|---|---|---|---|---|
| (EV-04) | Main-1D "1D · ลากต่อบล็อกได้จริง — สีชุด B" + BlockColors-1D | [School Bot – Block Studio (ประถม)](https://claude.ai/artifact/1tXuNM7Q26QfEfv5Legqrh) (Canvas C เดิม) | Draft (ร่าง · DEC-08) | ฐานของ FRM-16 · อ่านโค้ดแล้ว ไม่ได้ render · เป็น ESP32/MixGo/Python + แถบภารกิจ (CF-01) ต้องทำใหม่ |
| FRM-16 | SCR-16 พื้นที่ต่อบล็อก + ดูโค้ด | Canvas C เดิม | ยังไม่เริ่ม | ฐาน Main-1D · ตัดแถบภารกิจ · 856 · สถานะบันทึกเป็นตัวหนังสือเขียวใต้ชื่องาน |
| FRM-17 | SCR-17 ตัวจำลองบอร์ด (แท็บใน FRM-16) | Canvas C เดิม | ยังไม่เริ่ม | Tweaks ตามแผน: ST-28, ST-29 (+ ST-40, ST-41 ตาม SCREEN_INVENTORY v4) |
| FRM-18 | SCR-18 stage (แท็บใน FRM-16) | Canvas C เดิม | ยังไม่เริ่ม | ใช้มาสคอตจริง (DEL-09) |
| FRM-19 | SCR-19 เชื่อม Uno + ส่งลงบอร์ด | Canvas C เดิม | ยังไม่เริ่ม | Tweaks: ST-30, 32–34 (+ ST-45–47) · SCR-26 แผงข้อความ ยังไม่มี FRM ในแผนเดิม (เพิ่มใน DEL-08) |
| FRM-05 (ต้นฉบับแถบหน้าต่าง) | WindowBarV1 (app-shell) | [Canvas B](https://claude.ai/artifact/P1JcYv8G7hhXLkHwMFLTVK) | Done (ผู้ใช้อนุมัติ 2026-10-21) · ยังไม่ได้ใส่ใน Canvas C | ต้องแก้ตาม CR-10 ก่อนสำเนามาใช้ · ชิปอุปกรณ์ Uno (CR-08) |

สถานะ canvas เดิม: ต้องจัดแบบเดียวกับ Canvas A ก่อนแตะ (ย้ายฉบับเก่าไป `ARCHIVE — …`, แยก component, ≤ ~15 frame) ตามบทเรียนใน `../../context.md`

## ติดตาม R → D → OQ

| Req | สรุป | Design | OQ |
|---|---|---|---|
| R1 | หมวดบล็อก 10 หมวดสำหรับ Uno | D1 | OQ4, OQ11, OQ23, OQ25, OQ35 |
| R2 | รูปทรงและกฎต่อบล็อก (มน/หกเหลี่ยม, setup/loop 1 บล็อก) | D1 | OQ11, OQ26, OQ29, OQ32 |
| R3 | ดูโค้ด Arduino C++ อ่านอย่างเดียว | D1 | OQ2, OQ16, OQ25, OQ26, OQ27 |
| R4 | ตัวจำลองบอร์ดต่อสายอิสระ | D2 | OQ1, OQ13, OQ20, OQ21, OQ25, OQ29, OQ32–OQ35 |
| R5 | ความเสียหายสมจริง ไม่กะพริบ | D2 | OQ1, OQ9, OQ28, OQ34 |
| R6 | โต้ตอบปุ่มกด/potentiometer + คีย์บอร์ด | D2 | OQ15, OQ25 |
| R7 | stage + มาสคอต | D3 | OQ14, OQ19, OQ27, OQ28, OQ34 |
| R8 | แผงข้อความจากบอร์ด | D4 | OQ2, OQ10 |
| R9 | เชื่อม Uno · ส่งลงบอร์ด · หยุดทั้งหมด | D5 | OQ3, OQ18, OQ22, OQ26, OQ27, OQ30, OQ31, OQ32, OQ36 |
| R10 | จำลองพร้อมกัน · แก้ระหว่างจำลองหยุดเอง | D1 (+D2, D3) | OQ8, OQ17, OQ26, OQ27, OQ31 |
| R11 | โครงหน้า · ไม่มีภารกิจ · งานใหม่/งานของฉัน | D1 | OQ5, OQ7, OQ24, OQ31, OQ32, OQ33 |
| R12 | UI เดียว ป.1–6 (RSK-09) | D1–D5 | OQ6, OQ29, OQ33, OQ34, OQ35 |
| R13 | สั่งแขนกล (Future · นอก MVP) | - (ไม่ออกแบบ: นอก MVP ตาม DEC-17) | OQ12 |

## Design

| ID | ครอบคลุม | ไฟล์ | Canvas | Artboard | Publish | อัปเดต |
|---|---|---|---|---|---|---|
| D1 | R1, R2, R3, R10, R11, R12 | design/D1-editor.md | C1 | `Main.dc.html` (A) · `Spec.dc.html` (F) · ชิ้นส่วน `BlocksPane` `WindowBar` `BottomBar` `Mascot` | canvas v6 (2026-10-21) · ยังไม่ได้ตรวจบน canvas | 2026-10-21 |
| D2 | R4, R5, R6 | design/D2-simulator.md | C1 | `SimStates.dc.html` (B) · ชิ้นส่วน `SimPane` | canvas v6 (2026-10-21) | 2026-10-21 |
| D3 | R7 | design/D3-stage.md | C1 | `StageStates.dc.html` (C) · ชิ้นส่วน `StagePane` | canvas v6 (2026-10-21) | 2026-10-21 |
| D4 | R8 | design/D4-serial-panel.md | C1 | `SerialStates.dc.html` (D) · ชิ้นส่วน `SerialPane` | canvas v6 (2026-10-21) | 2026-10-21 |
| D5 | R9 | design/D5-upload-board.md | C1 | `SendStates.dc.html` (E) · ชิ้นส่วน `Cards` | canvas v6 (2026-10-21) | 2026-10-21 |

## ขั้นถัดไปที่ระบบเก่าวางไว้ (ข้อ 3 ทำแล้วใน C1 รอบ 2026-10-21 · ข้อ 1 ทำแล้วบางส่วน: แถบหน้าต่างเป็นสำเนาชั่วคราว · ดู D1–D5)
1. Designer เริ่ม Canvas C (FRM-16–19 + SCR-26) หลังแก้แถบหน้าต่างที่ต้นฉบับ Canvas B ตาม CR-10 ทาง ก (ลดชั้นต่ำกว่า z-stop) + AUD-F04/F05/F06 แล้วสำเนาไป Canvas C · ตัดแถบภารกิจ · ใช้มาสคอตจริง (ตัดแยกท่า DEL-09) · พื้นที่ 856 (CR-09)
2. ขอ dev ตอบ DEV-Q13 (ความเสียหาย) · DEV-Q14 (Serial จริง) · DEV-Q16 (หยุดทั้งหมดบน Uno)
3. Block Lab ตัวแก้ไขต้องมี "งานใหม่ (Ctrl+N)" + "งานของฉัน" (CR-07 · ตำแหน่ง Delegated)
4. ทำ token สีหมวดบล็อก (ยังไม่มีใน design system) · จับคู่บล็อกรายตัวจาก 126 บล็อกกับ dev

## สถานะ
- Feasibility: **ทำได้มีเงื่อนไข** (2026-10-21 · `ruler`) · R1–R12 ทำเป็น UI ได้ · R13 Future ไม่ประเมิน · ขั้นถัดไป: รอผู้ใช้ยืนยัน → session หลักเปลี่ยนเป็น `approved` (ยังเป็น `draft`) · พบข้อขัดแย้งใน requirement 9 ข้อ (X1–X9 ใน feasibility.md) ไม่แก้ `requirements.md` ให้ session หลักตัดสิน
- OQ ที่ยังเปิด: OQ1, OQ2, OQ3 (Material · ไม่ block ออกแบบ แต่ต้องตอบก่อนส่ง dev) · OQ4, OQ5, OQ8–OQ16, OQ21 · **จาก ruler:** OQ26–OQ30, OQ32, OQ33, OQ35 · **ใหม่จากการออกแบบ:** OQ36 · ต้องตอบก่อนส่ง dev: OQ1–3, OQ5, OQ27 (OQ25 ตอบแล้ว) · ปิดแล้ว: OQ6, OQ7, OQ17–OQ20, OQ22–OQ25, OQ31, OQ34
- Design: **designed** (2026-10-21 · `crayon`) · D1–D5 publish ที่ C1 (v6) ครบ R1–R12 · R13 ไม่ออกแบบ (Future นอก MVP) · ยังไม่ได้ render/ตรวจบน canvas · ค่าชั่วคราวที่ต้องเป็น DSG: สีหมวดบล็อก 10 สี (DSG-13), ขอบล่างปุ่มหยุด #8E1B1B (DSG-12), ภาพอุปกรณ์เวกเตอร์ (DSG-09) · แถบหน้าต่างเป็นสำเนาชั่วคราว (รอสำเนาจาก Canvas B หลัง CR-10) · ค้างจากรอบนี้: LED บนบอร์ดขา 13 (OQ13), ภาพแทนเสียงบนบัซเซอร์ (OQ35), ตัวนับตัวอักษรบล็อก "พูด" · ผู้ใช้ต้องตัดสิน: ค่าเริ่มต้นเสียง (OQ35), สีปุ่มส่งลงบอร์ด (OQ36), ค่าเริ่มต้นแผงโค้ด · OQ ใหม่: OQ36 · OQ7 ตอบแล้ว (Designer)
- Review: ยังไม่ได้ทำ (Auditor ระบบเก่ายังไม่เคยตรวจ Block Lab · รายการที่ต้องตรวจเป็นพิเศษอยู่ใน review.md)
- ข้ามขั้น: -
