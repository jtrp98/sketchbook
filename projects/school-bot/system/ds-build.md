---
project: school-bot
updated: 2026-11-04
scope: สรุปการเติมเนื้อหา Design System artifact (รอบที่ 3 · ไม่ใช่งานของ module · ไม่มี D#)
---

# DS build: School Bot Studio

DS: https://claude.ai/artifact/DgwzCEnxThrSoxnE5ZrNoy · version ที่ publish ล่าสุด **10** (id `1793758139-d06d`) · อ่านอย่างเดียว ไม่ได้ render หรือทดสอบคีย์บอร์ด/ผู้อ่านจอ (คอนทราสต์คำนวณมือ) · **ยังไม่ยืนยันว่า preview เป็น live แล้ว (ต้องให้ผู้ใช้เปิดดู)**

## ทำแล้ว

- `tokens.json` (theme light เดียว): สี 31 ตัว · type (IBM Plex Sans Thai ผ่าน Google) · spacing · radius · shadow · borderWidth · size · zIndex · duration · easing · lineHeight
- `README.md` brand book ภาษาไทย · `components/bundle.css` (คลาส `sb-*`), `bundle.js` (ไอคอน Lucide ~35 + hydrate + ตัวช่วย Button / DeviceStatus / Dialog), `index.d.ts`
- components (README + preview): WindowBar, Sidebar, Button, DeviceStatus, JobName, Tab, Card, Tooltip, Popover, Dialog, Toast, EmptyState, Focus, Cover
- asset: มาสคอต 10 ท่า · โลโก้ Block Lab + **Arm Lab (ไฟล์จริง รอบ 3)**

## ตัดสินแล้ว (ผู้ใช้ 2026-11-04 · ci-audit §7.4 · ย้ายออกจากค่าชั่วคราว)

- sidebar กว้าง 120 · พื้น `background` #F4F7FB · รายการที่เลือกพื้นขาว + เงาเบา
- focus ด้านในเฉพาะรายการนำทาง · การ์ดขอบ 3px ใช้วงนอก offset 2
- สถานะเตือนอุปกรณ์ = ไอคอน `warning-strong` + ข้อความ `text-primary`
- ปุ่มหยุด = มุมซ้ายล่างของแผงเล่น (แบบ Arm Lab) · ฉากหลัง dialog lab เว้นตำแหน่งนี้ (`sb-scrim-lab` ตัดมุม ไม่ใช่แค่ยก z)
- ไอคอนหุ่น (แขน/gripper/ข้อต่อ/ท่าชุด/USB): ใช้ชุดปัจจุบัน (bot/plug)
- โลโก้บนแถบ = School Bot (ไม่มี Studio) · ชื่อผลิตภัณฑ์ในข้อความยังเป็น School Bot Studio

## ค่าชั่วคราวที่เหลือ (ต้องให้ผู้ใช้ตัดสิน)

1. สี avatar/ปุ่มภาษาใน sidebar: `action-primary-subtle`
2. ขนาดโลโก้บนแถบ: สูง 32
3. `stop-dark` #8E1B1B (DSG-12) รอ approve · ขอบล่างปุ่ม danger ยืมค่านี้
4. `shadow-toast` geometry ยืมจาก shadow-float · ระยะ toast จากขอบล่างยังไม่ตัดสิน
5. hover ของปุ่ม/การ์ด: วง `focus-halo` (ปุ่มรองเพิ่มขอบ action-primary)
6. spinner: วงมีขอบแบบ Quiz · reduced-motion = ไม่หมุน
7. padding แถบบน: ปุ่มหน้าต่างชิดขอบขวา · ชื่อหน้า N2 16/600 text-secondary · line-height `display-countdown` 1.3 · ชั้นของแถบหน้าต่าง (CR-10)
8. ขนาดพื้นที่เว้นปุ่มหยุดใน `sb-scrim-lab` 232 x 88 (คำนวณจากปุ่มใน preview)
9. fallback ฟอนต์ไทย (`Leelawadee UI`, `Tahoma`) · IBM Plex Sans SC (zh) ยังไม่ได้ใส่

## ยังรอ

- ที่ว่างปุ่มระบบ Mac 76 (`mac-controls-width`): คงไว้ รอภาพอ้างอิงจากผู้ใช้
- โลโก้ School Bot: `School Bot.svg` (520 KB) เป็น PNG ฝังใน SVG (`<image>` + pattern) ตอนอัปโหลดเข้า DS ระบบตัดภาพฝังออก เหลือ 542 ไบต์ภาพว่าง จึงไม่ได้ลงทะเบียน (ลบแล้ว) · preview ใช้ตัวอักษร "School Bot" ในกรอบเส้นประ · ต้องการ SVG เวกเตอร์ (path) หรือ PNG พื้นโปร่ง · Cover ไม่มีกล่องโลโก้ (มีแต่ชื่อผลิตภัณฑ์ตัวอักษร) จึงไม่ได้แก้
- ไฟล์ฟอนต์ IBM Plex Sans Thai (OFL) สำหรับฝังในโปรแกรม

## ปัญหา "Previews can't run: components/bundle.js is missing" (แก้ใน v10 · ยังไม่ยืนยัน)

- สาเหตุที่พบจากโค้ด `artifact-type/app.js`: หน้าถือว่ามี bundle ก็ต่อเมื่อ header `@ds-bundle` ประกาศ `components` อย่างน้อย 1 ชื่อ (`s=r.length>0&&files.includes(bundleJs)`) ของเดิมเป็น `"components":[]` จึงอ่าน bundle.js เป็น null ทั้งที่มีไฟล์ และมีโฟลเดอร์ component จึงขึ้นข้อความ missing แล้ว preview เป็น static ไม่มี tokens.css/bundle.css
- แก้: header ประกาศ Button, DeviceStatus, Dialog และ `bundle.js` ส่งออกฟังก์ชันจริง 3 ตัว (คืน HTML string ใช้คลาส `sb-*`) + `index.d.ts`
- ยังไม่ได้ยืนยัน: การ render จริง (ไม่มีเครื่องมือ render) · ไม่ได้เพิ่ม React/`libraries`/manifest.json (ไม่จำเป็นตามที่ตรวจ ยังไม่ยืนยัน)

## ข้อสังเกตคอนทราสต์ที่ไม่ผ่านตามต้นทาง (คงไว้)

- `border` (1.3:1) และ `border-strong` (1.48:1) บนขาวไม่ถึง 3:1 · toast 14/13px และปุ่ม 32 ต่ำกว่า ≥16/44 (ข้อยกเว้นที่ผู้ใช้อนุมัติ)
- ข้อความ `text-secondary` บน `background` (sidebar ใหม่) 5.61:1 ผ่าน · `action-primary` บน `background` 5.17:1 ผ่าน

## ยังไม่ได้ทำ

- ชิปมีกรอบ · ช่องกรอก/ค้นหา · การ์ดคำถาม/ด่าน Quiz · ตารางเว็บครู · wizard · ชุดควบคุมพื้นที่ต่อบล็อก · แผงลอย/บล็อก/terminal/ตัวแก้โค้ด Block Lab · Attention Ring (มีกฎ ไม่มี preview) · แถบข้อมูลในหน้า
- ไม่ได้ render ตรวจภาพ · ไม่ได้ทดสอบคีย์บอร์ด/ผู้อ่านจอ · ไม่ได้แตะ INDEX/CHANGELOG ของโปรเจกต์

## เติมตามคำอนุมัติของผู้ใช้ 2026-11-04 (OQ25–OQ27 · หน้าเชื่อมต่อหุ่น · DS เวอร์ชัน 11)

ผู้ใช้อนุมัติ 4 ข้อ (เติมเฉพาะข้อที่บล็อก) ใช้เฉพาะ token ที่มีแล้ว ไม่มี Hex ใหม่:
- `z-windowbar` = 65 (ต่ำกว่า `z-stop` 70, สูงกว่า `z-bottombar` 60 · แก้ CR-10/AUD-F01) · tokens.json + README §12 ข้อ 12
- `sb-actionbar` แถบปุ่มล่าง: พื้น `surface` ขอบบน `border-default` สี `border` · padding `space-4`/`space-6` · `z-bottombar` · [หยุด ซ้ายสุด] … [รอง][หลัก] · gap `space-3` · ปุ่มสูง `control-lg` (56)
- `sb-notice` กล่องสถานะ: info (`action-primary-subtle` + `border-strong`) · warning (`warning-bg` + `warning-strong`) · error (พื้น `surface` ขอบ+ไอคอน `danger`) · success (ขอบ+ไอคอน `success`)
- `sb-check` checkbox: กล่อง `icon-lg` (24) `radius-sm` · ติ๊ก = `action-primary` + เครื่องหมายถูก `text-on-dark` · แถวสูงไม่ต่ำกว่า `control-sm` (44)
- ยังไม่เติม (ใช้ของเดิมใน DS ไปก่อน): แถบความคืบหน้า, select/input นอกชื่องาน, การ์ดข้อมูลไม่กดได้, มาสคอตท่าอื่น
- ยังไม่ได้ทำ: preview.html / README ของ component ใหม่ 3 ตัว · ยังไม่ได้ render ตรวจ · ไม่ได้อัปเดต `design-system.json` (lastChange)
