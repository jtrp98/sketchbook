---
module: arm-lab
design: D5
covers: [R14]
canvas: C1
updated: 2026-11-11
---

# D5 อ่านท่าทีละข้อ (R14 แก้ 2026-11-11)

อ้างอิง: R14 "อ่านท่าทีละข้อ" (1)–(6) · OQ104–OQ108 (answered) · CHANGELOG 2026-11-11 · `feasibility/R12.md` รอบ 2026-11-11

## สถานะงาน

- **C1 (MainV6A): แก้ในเครื่องแล้ว ยังไม่ publish รออนุมัติ** (C1 แชร์ในองค์กร) · อ่านจาก C1 version `1794362983-1a9b` · ไฟล์เตรียมไว้ที่ scratchpad (ดู "ไฟล์ที่เตรียม publish") · OQ109/OQ110 answered แล้ว · เปิด OQ111 (ไม่ block)
- **C2 (D4 ถ้อยคำแขนอ่อน): publish แล้ว C2 Version 34 `1794379449-a773`** (ดูท้ายไฟล์)
- DS ที่ใช้ (C1): School Bot Studio Design System Version 26 `1794382709-abb3` (Badge, Button + `aria-pressed`, Notice `sb-notice-warning`, Tooltip, ไอคอน `lock`/`triangle-alert` จาก `components/bundle.js`, `components/bundle.css`)

## ไฟล์ที่เตรียม publish (C1 · 2026-11-11)

| published path | ที่มา | เปลี่ยน |
|---|---|---|
| `project/MainV6A.dc.html` | scratchpad แก้แล้ว | E1 state `jLock`/`relOld`/`relMsg` + method `relLockOne`/`relUnlockOne`/`relLockAll`/`relDone` · ค่าสดเฉพาะข้ออ่อน · หยุด = ล็อกทุกข้อ · props ใหม่ของ E2–E7 · ลิงก์ DS css |
| `project/MainV6AJoints.dc.html` | scratchpad แก้แล้ว | E2 notice + E4 ล็อกทั้งหมด แทนแถบส้มเดิม · E3/E5 แถวข้อต่อ · `sb-sr aria-live` · `data-relmenu` ปุ่มเมนู (โฟกัสหลังล็อกทั้งหมด) · ลิงก์ DS css + ฟอนต์ IBM Plex Sans Thai |
| `project/MainV6AStage.dc.html` | scratchpad แก้แล้ว | E7 Badge บนวงกลม ID · E6 ไปท่านี้/กลับท่าพัก `aria-disabled` + `sb-tip` · ลิงก์ DS css |
| `project/MainV6ABar.dc.html` | scratchpad แก้แล้ว | E6 ปุ่มเล่น `aria-disabled` + `sb-tip` · ลิงก์ DS css |
| `project/ds/school-bot/bundle.css` | `{artifact: DS, path: project/components/bundle.css}` | นำเข้า DS v26 (มี Badge, `sb-btn-secondary[aria-pressed]`) |
| `project/ds/school-bot/bundle.js` | `{artifact: DS, path: project/components/bundle.js}` | นำเข้า DS v26 (ขนาดเท่าเดิม 12777 · ส่งเพื่อให้ตรง version) |

ไม่ต้องส่ง `canvas.json` (ไม่เพิ่ม/ย้าย artboard)

## ทำแล้วตามใบสั่ง (สรุป)

- E1 ✔ · E2 ✔ `sb-notice sb-notice-warning` + `triangle-alert` (`sb-i` 20) หัว "กำลังคลายแขน · ล็อกแล้ว n จาก 6 ข้อ" เนื้อ "บิดข้อที่อ่อนด้วยมือ แล้วกด “อ่านท่า” ทีละข้อ" (OQ111 ง) · E3 ✔ `sb-btn sb-btn-secondary sb-btn-sm` `aria-pressed` + ไอคอน `lock` นำหน้า ป้าย "อ่านท่า S#"/"เลิกอ่าน S#" แทน −/+ · E4 ✔ `sb-btn sb-btn-primary` "ล็อกทั้งหมด" + ไอคอน `lock` · E5 ✔ ตัว 16/700 `text-primary` ข้อล็อกมีไอคอน `lock` `sb-i-sm` ข้างตัวเลข ข้ออ่อนไม่มี · `aria-label` บอก "ค่าสด ข้อนี้อ่อนอยู่"/"อ่านแล้ว ล็อกอยู่" · E6 ✔ ไปท่านี้, กลับท่าพัก, เล่น: `aria-disabled` + `sb-tip` "แขนยังอ่อนอยู่ กดล็อกทั้งหมดก่อน" (slider/มือคีบ ถูกแทนด้วยปุ่มอ่านท่าระหว่างโหมดจึงไม่ต้องมีเหตุผล) · E7 ✔ `Badge` (`sb-badge-host` + `sb-badge` + `lock`) · `aria-label` วงกลมเพิ่ม "อ่านแล้ว ล็อกอยู่" · **E8 ไม่ได้ทำ**: ข้อความนี้ไม่มีใน MainV6A เดิม → OQ111 ก
- ถอดปุ่มเดิมในโหมด "ล็อกข้อต่อ" (นับถอยหลัง) และ "＋ เป็นท่าใหม่ต่อจากท่านี้" และกรอบส้มกะพริบของคอลัมน์ข้อต่อ (แทนด้วย notice) → OQ111 ค
- ส่วนเดิมของ MainV6A (Hex/Mitr/Noto) คงไว้ตาม OQ109 · ไอคอน SVG ใช้ path จาก DS `components/bundle.js` ตรงตัว (runtime ของ canvas ไม่เรียก `SchoolBot.hydrate()` ใน `sc-if`)
- ยังไม่มีเกณฑ์ของทีมใน knowledge บางไฟล์: ใช้ WCAG 2.1/2.2 AA ทั่วไป

## ใบสั่งแก้ C1 (ร่าง · ทำเมื่อตอบ OQ109/OQ110 และได้รับอนุมัติ publish)

แก้ผ่าน MainV6A (logic/state) + MainV6AJoints (แถวข้อต่อ) + MainV6AStage (วงกลม ID) เท่านั้น ไม่ทำ MainV6A ใหม่ทั้งหน้า · ส่วนที่เพิ่มโหลด DS (`ds/school-bot/tokens.css`, `components/bundle.css`) ตาม D2 (ConnectV3)

| # | องค์ประกอบ | ที่ | DS ที่ใช้ | หมายเหตุ |
|---|---|---|---|---|
| E1 | state ใหม่ `relaxMode` + `jointRead[6]` (อ่อน/อ่านแล้วล็อก) + ค่าสด | MainV6A logic | - | เข้าโหมดหลังนับถอยหลังของปุ่ม "ปลดล็อกข้อต่อ" เดิม · ล็อกครบ = จบโหมดเอง · ปุ่มหยุด = ล็อกทุกข้อ (OQ105) · หลุด = ล้างสัญลักษณ์และค่าที่อ่าน |
| E2 | สถานะโหมดคลายแขน | หัวแผงข้อต่อ (MainV6AJoints) | `sb-notice sb-notice-warning` + ไอคอน `triangle-alert` (`icon-md` 20) · ตัว 16 `text-primary` | ตำแหน่ง/ถ้อยคำ → OQ110 ก |
| E3 | ปุ่มสลับต่อข้อ "อ่านท่า S#"/"เลิกอ่าน S#" `aria-pressed` | แถวข้อต่อ S0–S5 | `sb-btn sb-btn-secondary sb-btn-sm` (`control-sm` 44) · ข้อความเปลี่ยนตามสถานะ | **DS gap: ไม่มี pressed state ของ `sb-btn`** (OQ109 ข) · ไม่มีคีย์ลัด (OQ108) · ประกาศ `aria-live=polite` เฉพาะล็อก/เลิกอ่าน |
| E4 | ปุ่ม "ล็อกทั้งหมด" | หัวแผงข้อต่อ ใต้ E2 | `sb-btn sb-btn-primary` (`control-md` 48 · ไม่ขยับหุ่นจึงไม่ใช่ `sb-btn-robot`) | หลังกด โฟกัสกลับปุ่มเมนู "ปลดล็อกข้อต่อ" เดิม (OQ108) |
| E5 | ค่าสดตอนข้ออ่อน | ช่องค่าเดิมของแถวข้อต่อ | ตัว 16/700 `text-primary` (ค่าที่ต้องอ่านเพื่อทำงาน = เนื้อหาหลัก README) | **DS gap: ไม่มีรูปแบบ "ค่าสด/กำลังอ่าน"** (OQ109 ค) · ไม่ประกาศค่าสด (OQ108) |
| E6 | ปุ่มสั่งขยับปิดพร้อมเหตุผล (ไปท่านี้/เล่น/กลับท่าพัก/slider/มือคีบ) | MainV6AStage, MainV6ABar, MainV6AJoints | `aria-disabled="true"` + `sb-tip` (Button: ห้าม `disabled` เงียบ) | ถ้อยคำเหตุผล → OQ110 ข |
| E7 | สัญลักษณ์ล็อกบนวงกลม ID เฉพาะข้อที่อ่านแล้วล็อก | `armDots` ใน MainV6A → MainV6AStage | ไอคอน `lock` (มีใน `bundle.js`) `icon-sm` 16 | **DS gap: ไม่มี badge/overlay บนวงกลม ID** (วงกลม ID เองยังเป็นค่าเดิมของ frame ไม่ใช่ DS) (OQ109 ก) · `aria-label` วงกลมเพิ่ม "อ่านแล้ว ล็อกอยู่" · ไม่ใช้สีอย่างเดียว (1.4.1) |
| E8 | ข้อความถาวร "แขนล็อกอยู่ ห้ามบิดด้วยมือ" | ตามเดิม | - | แสดงเมื่อไม่มีข้อใดอ่อน (OQ105 ช ข้อเสนอ ruler) |

## DS gap

**ไม่มี DS gap ค้าง** (3 ข้อด้านล่างปิดแล้วด้วย DS Version 26 · OQ109 · ds-build G21/G22) · ประวัติ:
- (ปิด) DS gap: เครื่องหมาย/badge ซ้อนบนวงกลม ID ข้อต่อ (ขนาด ตำแหน่ง พื้น ขอบ) · ใช้ที่ MainV6AStage วงกลม S0–S5 · ใกล้เคียงที่สุดใน DS: ไอคอน `lock` + `icon-sm` (ไม่มี component badge)
- DS gap: สถานะกดค้าง (`aria-pressed="true"`) ของปุ่มข้อความ `sb-btn` · ใช้ที่ปุ่มสลับ "อ่านท่า S#"/"เลิกอ่าน S#" · ใกล้เคียงที่สุดใน DS: `sb-ibtn[aria-pressed]` (ไอคอนล้วน) / `sb-chip[aria-pressed]` (FilterChip ความหมายตัวกรอง ใช้ข้ามความหมายไม่ได้)
- DS gap: รูปแบบแสดง "ค่าสด" (กำลังอ่าน ยังไม่ล็อก) ให้ต่างจากค่าที่ล็อกแล้วโดยไม่ใช้สีอย่างเดียว · ใช้ที่ช่องค่าแถวข้อต่อ · ใกล้เคียงที่สุดใน DS: `sb-tag` / ตัว 16/700 `text-primary`
- หมายเหตุ: MainV6A ทั้ง frame ยังใช้ Hex/ฟอนต์เดิม (Mitr/Noto) ไม่ใช่ DS · ส่วนที่ D5 เพิ่มจะใช้ DS ทำให้ในหน้าเดียวมีสองชุด (รายงานกลับ ไม่ตัดสินเอง)

## Heuristics / HIG / UD

H1 (สถานะโหมด + สัญลักษณ์ล็อกต่อข้อ) · H3 (เลิกอ่านได้ทีละข้อ, ล็อกทั้งหมด, ปุ่มหยุด) · H5 (ปิดปุ่มสั่งขยับระหว่างโหมด) · H6 (สถานะเห็นบนแถวและบนวงกลม ID) · H9 (เหตุผลบน tooltip) · UD: ไม่ใช้สีอย่างเดียว, ข้อความปุ่มระบุ S#

## WCAG AA (ตามแผน ยังไม่ได้ตรวจบน render)

- 1.4.1: สัญลักษณ์ `lock` + aria-label บนวงกลม ID · ข้อความปุ่มเปลี่ยน ไม่พึ่งสี
- 1.4.3: `action-primary` บน `surface` 5.55 · ขาวบน `action-primary` 5.55 · ตัว `text-primary` บน `warning-bg` ตาม DS
- 2.5.8 / ข้อกำหนดทีม: ปุ่มสลับ 44 (`control-sm`) · ล็อกทั้งหมด 48
- 4.1.2: `aria-pressed` + ชื่อปุ่มเปลี่ยน · 4.1.3: ประกาศเฉพาะล็อก/เลิกอ่าน (`aria-live=polite`)
- 2.4.7: focus ring `action-primary` 3px offset 2 (DS)

## C2 · D4 ถ้อยคำแขนอ่อนแบบกลาง (R14 (6) · publish C2 Version 34 `1794379449-a773` · 2026-11-11)

- `HoldArm`: หัว "ประคองแขนไว้ก่อน บางข้ออาจยังอ่อนอยู่" · เนื้อ "สายหุ่นหลุดตอนปลดล็อกข้อต่อ บางข้ออาจยังอ่อนอยู่ ประคองแขนไว้และตรวจดู แล้วเรียกครู" (คงเรื่องเรียกครูตาม R14)
- `BannerArmWeak` (ข้อความอยู่ใน `ArmShell` titles.armweak): "บางข้ออาจยังอ่อนอยู่ ประคองแขนไว้และตรวจดู แล้วเรียกครู"
- ไม่แตะ `BackAskArmWeak` (นอกขอบเขตงาน · ถ้อยคำ "แขนอาจยังอ่อนอยู่" ยังเป็นแบบกลางพอ)
- ไม่มี DS gap ในส่วนนี้ (component เดิม `sb-dialog`, `sb-banner-warn`)

## ข้อเสนอแนะ

- ขออนุมัติ publish C1 ตาราง "ไฟล์ที่เตรียม publish" แล้วเปิดดู render (ยังไม่ได้ตรวจ: ความสูงแผงข้อต่อ 424 กับ notice + 6 แถว อาจล้น · tooltip ชิดขอบ)
- ตอบ OQ111 (E8 ตำแหน่งข้อความถาวร, หยุดแล้วเขียนค่าหรือไม่, ปุ่มเดิมที่ถอด)
- พิจารณาให้ DS มี badge ทั่วไปสำหรับเครื่องหมายบนวงกลม/ไอคอน (ใช้ซ้ำได้ใน Arm Lab)
