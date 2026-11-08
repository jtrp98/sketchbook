# Learning Game Design Library — School Bot (v0.1, from G1 Unit 3)

Legend: **[E]** = evidence from source file · **[R]** = design recommendation (not a school requirement)

## 1. Project Context
School Bot curriculum, ป.1 Unit 3 "AI Around Me" (1 period, 50 min). First game of a reusable system (target: 40+ lessons × 6 grades). Code: `src/game/` (types → content → mechanics → shell).

## 2. Source Material Inventory
| ID | File | Class | Relation to Unit 3 | Inspected |
|---|---|---|---|---|
| S1 | Lesson Plan ป.1 — Unit 3 AI Around Me.pdf | Lesson Plan | Source of truth | Text, full |
| S2 | AI Hidden Hunt.pdf (1 p.) | Student Worksheet | **Unit 3** (finding AI in daily life) | Text + rendered page |
| S3 | AI Puzzle.pdf (1 p.) | Student Worksheet | Other unit (Input→Process→Output) | Text + rendered page |
| S4 | My Dream Robot.pdf (1 p.) | Student Worksheet | Other unit (Sensor/Motor, says "after learning Sensor & Motor") | Text + rendered page |
| S5 | image.png — Teachable Machine "How do I use it?" | Supporting (external web) | Not Unit 3 (Gather→Train→Export = how AI learns; S1 §6 defers this) | Image |
| — | Teaching slides | **Not provided** | — | Slide Design DNA below is derived from worksheets only |

## 3. Slide Design DNA (worksheet-derived — no slides received)
- [E] Brand: "School Bot" orange logo top-right on every sheet (S2–S4); orange/white round robot mascot peeks from page edge with "School Bot Tips!" bubble (S2 only).
- [E] Header: ชื่อ / เลขที่ / ชั้น line; heavy rounded all-caps display title (S2–S4).
- [E] Content in rounded, **dashed-border** panels; sections labelled "ตอนที่ 1 / ตอนที่ 2" or "ภารกิจ", each with underlined "คำชี้แจง" (S2–S4).
- [E] S2: one dense, warm, cartoon scene (home, street, school, shop, park) — illustration > text. S3: flat solid-color shapes (blue/orange/green/yellow). S4: blank draw box.
- [E] Marking language uses symbols: circle = AI, ⭐ = choose one, ✓ = select function, ✗ = not AI (S2); circle = sensor, square = motor (S4).
- [R] Game UI keeps: orange accent, dashed drop zones/panels, School Bot Tip callout, symbol-based marks (shape + color, not color alone).

## 4. Engagement & Instructional Patterns
| ID | Pattern | Evidence | Purpose | Reusable rule |
|---|---|---|---|---|
| P1 | Day-in-the-life framing | S1 §6 (เช้า/ระหว่างทาง/โรงเรียน/หลังเลิกเรียน) | Connect to own life | Introduce concept through 3–4 familiar moments of the child's day |
| P2 | Paired contrast | S1 §7 (พูด vs กดปุ่ม, ใบหน้า vs รหัส) | Make the distinguishing feature visible | Show near-identical outcomes with one varying cause; ask which has the concept |
| P3 | Function over object | S1 §3 + S2 tip "อย่าดูแค่ว่าเป็นอุปกรณ์อะไร ลองสังเกตว่ากำลังช่วยทำอะไร" | Reasoning over memorizing names | Ask "what is it doing?" before "what is it?" |
| P4 | "Not sure" is valid | S1 §7 🤔, §9 | Safe uncertainty | Always offer a no-penalty "ไม่แน่ใจ" that yields a hint |
| P5 | Seek-and-find scene | S2 | Observation in context | Hide examples in one rich scene; include distractors that are tech but not the concept |
| P6 | Non-example required | S1 Think&Talk, S2 ข้อ 3 | Counter "all electric = AI" misconception | Every classification set must contain plausible non-examples |
| P7 | Ask "why?" | S1 §7 "อะไรทำให้หนูคิดแบบนั้น?" | Justification | Feedback states the reason, not just right/wrong |
| P8 | Input→Process→Output strip | S3 ตอนที่ 2 | System thinking | (Future units) visual 3-box strip with a "?" slot to fix |
| P9 | Revisit & upgrade own artifact | S4 ตอนที่ 2 | Spiral learning | (Future units) reuse earlier student creation in later lesson |

## 5. Worksheet & Scoring Patterns
| EX ID | Original type | Source | Objective | Student action | Answer format | Scoring | Game adaptation |
|---|---|---|---|---|---|---|---|
| EX1 | Seek & circle | S2 instr. | Identify AI situations | Circle in scene | Multiple valid | **Unspecified** | Tap hotspot → judge AI / not AI (`hunt`) |
| EX2 | Pick one (⭐) | S2 ข้อ 1 | Personal choice | Star one | Open | Unspecified | Folded into hotspot inspect; open choice kept in `reflect` |
| EX3 | Single choice ✓ | S2 ข้อ 2 | Name AI's function | Tick 1 of 3 | ดูภาพฯ / อ่านข้อความฯ / ตรวจท่าทาง | Unspecified | Second step after a correct AI judgement |
| EX4 | Mark non-example ✗ + write name | S2 ข้อ 3 | Not all tech is AI | Mark + write | 1 item, free text | Unspecified | Mark ≥1 non-AI hotspot; writing **not** replicated (limitation) |
| EX5 | Line matching | S3 ตอนที่ 1 | Input→label | Draw lines | 1:1 | Unspecified | `match` template |
| EX6 | Fix the missing input | S3 ตอนที่ 2 | Reverse reasoning | Circle 1 of 4 | 1 correct | Unspecified | Future "find & fix" template |
| EX7 | Draw + describe | S4 | Design, explain | Draw, write | Open | Unspecified (rubric needed) | Not convertible without loss; keep on paper or build a "construct" mechanic |
- [R] Proposed default: **practice mode** — unlimited retries, hints logged (mistakes/hints per segment shown on recap, not a score). **Assessment mode** (unbuilt): first-attempt correctness, hints disabled or recorded.

## 6. Reusable Gameplay Mechanics (implemented in `mechanics.tsx`)
| ID | Name | Interaction | Fits | Feedback | Difficulty knobs | Don't use when |
|---|---|---|---|---|---|---|
| explore | Explore & reveal | Tap cards to reveal | Introducing examples | Reveal + follow-up question | # cards | Assessing (no wrong answers) |
| compare | Paired contrast | Pick 1 of 2 + "not sure" | Distinguishing a feature | Reason on both sides | Closer pairs | Concept has no clear contrast |
| match | Categorize to labels | Drag or tap-tap to bins | Function/label mapping | Per-card targeted hint | More labels | Order matters |
| sort | Binary classify | Tap item → bin | Example vs non-example | Explain every placement | Trickier distractors | >3 categories (use match) |
| hunt | Seek & find | Tap objects in an original SVG scene → judge → ability | Observation in context | Ring/✗ marks + reason | Smaller/more spots | No suitable illustration |
| robot | Create & save | Pick job → assemble parts and/or free-draw → name; saved for later revisit | Open design, spiral lessons | Encouraging only; incomplete prompt | More part types | Anything to be scored |
| reflect | Personal link | Multi-select, all accepted | Opinion, exit ticket | None needed | — | Anything with a right answer |
Accessibility: tap-to-place alternative to drag; ≥56px targets; marks use shape + color; `prefers-reduced-motion` respected.

## 7. Exercise-to-Game Templates
Content field contract per segment (`types.ts`): `id, mechanic, missionLabel, title, instruction, tip?, hints[] (graduated), objective, recap` + mechanic data. Completion = all required items correct (hunt: all AI + `minNonAi`). Scoring config: not implemented [R].

## 8. Shared UI Patterns
| Component | Fixed | Configurable |
|---|---|---|
| GameShell (intro/play/done) | layout, flow, retry, hint ladder, stats | lesson object |
| ProgressTrack | done/current/next styles | segment titles |
| Instruction header + School Bot Tip | position, style | label, title, instruction, tip |
| FeedbackBar | 5 tones w/ icon + title | text |
| Button / Card / Icon | style | label, icon |
| Recap (Done) | layout | keyMessages, per-segment recap |

## 9. Reusability Matrix
| Pattern | Type | Content changes | Reused UI | Mechanic can vary |
|---|---|---|---|---|
| P1 | Intro | moments | explore | explore / hunt |
| P2 | Classification | pairs | compare | compare / sort |
| P3,P7 | Feedback | reasons | FeedbackBar, tip | all |
| P5 | Observation | image + hotspots | hunt | hunt |
| P6 | Misconception | non-examples | sort, hunt | sort / hunt / compare |
| P8 | System | I/P/O content | (new) | find & fix, sequence |
Most-reusable: P3, P4, P7, shell. Objective-specific: P2, P5. Not generalized: Unit 3 ability set. Gaps: sequence, find-and-fix (S3), construct/draw (S4), audio narration.

## 10. Evidence References
S1 §2 objectives, §5 timeline, §6–8 missions, §10 assessment, §11 key messages · S2 instruction + ข้อ 1–3 + tip · S3 ตอนที่ 1–2 · S4 ตอนที่ 1–2 · S5 screenshot.

## 11. Assumptions & Unresolved Questions
1. **Conflict:** S1 abilities = ดูภาพ / ฟังเสียง / เข้าใจภาษา / แนะนำ; S2 ข้อ 2 options = ดูภาพและบอกสิ่งที่พบ / อ่านข้อความให้ฟัง / ตรวจท่าทาง. Game uses S1 set in Mission 3 and S2 set in Hidden Hunt exactly as written. Confirm with curriculum team.
2. Hotspot answers in the scene are interpreted by us (e.g. doorbell camera = sees dog). Verify.
3. No scoring rules in any worksheet; no slides received.
4. S3/S4/S5 belong to other units; not used in Unit 3 gameplay.
5. Resolved: S2 image not used (D3).

### Decisions confirmed by user
- D1 (re Q1): Use the Lesson Plan ability set (ดูภาพ / ฟังเสียง / เข้าใจภาษา / แนะนำ) across the whole game, including Hidden Hunt. Lesson Plan outranks worksheet wording.
- D2 (re Q2): User did not confirm the answer key. The S2 worksheet has no answer key; the earlier hotspot answers were our interpretation of the S2 picture. Those hotspots have now been replaced (see D3).
- D3 (re Q5): The S2 scene image **may not be used**. Hidden Hunt now draws its own SVG scene (`SceneBackdrop` in `mechanics.tsx`). The 6 objects are taken from Lesson Plan examples plus S2 situations (door camera, voice speaker, phone translating a sign, video recommendation, plus non-AI lamp and remote-control car). The shop scanner was removed at the user's request. The answer key still needs teacher review.
- D4 (re Q4): A separate **Test mode** was added. It disables hints and retry, and "ไม่แน่ใจ" gives no hint. The score is accuracy (correct / all answers) over compare, match, sort and hunt. Writing the name of a non-AI item (S2 ข้อ 3) is still not replicated.

- D5 (My Dream Robot, S4): Only Part 1 is built, as segment `robot` in Unit 3. It is free and creative like the worksheet: not scored, no wrong answers. It combines part assembly with a free-draw layer. Each part option has `kind` (sensor/motor/none) for Part 2. Robots are saved through `robotStore.ts` (localStorage for now; backend planned but not built). Part 2 "Upgrade My Robot" will reload the saved robot after the Sensor/Motor unit and is **not yet built**.

## 12. Rules for Future Lessons
1. Start from the Lesson Plan objectives; each segment must name its objective.
2. Pick 3–5 mechanics from the list above; avoid repeating the same mechanic back-to-back.
3. Every classification set includes a non-example.
4. Feedback always gives a reason; wrong answers give a targeted hint, never a loss of progress.
5. Offer "not sure" when the lesson plan allows uncertainty.
6. Reuse the worksheet **task structure** as a segment. Do not reuse worksheet artwork unless rights are confirmed.
7. Keep the skill measured by the worksheet; mark any lost dimension (e.g. writing) as a limitation.
8. New lesson = new `lesson-*.ts` only; new mechanic = add to `mechanics.tsx` + `MECHANICS` registry.
