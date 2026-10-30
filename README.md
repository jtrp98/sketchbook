# Sketchbook

ที่เก็บ requirement, design และเอกสารส่งมอบงาน UX/UI ของทุกโปรเจกต์ในบริษัท ทำงานร่วมกับ Claude Code ผ่านชุดเครื่องมือ **Pencil Case**: ผู้ช่วย 4 ตัวที่พางานจากความต้องการไปจนถึง handoff ให้ dev

กฎทั้งหมดที่ Claude ใช้อยู่ใน [CLAUDE.md](CLAUDE.md) ไฟล์นี้เป็นคู่มือสำหรับคนในทีม

## Pencil Case

| เครื่องมือ | Role | ทำอะไร | เรียกใช้ |
|---|---|---|---|
| ✏️ `pencil` | Requirement | ถามเค้นความต้องการจนครบ แล้วจดเป็น R# | พิมพ์ `/pencil <โปรเจกต์>/<module>` |
| 📏 `ruler` | Feasibility | ตรวจว่า requirement ทำเป็น UI ได้จริงไหม ชี้ช่องโหว่และ edge case | พูดว่า "ตรวจว่าทำได้ไหม" |
| 🖍️ `crayon` | Designer | ออกแบบหน้าจอบน Design canvas (Artifact) ตาม WCAG AA | พูดว่า "ออกแบบ ..." |
| 🖊️ `highlighter` | Reviewer | ตรวจ design, a11y, ความถูกต้องของเอกสาร และทำ handoff spec | พูดว่า "ตรวจ ..." หรือ "ทำ handoff" |

ไม่ต้องจำชื่อ agent พูดตามปกติได้เลย Claude จะเลือกเครื่องมือให้เอง ระบุแค่ **โปรเจกต์** และ **module** ทุกครั้ง

## ลำดับงาน

```
pencil ──► ruler ──► crayon ──► highlighter ──► dev
 draft    approved   designed    reviewed       built
```

| สถานะ | แปลว่า | ขั้นต่อไป |
|---|---|---|
| `draft` | จด requirement แล้ว | ให้ `ruler` ตรวจ |
| `approved` | ทำได้ และคุณยืนยันแล้ว | ให้ `crayon` ออกแบบ |
| `designed` | ทุก R# มี design แล้ว | ให้ `highlighter` ตรวจ |
| `reviewed` | ไม่มีปัญหาระดับ "สูง" ค้าง | ทำ handoff ส่ง dev |
| `built` | dev ทำเสร็จ (บอก Claude เอง) | - |

ถ้าแก้ requirement หลัง `approved` สถานะจะกลับเป็น `draft` และต้องให้ `ruler` ตรวจใหม่

## เริ่มใช้งาน

1. clone repo แล้วเปิดโฟลเดอร์ใน Claude Code (desktop app แท็บ Code หรือ CLI)
   ```bash
   git clone https://github.com/jtrp98/sketchbook.git
   ```
2. เริ่ม module ใหม่ด้วย `/pencil <โปรเจกต์>/<module>` เช่น `/pencil school-bot/login`
   - โปรเจกต์หรือ module ที่ยังไม่มี Claude จะสร้างจากแม่แบบใน `projects/_template/` ให้
3. ตอบคำถามจน requirement ครบ แล้วสั่งงานต่อตามลำดับ เช่น
   - "ตรวจ school-bot/login ว่าทำได้ไหม"
   - "ออกแบบ school-bot/login"
   - "review school-bot/login" แล้ว "ทำ handoff school-bot/login"
4. commit และ push ไฟล์ที่เปลี่ยนทุกครั้งที่จบงาน เพื่อให้ทีมเห็นสถานะล่าสุด

## Canvas (ที่วาง design)

design จริงอยู่บน Design canvas (Artifact บน claude.ai) repo นี้เก็บแค่ลิงก์และสรุป ไม่เก็บ HTML ของ canvas

- 1 module มีได้หลาย canvas ลงทะเบียนเป็น C# ในตาราง Canvas ของ `INDEX.md` ของ module
- ก่อนออกแบบ, review หรือ handoff ถ้ายังไม่มี canvas Claude จะถามทุกครั้งว่าจะใช้ artifact ที่มีอยู่ (ส่งลิงก์ให้) หรือสร้างใหม่
- canvas ที่แชร์ทั้งองค์กร Claude จะรอให้คุณอนุมัติก่อน publish ทุกครั้ง

## โครงสร้าง

```
sketchbook/
├── CLAUDE.md                 กฎที่ Claude ใช้ (แก้ที่นี่ที่เดียว)
├── knowledge/                ความรู้กลาง: brand, tokens, WCAG, components, heuristics
├── projects/
│   ├── _template/            แม่แบบโปรเจกต์และ module
│   └── <โปรเจกต์>/
│       ├── INDEX.md          สารบัญ: module ทั้งหมดและสถานะ
│       ├── CHANGELOG.md      ประวัติการเปลี่ยน requirement
│       ├── archive/          ของเก่า
│       └── modules/<module>/
│           ├── INDEX.md      สถานะ, canvas, ตาราง R → D → OQ
│           ├── requirements.md   R#
│           ├── oq.md             คำถามที่ยังไม่ตัดสิน (OQ#)
│           ├── feasibility.md    ผลตรวจของ ruler
│           ├── review.md         ผลตรวจของ highlighter
│           ├── handoff.md        spec สำหรับ dev
│           └── design/D<n>-<ชื่อ>.md
└── .claude/
    ├── agents/               ruler, crayon, highlighter
    └── commands/             pencil
```

## ID ที่ใช้

| ID | คือ | ตัวอย่าง |
|---|---|---|
| R# | requirement | R1 ผู้ใช้ login ด้วยเบอร์โทรได้ |
| OQ# | คำถามที่ยังไม่ตัดสิน | OQ2 ลืมรหัสผ่านต้องส่ง OTP ไหม |
| D# | design | D1-login-form |
| C# | canvas ของ module | C1 Login screens |

ID ไม่ใช้ซ้ำ แม้ลบไปแล้ว

## เพิ่มความรู้กลาง

เพิ่มไฟล์ใน `knowledge/` (เช่น `brand.md`, `design-tokens.md`) แล้วอัปเดตตารางใน [knowledge/README.md](knowledge/README.md) ทุก agent จะใช้ทันที ถ้าไฟล์ไหนยังไม่มี agent จะใช้มาตรฐานทั่วไปและระบุในงานว่า "ยังไม่มีเกณฑ์ของทีม"
