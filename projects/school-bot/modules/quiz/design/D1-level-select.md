---
module: quiz
design: D1
covers: [R12, R1, R6, R8, R10, R11, R17]
canvas: C1
updated: 2026-11-09
---

# D1 หน้าเลือก Level (6 ใบ)

- **ทำใหม่ 2026-11-09 (รอบ 2 · ไฟล์ในเครื่องรอบแรกหายก่อน publish · สร้างใหม่ทับไฟล์สด C1 v789 `1794207717-f577` ตามรายการ "แก้ 2026-11-09" ด้านล่าง) · ยังไม่ publish (C1 shared · agent ไม่มี AskUserQuestion รออนุมัติจาก session หลัก):** ไฟล์ที่แก้ `…/scratchpad/artifact-files/4f330c07-5a09-4cc5-82c9-425fd97916ea/project/QuizLevelsV1.dc.html` · **สำเนาชั่วคราวกันหายใน sketchbook (ลบหลัง publish):** `design/src/QuizLevelsV1.dc.html` · **DS ที่ใช้:** School Bot Studio Design System **v24** (version id `1794197914-a9c2` · read 2026-11-09) · C1 มี `ds/school-bot/bundle.css`, `bundle.js`, `tokens.css` จาก v24 แล้ว (ไม่ต้องส่งซ้ำ) · ไฟล์เพิ่ม `<script src="ds/school-bot/bundle.js">` + `tokens.css` + `bundle.css` · root ใส่ `class="sb-root"` · ลบ CSS `.sb-*`/`.sb-i-*` ที่ตกค้างจาก HomeRail ออก (SidebarN3 มี `.sbn-*` ของตัวเองครบ) · สี/ขนาด/ระยะ/ขอบ ที่แตะใช้ `var(--token)` ของ DS ทั้งหมด · ไอคอนใหม่ใช้ `window.SchoolBot.icons` ผ่าน mask (`lock` `check` `rotate-ccw` `triangle-alert` `circle-alert`)
  - **ความคืบหน้าบนการ์ด (R12 · OQ55):** ไม่เคยเล่น = ไม่แสดงตัวเลข (การ์ดเปิด = ข้อความ "ยังไม่เริ่ม" · ไม่มีดาว ไม่มีแถบ) · เคยเล่น = "ผ่าน x/44 ภารกิจ" (นับทุกด่านรวมเกม) + ดาว + แถบ ทั้งการ์ดเปิดและการ์ดล็อก (ดาวรวมในหัวหน้านับ level ที่ล็อกด้วย · OQ52)
  - **การ์ดล็อก (R7):** ใช้แบบ DS Card สถานะปิดใช้ (`aria-disabled` พื้น `off-bg` ขอบ `border` ไม่นูน ตัว `text-secondary` ไม่มี hover/ยก) + ไอคอน `lock` + **เหตุผลบนการ์ดเสมอ ไม่ต้องแตะ** (H5) · เหตุผลแยก 4 แบบ (OQ56/ST-11): สูงกว่าชั้นตามปกติ "Level n สำหรับ ป.n" (ไม่ชวนติดต่อครู) · ครูลดสิทธิ์ (level ≤ ชั้นแต่ > N) "ติดต่อครูเพื่อปลดล็อก" · ไม่รู้ชั้น (state `unknownGrade`) · โหลดสิทธิ์ไม่ได้ (state `accessFail`) · "เล่นล่าสุด" ไม่ขึ้นบนการ์ดล็อก · **ตัดป้าย "ชั้นของฉัน" ออก** (R12/OQ41 ที่ D1 เดิมยังมี) และขอบเน้นการ์ดชั้นตัวเอง · ตัดข้อความ "เข้าได้ทุกใบ" ในหัวหน้า
  - **Skeleton (R8):** state `loading` ใช้ DS `Skeleton` (`sb-skel-card` + `sb-skel-line` + `sb-skel-block`) แทนกล่อง skeleton เดิม · ไม่มี spinner ซ้อน (DS: ห้าม spinner เมื่อรู้รูปทรง) · `role=status aria-busy` + ข้อความ `sb-sr` "กำลังโหลดบทเรียน…" ครั้งเดียว
  - **สถานะใหม่ (Tweak `state` = normal · first · loading · progressFail · accessFail · unknownGrade · sessionExpired · offline):** `accessFail` โหลดสิทธิ์ไม่ได้ = ล็อกทุกใบ (เหตุผลบนการ์ด "ยังโหลดสิทธิ์ไม่ได้ กด ลองอีกครั้ง ด้านบน") + DS Notice error "ยังโหลดสิทธิ์การเรียนไม่ได้" + ปุ่ม "ลองอีกครั้ง" (OQ43 · ความคืบหน้าที่เคยเล่นยังแสดง) · `unknownGrade` ไม่รู้ชั้น = เปิดแค่ Level 1 ที่เหลือล็อก "ยังไม่รู้ว่าเธอเรียนชั้นไหน" + DS Notice warning (ถ้อยคำ guest รอ app-shell แผน 4 · OQ61) · `sessionExpired` = DS Notice warning "ล็อกอินหมดอายุแล้ว · ผลที่เล่นไว้เก็บอยู่ในเครื่อง ไม่หาย" + ปุ่ม "เข้าสู่ระบบใหม่" (ปุ่มจำลอง ยังไม่ลิงก์ไปหน้า login ของ app-shell) · การ์ดเล่นต่อได้ปกติ (R8) · `progressFail` = DS Notice warning + ปุ่ม "ลองอีกครั้ง" · การ์ดเปิดแสดง "ผ่าน –/44 ภารกิจ" + ดาว "–" ไม่แสดงแถบ/ไม่แสดงดาวรวม/ไม่แสดง "เล่นล่าสุด" · การ์ดล็อกไม่แสดงตัวเลข (ไม่รู้ว่าเคยเล่นไหม) · Tweak `teacherN` (ครูปรับ N · 0 = ไม่ได้ปรับ · ต่ำกว่าชั้น = การ์ดล็อกแบบ "ติดต่อครูเพื่อปลดล็อก") · `myGrade` 1–6 (ไม่รู้ชั้นใช้ state `unknownGrade`) · `soon` (เร็ว ๆ นี้ Level 5–6 ที่เปิดอยู่)
  - **ตัวอย่างข้อมูล:** Level 1 จบแล้ว 44/44 · Level 2 12/44 · Level 3 และ 5, 6 ยังไม่เคยเล่น · Level 4 18/44 (ตั้ง `teacherN` = 3 จะเห็นการ์ดล็อกที่ยังแสดงผ่าน 18/44 + 44 ดาว) · ดาวรวมนับ level ที่ล็อกด้วย (OQ52) · "เล่นล่าสุด" = Level 2 เฉพาะเมื่อไม่ล็อก (R12: ไม่ชี้ไป level ล็อก)
  - **ST-14:** หน้านี้ไม่มีพฤติกรรมออก/ทำต่อ · ออกกลางด่านแล้วเข้าใหม่เริ่มข้อแรกและไม่ทิ้งร่องรอยบนการ์ด (ไม่มี "ทำต่อ") · "เคยเล่น" = มีผลจบด่านที่บันทึกแล้วอย่างน้อย 1 ด่าน (R12) ผ่าน 0/44 + 0 ดาว แสดงได้ถ้าเคยเล่นแต่ยังไม่ผ่าน
  - **OQ57:** เพิ่ม N มีผลเมื่อเปิดหน้านี้ครั้งถัดไปขณะออนไลน์ · ลด N มีผล login ถัดไป = พฤติกรรมของระบบ ไม่มี UI เพิ่ม (ข้อความหลังบันทึกอยู่ที่ teacher-web)
  - **DS gap:** ไม่มี DS gap ใหม่ (Skeleton, Notice, Button, Card ปิดใช้ มีใน DS) · ค่าเดิมของ D1 ที่ยังไม่มาจาก DS คงไว้ ไม่แตะ: สี accent level 1–6 (`level-1..6` = G3-3/G4 รอ · ใช้ที่จุดบน LEVEL badge), แถบความคืบหน้า `q-bar` (DS ไม่มีแถบ progress · ใช้ token `border`/`action-primary`/`success`/`radius-pill`), ภาพเกาะ (G4), การ์ด Level เปิด `q-card` ที่มี hover ยก (DS Card ไม่มี hover ยก), สีดาวเต็ม `#F2C94C` (DS ไม่มี `star-fill` · ขอบดาวใช้ `warning-strong`), ไอคอนนาฬิกาในกล่อง "เร็ว ๆ นี้" (DS ไม่มีไอคอน clock · `.q-i-clock` เดิม)
  - **ยังไม่ได้ตรวจ:** render จริงทั้งหมด (agent ไม่มี browser) รวมไอคอน SVG ใน `<sc-if>` · `<a>` การ์ดล็อกไม่มี `href` (ต้องดูว่า dc runtime ตัด attribute ที่เป็น undefined จริง) · `.sb-card[aria-disabled]` บนแท็ก `<a>`

- **Artboard:** `QuizLevelsV1.dc.html` (1440×900 · แถบหน้าต่าง 60 + พื้นที่ 840 · มี sidebar มาตรฐาน เลือก "บทเรียน") ใน canvas C1 · ปลายทางลิงก์ไป `QuizMapV1.dc.html` (D2)
- **แก้ sidebar 2026-11-02 (ผู้ใช้สั่ง · งานของ app-shell ที่ทำผ่าน quiz):** ใน Play เมนู sidebar ต้องคลิก 2 ครั้ง เพราะลิงก์ข้าม artboard อยู่ใน `dc-import` child (`HomeRail`) → ย้าย markup sidebar ทั้งชุด (แถบ 104 · แถบกาง 264 · เมนูโปรไฟล์) เข้าไปในแต่ละ frame: `HomeV6A` · `MyWorkV1` · `MyWorkV1Block` · `QuizLevelsV1` · ลิงก์เมนูเป็น `<a href="X.dc.html">` แบบ literal (หน้าหลัก → HomeV6A · บทเรียน → QuizLevelsV1 · Block Lab → MyWorkV1Block · Arm Lab → MyWorkV1) · class `on`/`aria-current` มาจาก `sbVals(sel)` ใน script ของ frame (state กาง/โปรไฟล์/ภาษา + Esc อยู่ใน frame) · หน้าตา/ขนาดเดิมทุกค่า · `MyWorkV1Block` เปลี่ยนจาก import ทั้งหน้าเป็นสำเนาเต็มของ MyWorkV1 (Tweak `lab` ค่าเริ่ม block · แก้ MyWorkV1 ต้องแก้ไฟล์นี้ตาม) · `HomeRail` เหลือเป็นต้นแบบ (ไม่มีใคร import) · QuizLevelsV1 เติม CSS `.sb-mi.danger` และ reduced-motion ของ `.sb-nav:active/.sb-btn:active` (ไอคอน globe/gear/lock/star/dots/l มีครบแล้ว · medal ไม่ได้ใช้ใน sidebar) · ปุ่ม hero ของ HomeV6A: ครั้งแรก "เริ่มด่านแรก" → `QuizLevelsV1` · "เรียนต่อ"/"ไปหน่วย 4" → `QuizMapV1` (ข้อสมมติตาม app-shell R7 "ปุ่มเรียนต่อ → บทเรียน" + "เรียนต่อไป level ล่าสุด") · **ยังไม่ publish:** publish ถูกปฏิเสธเพราะมีคนแก้ `canvas.json` ของ C1 ระหว่างทำ (version 1793595082-7c21) รอ session หลักตัดสินว่าจะ publish ใหม่ · `LearnMapV1.dc.html` ไม่มีใน C1 แล้ว (version 1793595048-dec8) จึงไม่ได้แก้
- **Publish:** publish แล้ว 2026-11-01 บน C1 (version 708 · ผู้ใช้อนุมัติ) · artboard `QuizLevelsV1.dc.html` · https://claude.ai/artifact/AnEWv6UNbgcNvUXS1sfHQd · ยังไม่ได้ตรวจ render จริง · ไม่เก็บ HTML ใน sketchbook · **แก้ 2026-11-01 (ผู้ใช้ขอใช้ภาพจริงจากโฟลเดอร์ ref):** ภาพเกาะบนการ์ดเปลี่ยนจากเวกเตอร์เป็นภาพเกาะ 6 ใบที่ตัดจาก `assets/ref/Quiz/Start Page.png` (200×176 พื้นขาว · asset ของ C1 · ค่า `img` ต่อ level ใน renderVals) publish C1 version 713 · เปิดตรวจบน canvas แล้ว: แสดงครบ 6 ใบ · ข้อสังเกต: ภาพเกาะเล็กกว่าในภาพอ้างอิง (ราว 140×124) เพราะภาพตัดจากหน้าจอขนาดเล็ก ถ้าต้องการใหญ่ขึ้นต้องได้ไฟล์ภาพเกาะต้นฉบับ (OQ19) · พื้นภาพเป็นสีขาวทึบ ใช้ได้เฉพาะบนการ์ดพื้นขาว · **รอบ 2 publish แล้ว C1 v791 (2026-11-09 · ผู้ใช้อนุมัติ · id `1794209576-10fb`) · ยังไม่ได้ตรวจ render จริง** · **2026-11-09 แก้บรรทัดรอง unknownGrade เป็น "ดูแผนที่ได้ แต่ยังเริ่มภารกิจไม่ได้นะ" (ตรง R7 และ D2 · ผู้ใช้ตัดสิน) publish แล้ว C1 v793 (id `1794210094-49da`)**
- **ภาพอ้างอิง:** `Start Page.png` (ตัด Arm Lab และปุ่ม "เพิ่มท่า" ออก) · ภาพเกาะวาดใหม่เป็นเวกเตอร์ placeholder (ไม่ฝังบิตแมป) · ชื่อเกาะ/ระดับเป็นตัวอย่างสมมติ (OQ19)

## สิ่งที่ออกแบบ
- หัวหน้า "บทเรียน" 28/700 + คำอธิบาย + ชิป "ดาวรวม" · การ์ด 3×2 gap 24 (กว้างหดตามพื้นที่ · สูงต่ำสุด 340) · เลื่อนเฉพาะ `main` เมื่อข้อความยาว (+40%)
- การ์ด Level: ป้าย LEVEL n (จุดสี accent + ข้อความ) · ป.n · ภาพเกาะ · ชื่อ 20/700 · คำอธิบาย 16 · ความคืบหน้า "ผ่าน x/44 ภารกิจ" + แถบ + ★ ดาวรวมของ level (เฉพาะที่เคยเล่น · ยังไม่เคยเล่น = "ยังไม่เริ่ม") · การ์ดเปิดแตะเข้าได้ (ลิงก์ไปแผนที่) · การ์ดล็อกแตะไม่ได้ เหตุผลอยู่บนการ์ด
- ป้าย "เล่นล่าสุด" (Level 2 ในตัวอย่าง · ไม่ขึ้นบนการ์ดล็อก) เพื่อให้กลับไปต่อได้เร็ว · **ไม่มีป้าย "ชั้นของฉัน" แล้ว (R12/OQ41)**
- **สถานะ (Tweaks):** ดูหัวข้อ "สถานะใหม่" ด้านบน · `loading` = DS Skeleton ไม่ใช่ 0/0 · `offline` = ชิปบนแถบหน้าต่าง · `soon` = Level 5–6 "เร็ว ๆ นี้" ที่เปิดอยู่ แตะแล้วขยายคำอธิบายในการ์ด (OQ27 Proposed ไม่เงียบ) · Level 1 ตัวอย่างแสดง "จบแล้ว" (ไอคอน check + ข้อความ + แถบเขียว)
- ภาษา: Tweak `lang` ไทย/EN/中文 (ฟอนต์ fallback IBM Plex Sans SC)

## ค่าที่ใช้
- โทเค็น brand: `background #F4F7FB` · `surface #FFFFFF` · `border #DCE3EC` · `text-primary #14243D` · `text-secondary #5A6377` · `action-primary #1866C9` / `-dark #0F4C99` / `-subtle #EAF2FD` · `success #2E7D32` · `warning-bg #FFF4CC` + `warning-strong #B07F00` (ชิปออฟไลน์/แถบเตือน) · radius-lg 16 · radius-md 12 · border-default 2px · ปุ่มนูน ขอบล่าง 4px · shadow-float · focus ring 3px `#1866C9` offset 2 (เฉพาะ :focus-visible) · spacing 4/8/12/16/24/32 · type 14/16/18/20/28
- **ค่าชั่วคราว (ไม่อยู่ใน brand §1):** สีดาวเต็ม `#F2C94C` + ขอบ `#B07F00` (ดาวว่างไม่ได้ใช้ในหน้านี้) · สี accent ต่อ level (จุด/เกาะ เท่านั้น ไม่ใช่ปุ่ม/สถานะ): L1 `#5BC98A` L2 `#5AA9F5` L3 `#F5B97A` L4 `#73B8FF` L5 `#FF7B5C` L6 `#C03BF0` · สีภาพเกาะ placeholder (rock/top/rim/decor) ต่อ level · แถบหน้าต่าง 60 เป็น stand-in (รอ `WindowBarV1` ฉบับ 60 · CR-09) → OQ33 / OQ35

## Heuristics / UD
- H1 สถานะระบบ (loading skeleton, progressFail ไม่หลอกว่า 0) · H2 ภาษาเด็ก "ผ่าน 12/44 ภารกิจ" · H3 ทางกลับ (sidebar) · H4 คำเดียว "ภารกิจ" ทั้งหน้า (OQ30) · H5 การ์ด "เร็ว ๆ นี้" อธิบาย ไม่ปล่อยเงียบ · H6 จำง่าย (ป้ายเล่นล่าสุด/ชั้นของฉัน) · H9 ข้อความ error บอกว่าข้อมูลไม่ได้หาย
- UD: สถานะไม่ใช้สีอย่างเดียว (จบแล้ว = ไอคอน+ข้อความ · accent เป็นของตกแต่ง ตัวบอก level = ข้อความ "LEVEL n")

## WCAG AA (ตรวจด้วยมือ)
- text-primary บน surface 14.5:1 · text-secondary บน surface ≈6.1:1 · `#0F4C99` บน `#EAF2FD` ≈7.5:1 · success บนขาว 5.1:1 · focus ring บนขาว 5.6:1
- เป้ากด: การ์ดทั้งใบ · ปุ่มแถบเตือน 48 · ปุ่มหน้าต่าง 48×44 · ตัวอักษรใน control/เนื้อหา ≥16 (ข้อมูลรอง 14 = ป้าย LEVEL/ป.n/ป้ายชั้นของฉัน)
- role=link/button ตามกรณี · aria-label รวมชื่อ level + ความคืบหน้า + ดาว · reduced-motion: ปิด transition/spinner (เหลือวงนิ่ง) · ไม่กะพริบ
- **ยังไม่ได้ตรวจ:** render จริง/ภาพหน้าจอ · ความยาวข้อความ EN/中文 ในการ์ด (ออกแบบเผื่อ +40% ด้วยการ์ดสูงยืดและ `main` เลื่อนได้) · screen reader จริง

## ค่าจาก DS ที่ใช้เพิ่มรอบ 2026-11-09 (ชื่อ token/component · ค่า)
| ส่วน | DS |
|---|---|
| Skeleton | `sb-skel-card` (`radius-lg` · `border-default` `border` · `surface` · padding `space-4`) · `sb-skel-line` (สูง `space-4` · `radius-sm` · `off-bg` · `border-thin`) · `sb-skel-block` (`off-bg` · `radius-md` · padding `space-8`) · `sb-skel` gap `space-2` |
| Notice | `sb-notice` + `-warning` (`warning-bg` · `warning-strong`) · `-error` (`danger`) · ไอคอน `triangle-alert` / `circle-alert` ขนาด `icon-lg` 24 |
| ปุ่ม | `sb-btn sb-btn-secondary` สูง `control-md` 48 · ไอคอน `rotate-ccw` `icon-md` |
| การ์ดล็อก | Card ปิดใช้: `off-bg` · `border` · `border-default` ล่าง (ไม่นูน) · `text-secondary` · แผ่นภาพเกาะ `surface` + `border-thin` + `radius-md` · เหตุผล `text-primary` 16/600 + `lock` `icon-md` · gap `space-2` |
| ตัวหนังสือ | `text-md` 16 · `lh-body` |

## H / UD / WCAG ที่เพิ่ม
- H1 skeleton ไม่หลอกว่า 0 และไม่ล็อกก่อนข้อมูลมา · H5 เหตุผลล็อกอยู่บนการ์ดเสมอ แยก 4 แบบ ไม่ชวนติดต่อครูเมื่อสูงกว่าชั้นปกติ · H9 ข้อความ error บอกว่าผลไม่หาย
- UD: สถานะล็อก = ไอคอน + ข้อความ + พื้น/ขอบต่าง (ไม่พึ่งสีอย่างเดียว) · การ์ดล็อก `role=button aria-disabled tabindex=0` โฟกัสด้วยคีย์บอร์ดแล้วอ่านเหตุผลได้
- WCAG (คำนวณมือจากค่า DS): `text-primary` บน `off-bg` ≈ 13.3:1 · `text-secondary` บน `off-bg` 5.56:1 (ชื่อ/คำอธิบายบนการ์ดล็อก) · ไอคอน `warning-strong` บน `warning-bg` 3.24:1 (กราฟิก ≥3:1 คู่ข้อความ) · เป้ากด: ปุ่มลองอีกครั้ง 48 · ยังไม่ได้วัดจริง

## ข้อเสนอแนะ
- ใช้คำ "ภารกิจ" ทั้ง UI (แทน "ด่าน") เพื่อให้ตรงกับแผงภารกิจ (OQ30) · ภาพเกาะจริง/ชื่อเกาะจริงรอ OQ19 · ตัวเลข "x/44" มาจาก manifest (ไม่ fix 44 · OQ18)
