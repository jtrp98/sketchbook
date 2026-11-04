---
module: arm-lab
updated: 2026-11-04
status: draft
depends_on: [app-shell, my-work]
---

# Arm Lab (สารบัญ module)

เป้าหมาย: นักเรียน ป.1–6 สอนท่าแขนกล 6 ข้อต่อ แล้วเล่นเป็นลำดับ กับหุ่น Raspberry Pi ผ่าน USB · ครูตั้งค่าขั้นสูงในโหมดครู

ข้อมูลจากระบบเก่า (`~/Documents/School Bot/Handoff`) นำเข้ามาไว้ใน module นี้ครบแล้ว (2026-10-21) **sketchbook เป็นแหล่งความจริง** ไม่ต้องเปิดโฟลเดอร์เดิม · บริบทร่วมโปรเจกต์: `../../context.md` · brand: `../../brand.md`

## ไฟล์ (อ่านเฉพาะที่งานต้องใช้)

| ไฟล์ | อ่านเมื่อ |
|---|---|
| requirements.md | ต้องรู้ว่าต้องทำอะไร (R1–R17, กฎ, ตัวเลข/ขีดจำกัด, edge case) |
| oq.md | ต้องรู้ว่ามีอะไรยังไม่ตัดสิน (OQ1–OQ24) |
| feasibility.md | ผล feasibility รวม (ruler 2026-10-21) + ตารางผลรายข้อ + เงื่อนไขหลัก + สถานะที่ขาด (H1/H5/H9) + BUG ของ frame ฐาน (ข้อมูล BUG/EDIT จาก Architect เดิม) |
| feasibility/R1.md | R1, R2, R3, R10: ฐาน 6A, โปรโตคอล Pi, แขนบนจอไม่ขยับ, ป.1–6 (ARC-I04, DEV-Q02) |
| feasibility/R4.md | R4: โหมดครู (SCR-14, SCR-15, ST-26) |
| feasibility/R5.md | R5, R11, R16: ปุ่มหยุด, เชื่อมต่อหุ่น, หลุด/เชื่อมกลับ (SCR-12/13, ตาราง ST-19–24/48, ARC-I31, DEV-Q15) · **ท้ายไฟล์: ตรวจใหม่ 2026-11-04 ทางเข้าไฮไลต์ (OQ30–OQ34)** |
| feasibility/R6.md | R6–R9: บันทึก cloud, export .ini, กู้คืนสำรอง, นำเข้า (เทียบ my-work) |
| feasibility/R12.md | R12–R15, R17: ท่า, ข้อต่อ/ขีดจำกัด, แก้/อ่านท่า, การเล่น, เมนูและคีย์ลัด |
| design/ | แก้หรือตรวจ design (D1 มือคีบ % · ดูตาราง Design) |
| review.md | ดูผลตรวจ (รอบ 2026-11-04 D1 โดย highlighter · รอบ 2026-10-21 นำเข้าผล Auditor เดิม AUD-F01, F02, F07–F09) |
| handoff.md | ส่งต่อ dev (ยังไม่มี) |

## Canvas

สร้าง canvas: session หลักเท่านั้น · ไม่มี C# ที่ใช้ได้ → ถามผู้ใช้ก่อนเริ่มงานทุกครั้ง (กฎ "ไม่มี canvas" ใน CLAUDE.md) · สิทธิ์: private / shared (shared ต้องได้รับอนุมัติก่อน publish)

| ID | ชื่อ | ลิงก์ | สิทธิ์ | ใช้กับ |
|---|---|---|---|---|
| C1 | School Bot – หน้าควบคุมแขนกล (ประถม) (Canvas A) | https://claude.ai/artifact/AnEWv6UNbgcNvUXS1sfHQd | shared ในองค์กร (ผู้ใช้เป็นเจ้าของ · `read` ได้ 2026-11-04) | R1–R17 · frame ของ Arm Lab: MainV6A (FRM-02) + component, TeacherLoginV1 (FRM-04), ConnectV3 (FRM-06), TeacherV5A (FRM-08) · **D1** (แก้ที่ MainV6A + MainV6AJoints + MainV6ASeq + MainV6ABar) · **D2** (ConnectV3 + wrapper Many/Connected/Fail2) · **รอบ 2 nav bar (2026-11-04): MainV6A/MainV6ATopBar รวมเป็นแถบ N1 สูง 60 (WindowBarV1 nav=n1) + พื้นที่ 840 · เอาการ์ดอุปกรณ์ใน body ออก ขยายเวที · TeacherLoginV1/TeacherV5A = N1 แบบเชื่อมต่อ · **ConnectV3 ไม่ถูกแตะ** (ผู้ใช้แก้อีกแชท · WindowBarV1 คงโหมดแถบเก่า 44 ให้) · publish แล้วที่ C1 v757 (2026-11-04 · ผู้ใช้อนุมัติ · ยังไม่ได้เปิดดู render จริง) · **ConnectV3 + wrapper แก้ตาม D2 แล้ว ใช้ DS (`ds/school-bot/tokens.css`, `bundle.css`) + WindowBar N1 · C1 v758 (2026-11-04)**** |

หมายเหตุ C1: canvas นี้มี frame ของ module อื่นด้วย (HomeV6A + HomeRail + WindowBarV1 สำเนา → `app-shell` · MyWorkV1/MyWorkV1Block → `my-work` · LearnMapV1 → `quiz`) → กฎ "1 canvas อยู่ใน module เดียว" ลงทะเบียนไว้ที่ module นี้ก่อน · รอผู้ใช้ตัดสินถ้าต้องแยก canvas
canvas อื่นในระบบเก่า (ยังไม่ลงทะเบียน): Canvas B เข้าระบบ+บทเรียน (WindowBarV1 ต้นฉบับ) · Canvas C Block Studio · ARCHIVE ของ Canvas A (46 ไฟล์ฉบับเก่า) · ดู `app-shell`, `block-lab`

## งานออกแบบเดิม (frame จากระบบเก่า · ยังไม่ลงทะเบียนเป็น D#)

| FRM | ชื่อ / ไฟล์ | สถานะในระบบเก่า | หมายเหตุ |
|---|---|---|---|
| FRM-02 | 6A · Arm Lab MainV6A.dc.html (327 KB) + component MainV6ATopBar, MainV6AStage → MainV6ABar, MainV6AJoints, MainV6ASeq | **Done** (ผู้ใช้อนุมัติ 2026-10-21 หลัง CR-05 + EDIT-07) · EDIT-09 แถบหน้าต่าง + เวที 768 รอตรวจบน canvas | ฐาน frame (อนุมัติแล้ว DEC-08) · แก้ผ่านใบสั่งแก้เท่านั้น · ยังต้องออกแบบ ST-21/ST-48 ตาม CR-11 |
| FRM-04 | login ครู TeacherLoginV1.dc.html (dialog) | **Done** (ผู้ใช้อนุมัติ 2026-10-21) · EDIT-09 รอตรวจ | Tweaks: ok/wrong/student/otherSchool/offKnown/offNew · ข้อมูลตัวอย่าง: โรงเรียนตัวอย่างวิทยา · ครูสมใจ (somjai.k) · น้องมายด์ |
| FRM-06 | เชื่อมต่อหุ่น ConnectV3.dc.html (73 KB) + wrapper Many/Connected/Fail2 | **Draft** · Auditor ตีกลับ (RETURN) · EDIT-10 รอผู้ใช้ตรวจ | ข้อมูลตัวอย่าง: หุ่นกลุ่ม 3 COM7 · หุ่นกลุ่ม 5 COM9 · Bluetooth COM3 · 115200/9600 bps · รหัส E-NOREPLY, E-BUSY · ต้องแก้ตาม CR-10, CR-11, AUD-F07/F08/F09 |
| FRM-08 | เมนูครู 5A TeacherV5A.dc.html (ฐาน SCR-15) | Draft (ฐานเดิม · Assume) · EDIT-03 เปิดที่หน้าเข้าแล้ว + ปุ่มออกจากโหมดครู | หน้า PIN ใน Tweaks ล้าสมัย ต้องลบ · ยังมี emoji เดิม · ทำได้ทุกเมื่อ (ไม่ขึ้นกับ DEV-Q) |
| FRM-07 | กู้คืนงานสำรอง (SCR-10) | ยังไม่สร้าง | module `my-work` |

ข้อควรรู้เมื่อแตะ frame: MainV6A มี logic/state ทั้งหมด (dialog กู้คืน/นำท่าจากงานอื่น/ออก/เริ่มใหม่, ลิ้นชักประวัติ, เมนูซ้อน) ส่ง `vals6` ให้ component ลูก · CSS `.sc-host` = display:contents · ตรวจ emoji ด้วย `tools/check_emoji.py` ของ skill schoolbot-design (ไม่อยู่ใน repo นี้) · แยก component เกิน ~150 KB (ดู `../../context.md` บทเรียน canvas)

## ติดตาม R → D → OQ

D1 (มือคีบ % · R13/R15) มีแล้ว · D2 (หน้าเชื่อมต่อหุ่น · R5/R11/R16) แก้ frame และ publish แล้ว (C1 v758 · 2026-11-04 · ใช้ DS v12 + WindowBar N1 ใน ConnectV3 เท่านั้น) · R# อื่นยังไม่มี D# · frame ที่เกี่ยวข้องดูตารางด้านบน

| Req | สรุป | Design | OQ |
|---|---|---|---|
| R1 | ใช้ 6A แขนกล (MainV6A) เป็นฐาน | - | OQ1, OQ20 |
| R2 | หุ่น Raspberry Pi (ใกล้เคียง Zide) | - | OQ1, OQ12, OQ14 |
| R3 | แขนบนจอไม่ขยับ | - | - |
| R4 | โหมดครู (login ครูโรงเรียนเดียวกัน) | - | OQ6, OQ7, OQ8, OQ9, OQ10, OQ12, OQ19 |
| R5 | ปุ่มหยุด · เตือน · ปิดปุ่มเมื่อหลุด | D2 (publish C1 v758) | OQ11, OQ14, OQ15, OQ26 (answered), OQ29, OQ31 (answered), OQ36, OQ39, OQ43 (answered), OQ45 (answered · ช่องที่เหลือ OQ50), OQ47 (answered ข้อ ก · ที่เหลือ OQ53), OQ50 (answered ข, ง), OQ53 (answered ก, ข) |
| R6 | บันทึกบน cloud | - | OQ2, OQ3, OQ8, OQ21 |
| R7 | export .ini | - | OQ3, OQ22 |
| R8 | กู้คืนสำรองในเครื่อง | - | OQ2, OQ3, OQ21 |
| R9 | นำเข้า .ini (?) | - | OQ4, OQ22 |
| R10 | UI เดียว ป.1–6 · WCAG 2.2 AA | - | OQ8, OQ17, OQ20 |
| R11 | เชื่อมต่อหุ่น USB · สถานะ | D2 (ยังไม่ publish) | OQ5, OQ14, OQ25 (answered), OQ26 (answered), OQ27 (DS เติม 4 ข้อแล้ว ที่เหลือใช้ของเดิม), OQ28 (answered), OQ29, OQ30 (answered บางส่วน), OQ31 (answered), OQ32 (answered), OQ33 (answered บางข้อ), OQ34, OQ36, OQ38, OQ39, OQ41, OQ43 (answered), OQ44 (answered), OQ45 (answered), OQ46 (answered), OQ47 (answered ข้อ ก), OQ48 (answered บางข้อ), OQ49 (answered บางข้อ), OQ54 (answered ข้อ ข), OQ55 (answered บางข้อ), OQ57, OQ58 |
| R12 | ท่าและท่าชุด (G####/K####, ท่า 0, เลิกทำ 6 วินาที) | - | OQ11, OQ17, OQ20 |
| R13 | ข้อต่อและขีดจำกัด (±180/±135/0–100%, 1000–9000 ms) · มือคีบเป็น % ไม่มีองศา/เลข 0 กลางแถบ | D1 | OQ17, OQ22, OQ23, OQ24 |
| R14 | แก้ท่า · อ่านท่าปัจจุบัน · ประวัติ | - | OQ1, OQ12, OQ17, OQ18, OQ52 (จ), OQ58 |
| R15 | การเล่น (ติ๊กดูรอบหุ่น, ช่วงท่า, รอบ, เตือน 30° ไม่นับมือคีบ) | D1 | OQ1, OQ14, OQ16, OQ24, OQ43 (answered), OQ44 (answered), OQ45 (answered), OQ46 (answered), OQ50 (answered ข, ง), OQ51 (answered), OQ52 (answered บางข้อ), OQ56 (answered ก ข · ค ง เปิด), OQ57 (answered ก · ข ค ง เปิด), OQ58 |
| R16 | หุ่นหลุดและเชื่อมกลับ (ST-21, ST-48) | D2 (publish C1 v758) | OQ11, OQ14, OQ15, OQ16, OQ18, OQ25 (answered), OQ26 (answered), OQ28 (answered), OQ29, OQ30 (answered บางส่วน), OQ31 (answered), OQ32 (answered), OQ33 (answered บางข้อ), OQ34, OQ35, OQ36, OQ37, OQ38, OQ39, OQ40, OQ41, OQ43 (answered), OQ44 (answered), OQ45 (answered), OQ46 (answered), OQ47 (answered ข้อ ก), OQ48 (answered บางข้อ), OQ49 (answered บางข้อ), OQ50 (answered ข, ง), OQ51 (answered), OQ52 (answered บางข้อ), OQ53 (answered ก, ข), OQ57, OQ58 |
| R17 | เมนู ☰ และคีย์ลัด | - | OQ13, OQ15 |

## Design

| ID | ครอบคลุม | ไฟล์ | Canvas | Artboard | Publish | อัปเดต |
|---|---|---|---|---|---|---|
| D1 | R13, R15 (มือคีบ S5 เป็น %, ข้อความเก็บนิ้ว) | design/D1-gripper-percent.md | C1 | MainV6A (ฐานของ frame), MainV6AJoints, MainV6ASeq, MainV6ABar | publish แล้ว (C1 v756) | 2026-11-04 |
| D2 | R11, R16, R5 (หน้าเชื่อมต่อหุ่น: แถบปุ่มล่างตายตัว, แตะการ์ดเลือก, ชื่อเดียว, AUD-F02/F07/F08/F09, CR-11) | design/D2-connect-actions.md | C1 | ConnectV3 (FRM-06) + wrapper Many/Connected/Fail2 | publish แล้ว (C1 v758 · DS v12 · 2026-11-04 · ยังไม่ได้เปิดดู render จริง) · OQ42: เปลี่ยนหุ่นไม่มี guard (MainV6A, C1 v763) | 2026-11-04 |

## ขั้นถัดไปที่ระบบเก่าวางไว้
1. Designer: แก้ ConnectV3 (AUD-F07, F08) + ออกแบบ ST-21/ST-48 ตาม CR-11 ใน FRM-06 และ FRM-02 (ตัดทางข้ามท่าพัก · วิธีหยุดทางกายภาพเป็นข้อความถาวร)
2. Designer: แก้แถบหน้าต่างที่ต้นฉบับ (CR-10 ทาง ก) แล้วสำเนามา Canvas A · FRM-08 เมนูครู (ลบหน้า PIN ใน Tweaks, ตัด emoji)
3. ผู้ใช้: ตรวจ EDIT-09/EDIT-10 บน canvas · ตอบ OQ11 กับ firmware

## สถานะ
- **2026-11-04 (ruler รอบ 6):** ตรวจ R11/R14/R15/R16 ตาม requirements.md จริง · ผล feasibility **ทำได้มีเงื่อนไข** (ไม่เปลี่ยน) · **ยังไม่พร้อม approved** (สถานะคง `draft`) · เปิด OQ58 (ปลดล็อกข้อต่อ vs ข้อความ popup · slider ล็อก/ตำแหน่งไม่ทราบ · พับแขน/ตัดการเชื่อมต่อไม่อยู่ใน trigger · ปุ่มปิดตอนยังไม่เชื่อม · Arm Lab ไม่มีไฟล์) · OQ56 (ก, ข) และ OQ57 (ก) บันทึกเป็น "ตามที่ session หลักแจ้ง" (ไม่มีคำตอบดิบ) · **OQ ที่ยังเปิดก่อน approved:** OQ58 ก ค · OQ50 ก ค จ ฉ · OQ56 ค · OQ57 ข ง · OQ54 ก ค · OQ52 ก จ · OQ13 · เอกสารที่ยังอ้าง ST-48/ST-24 (D1, D2, app-shell, my-work, feasibility ฯลฯ) ดู `feasibility/R5.md` "รอบ 6" ข้อ 3 · หมายเหตุ: บรรทัด "การเปลี่ยนสถานะ ... ตอนนี้ approved" ด้านล่างล้าสมัย (status จริง = draft) และตาราง FRM-02/ขั้นถัดไป ข้อ 1 ยังเป็นฉบับก่อน CR-11 ใหม่
- **2026-11-04 (ruler รอบ 5):** ผล feasibility **ทำได้มีเงื่อนไข** (ไม่เปลี่ยน) · บันทึกคำตอบ OQ50 (ข, ง) · OQ51 · OQ52 (ข, ค) · OQ53 (ก, ข) · OQ54 (ข) · OQ55 บางส่วน · **OQ ที่ยังเปิด:** OQ50 (ก, ค, จ, ฉ) · OQ52 (ก, จ, ตีความ ข) · OQ53 ค · OQ54 (ก, ค, นิยาม "ครั้งแรก") · OQ55 (พอร์ต/ผูกชื่อ) · OQ56 · OQ57 · OQ40 · ร่าง R14/R16 พร้อมบันทึก · R11/R15 บันทึกได้แบบมี ⟨OQ#⟩ แต่ยังไม่ควร approved · requirements.md ยังไม่ถูกแก้ · ดู `feasibility/R5.md` "รอบ 5"
- **2026-11-04 (ruler รอบ 3 · flow เชื่อมหุ่นแบบใหม่):** ผล feasibility **ทำได้มีเงื่อนไข** (ไม่เปลี่ยน · ความเสี่ยงความปลอดภัยสูงขึ้นเพราะถอดท่าพักบังคับ) · OQ43 answered (บันทึกคำตัดสินผู้ใช้ · แทนที่ OQ32/OQ35 คำตอบ/OQ36 ชิปสถานะกลาง/OQ37/OQ38/OQ33 ข้อ 4) · **OQ44–OQ49 `open`** (ความเร็วก้าวแรก · ขอบเขต popup · อายุ/รีเซ็ตติ๊ก · แถบเหลือง · ไฟล์อัตโนมัติ · ชื่อหุ่น) + OQ40 (ถ้อยคำถอดไฟ) ยังเปิด · ต้องตอบก่อน designed: OQ44–OQ48, OQ40 · requirements.md R11/R15/R16 ยังเป็นฉบับเก่า (session หลักแก้ → draft) · D1/D2 ต้องปรับ · ดู `feasibility/R5.md` "รอบ 3"
- **2026-11-04: สถานะกลับเป็น `draft`** เพราะแก้ R11/R16 (ทางเข้าแบบนำทางด้วยไฮไลต์ · OQ30) · **ruler ตรวจแล้ว 2026-11-04: ทำได้มีเงื่อนไข** (`feasibility/R5.md` หัวข้อ "ตรวจใหม่ 2026-11-04") · OQ31–OQ34 `open` (ข้อยกเว้น "กดที่ใดก็ตาม" · ST-48 อยู่ที่ไหน/ปุ่มกลับ · นิยามรอบ/สถานะ · DS gap) ถามผู้ใช้ด้วย AskUserQuestion ไม่ได้ในรอบ ruler → session หลักถาม · ไม่ block feasibility · ต้องตอบก่อน approved/designed · D1 และ D2 (publish บน C1 v758) ต้องปรับตามคำตอบ · ดู CHANGELOG 2026-11-04
- **2026-11-04 (ruler รอบ 2 · ความย้อนแย้ง/ความงงของเด็ก):** ผล feasibility คงเดิม ทำได้มีเงื่อนไข · เปิด OQ35–OQ41 `open` (ท่าพักซ้อนหลายที่ · สัญญาณพร้อมเล่น · popup หายเอง vs ค้าง · ระดับผ่อน · popup ดักการกด · ถ้อยคำถอดไฟ adapter · ชื่อหุ่น/logout) · OQ31, OQ32 answered แล้ว (บรรทัดบนเขียน open ล้าสมัย) · D2 ต้องปรับตาม OQ32/OQ35 · ดู `feasibility/R5.md` "ความย้อนแย้ง/ความงง รอบ 2"
- **2026-11-04 (ruler รอบ 4): ผู้ใช้ตอบ OQ44–OQ49 แล้ว (บางข้อมีช่องเหลือ) · OQ40 answered ส่วนวิธี · ยังไม่พร้อมบันทึก R11/R15/R16 ลง requirements.md เต็มรูป** เพราะมี OQ ที่ต้องตัดสินก่อนเขียน: OQ50 (ST-23 รวม/แยก · คำสั่งหลังติ๊ก · Esc) · OQ51 (ตำแหน่งไม่ทราบแต่ไม่รีเซ็ต) · OQ52 (เวลา/นิยามท่าพัก) · OQ53 (แถบทับ body บังอะไร · ดักการกดตอนหลุด) · OQ54 (ไฟล์: ทางเข้าอื่น/popup หุ่นเดิมใหม่) · OQ55 (ชื่อ "หุ่น" ซ้ำ) · ร่างข้อความ R11/R14/R15/R16 อยู่ท้าย `feasibility/R5.md` หัวข้อ "รอบ 4" (ยังไม่แก้ requirements.md) · ผล feasibility คง "ทำได้มีเงื่อนไข" · สถานะ `draft`
- DS gap รอบนี้ (OQ34 + รอบ 2: popup แถบลอย 4 แบบ · ชิปแดง/เขียว/สถานะกลาง): popup สั่น + reduced-motion · ฉากหลังดักการกดเว้นแถบ N1/ปุ่มหยุด + Dialog persistent · ชิปไฮไลต์พร้อมป้ายการกระทำ
- Feasibility: **ทำได้มีเงื่อนไข** (ruler 2026-11-04 · ตรวจใหม่ R13/R15 ส่วนมือคีบ % และ R11/R16 ส่วนทางเข้าไฮไลต์ (OQ30) · R# อื่นยึดผล 2026-10-21 · ดู feasibility.md · เสี่ยงสูงสุด R16/ST-48 ความปลอดภัยหุ่น)
- OQ ของ D2 (2026-11-04): OQ25, OQ26, OQ28 answered · OQ27 เติม DS แล้ว 4 ข้อ (v11) ที่เหลือ (แถบความคืบหน้า, select/input, การ์ดไม่กดได้, มาสคอตท่าอื่น) ใช้ของเดิมใน DS
- OQ ที่ยังเปิด (เพิ่ม 2026-11-04: OQ29 ข้อ 1, OQ31, OQ32, OQ33, OQ34): OQ1, OQ4, OQ5, OQ6, OQ9, OQ10, OQ11, OQ12, OQ13, OQ14, OQ17, OQ18, OQ19, OQ21, OQ22 (เปิด 2026-11-04 · มือคีบ %) · answered: OQ2, OQ3, OQ7, OQ8, OQ15, OQ16, OQ20 (3 ข้อหลังตอบ 2026-10-21 และแก้ requirements R1, R10, R12, R14–R16 แล้ว) · OQ23, OQ24 (ตอบ 2026-11-04 · แก้ R13/R15 แล้ว) · **ไม่มีข้อที่ block ผล feasibility** · ต้องตอบก่อนส่ง dev: OQ1, OQ11, OQ12, OQ14, OQ18, OQ22 · ที่เหลือใช้ข้อสมมติ Proposed ออกแบบต่อได้
- การเปลี่ยนสถานะ: ตอนนี้ `approved` (ทั้ง 2 ที่) · session หลักเปลี่ยนสถานะ · แก้ requirements.md ต้องกลับ `draft` ตามกฎ
- Review: highlighter ตรวจ D1 รอบ 2026-11-04 (ข้ามขั้น `designed`) · **ผล: ยังมีข้อ "สูง" 1 ข้อ (F1 R15 ST-23 ไม่มี UI เตือนก้าวไกล · ไม่ได้เกิดจาก D1) + กลาง 5 + ต่ำ 7** · สถานะคง `approved` (ไม่เปลี่ยนเป็น `reviewed`) · ดู review.md · รอบ 2026-10-21 นำเข้าผล Auditor เดิม RETURN: AUD-F01 สูง
- ข้ามขั้น: 2026-11-04 ส่ง highlighter ตรวจ D1 (R13/R15 มือคีบ) ทั้งที่สถานะยังเป็น `approved` (ยังไม่ `designed` เพราะมี D# เฉพาะ R13/R15) · ผู้ใช้สั่งให้ตรวจ
