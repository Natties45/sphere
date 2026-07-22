# Sphere Skills — จัดหมวดหมู่ใหม่

> **For Hermes:** Execute this plan task-by-task.

**Goal:** จัดระเบียบ skills ใน `sphere/skills/` ให้เป็นหมวดหมู่ชัดเจน ย้ายไฟล์ skill เข้าไปในโฟลเดอร์หมวดหมู่ และอัปเดต README.md + ask-sphere ให้ตรงกัน

**Architecture:** ใช้ directory structure เป็นหมวดหมู่ (engineering/, productivity/, router/, support/) ย้าย skill directories ที่มีอยู่เข้าไปข้างในด้วย `git mv` เพื่อรักษา git history

**Tech Stack:** git, markdown

---

## หมวดหมู่ที่ใช้

| หมวดหมู่ | Skills |
|---|---|
| **router/** | ask-sphere |
| **engineering/** | sphere-code-review, sphere-diagnosing-bugs, sphere-implement, sphere-improve-codebase-architecture, sphere-prototype, sphere-research, scrutinize |
| **productivity/** | sphere-grill-me, sphere-grilling, sphere-handoff, sphere-teach, sphere-writing-great-skills, management-talk, qwenchance |
| **support/** | op-ai |

---

### Task 1: สร้าง directory structure

**Objective:** สร้างโฟลเดอร์หมวดหมู่ที่ยังไม่มี (router/, productivity/, support/)

**Files:**
- Create: `skills/router/`
- Create: `skills/productivity/`
- Create: `skills/support/`

**Step 1: สร้าง directories**

```bash
mkdir -p skills/router skills/productivity skills/support
```

**Step 2: Verify**

```bash
ls -la skills/
```
Expected: มี `router/`, `productivity/`, `support/` โผล่มา

---

### Task 2: ย้าย skills เข้า engineering/

**Objective:** `git mv` skills ที่เป็น engineering ทั้งหมดเข้า `skills/engineering/`

**Files:**
- Move: `skills/sphere-code-review/` → `skills/engineering/sphere-code-review/`
- Move: `skills/sphere-diagnosing-bugs/` → `skills/engineering/sphere-diagnosing-bugs/`
- Move: `skills/sphere-implement/` → `skills/engineering/sphere-implement/`
- Move: `skills/sphere-improve-codebase-architecture/` → `skills/engineering/sphere-improve-codebase-architecture/`
- Move: `skills/sphere-prototype/` → `skills/engineering/sphere-prototype/`
- Move: `skills/sphere-research/` → `skills/engineering/sphere-research/`

**Step 1: git mv แต่ละตัว**

```bash
git mv skills/sphere-code-review skills/engineering/sphere-code-review
git mv skills/sphere-diagnosing-bugs skills/engineering/sphere-diagnosing-bugs
git mv skills/sphere-implement skills/engineering/sphere-implement
git mv skills/sphere-improve-codebase-architecture skills/engineering/sphere-improve-codebase-architecture
git mv skills/sphere-prototype skills/engineering/sphere-prototype
git mv skills/sphere-research skills/engineering/sphere-research
```

**Step 2: Verify**

```bash
ls -la skills/engineering/
```
Expected: 7 directories (6 ที่ย้ายมา + scrutinize ที่มีอยู่แล้ว)

---

### Task 3: ย้าย skills เข้า productivity/

**Objective:** `git mv` skills ที่เป็น productivity ทั้งหมดเข้า `skills/productivity/`

**Files:**
- Move: `skills/sphere-grill-me/` → `skills/productivity/sphere-grill-me/`
- Move: `skills/sphere-grilling/` → `skills/productivity/sphere-grilling/`
- Move: `skills/sphere-handoff/` → `skills/productivity/sphere-handoff/`
- Move: `skills/sphere-teach/` → `skills/productivity/sphere-teach/`
- Move: `skills/sphere-writing-great-skills/` → `skills/productivity/sphere-writing-great-skills/`
- Move: `skills/management-talk/` → `skills/productivity/management-talk/`
- Move: `skills/qwenchance/` → `skills/productivity/qwenchance/`

**Step 1: git mv แต่ละตัว**

```bash
git mv skills/sphere-grill-me skills/productivity/sphere-grill-me
git mv skills/sphere-grilling skills/productivity/sphere-grilling
git mv skills/sphere-handoff skills/productivity/sphere-handoff
git mv skills/sphere-teach skills/productivity/sphere-teach
git mv skills/sphere-writing-great-skills skills/productivity/sphere-writing-great-skills
git mv skills/management-talk skills/productivity/management-talk
git mv skills/qwenchance skills/productivity/qwenchance
```

**Step 2: Verify**

```bash
ls -la skills/productivity/
```
Expected: 7 directories

---

### Task 4: ย้าย skills เข้า router/ และ support/

**Objective:** `git mv` ask-sphere เข้า router/, op-ai เข้า support/

**Files:**
- Move: `skills/ask-sphere/` → `skills/router/ask-sphere/`
- Move: `skills/op-ai/` → `skills/support/op-ai/`

**Step 1: git mv**

```bash
git mv skills/ask-sphere skills/router/ask-sphere
git mv skills/op-ai skills/support/op-ai
```

**Step 2: Verify**

```bash
ls -la skills/router/ skills/support/
```
Expected: router มี ask-sphere, support มี op-ai

---

### Task 5: อัปเดต README.md

**Objective:** เขียน README.md ใหม่ให้ละเอียด แบ่งตามหมวดหมู่ พร้อมคำอธิบายภาษาไทยสั้นๆ อ่านจาก description ใน SKILL.md

**Files:**
- Modify: `skills/README.md`

**Step 1: เขียน README.md ใหม่ทั้งหมด**

เนื้อหาควรประกอบด้วย:
- หัวตารางแยกตามหมวดหมู่ (Router, Engineering, Productivity, Support)
- แต่ละแถว: ชื่อ skill | คำอธิบายภาษาไทยสั้นๆ (1-2 ประโยค) | Source
- คำอธิบายภาษาไทยควรสรุปจาก `description` field ใน SKILL.md ของแต่ละ skill

คำอธิบายภาษาไทยสำหรับแต่ละ skill (จาก description ที่อ่านแล้ว):

**Router:**
- **ask-sphere** — ที่ปรึกษาเลือก skill ที่เหมาะกับงานที่กำลังจะทำ บอกว่า skill ไหนใช้ตอนไหน

**Engineering:**
- **sphere-code-review** — Review changes ก่อน commit ตรวจทั้ง coding standards และ spec compliance
- **sphere-diagnosing-bugs** — Diagnosis loop สำหรับ hard bugs และ performance regressions
- **sphere-implement** — Implement งานตาม spec หรือ tickets
- **sphere-improve-codebase-architecture** — Scan โอกาสปรับปรุง architecture สร้าง HTML report
- **sphere-prototype** — สร้าง throwaway prototype เพื่อตอบ design question
- **sphere-research** — ค้นคว้าข้อมูลจาก primary sources ผ่าน background agent
- **scrutinize** — Outsider-perspective end-to-end review ของ plan/PR/code change

**Productivity:**
- **sphere-grill-me** — ปรับ idea ให้คมก่อนเริ่ม (ไม่มี codebase)
- **sphere-grilling** — ถามลึกเรื่อง plan/decision/idea จนกว่าจะเข้าใจตรงกัน
- **sphere-handoff** — สรุป conversation ส่งต่องานข้าม session
- **sphere-teach** — สอน concept ให้ user แบบ multi-session
- **sphere-writing-great-skills** — Reference สำหรับเขียน skill ให้มีคุณภาพ
- **management-talk** — เขียน content สำหรับผู้บริหาร ปรับภาษา engineer → leadership
- **qwenchance** — Context management, loop detection, handoff ก่อน context เต็ม

**Support:**
- **op-ai** — OLS Support Orchestrator รับเคส ค้นหา และแก้ไข knowledge base

---

### Task 6: อัปเดต ask-sphere (skill router)

**Objective:** ปรับ path references ใน `skills/router/ask-sphere/SKILL.md` ให้ตรงกับโครงสร้างใหม่

**Files:**
- Modify: `skills/router/ask-sphere/SKILL.md`

**Step 1: อ่านไฟล์ปัจจุบันและแก้ path references**

เปลี่ยน path references จาก `skills/sphere-xxx/` → `skills/engineering/sphere-xxx/` หรือ `skills/productivity/sphere-xxx/` ตามหมวดหมู่

---

### Task 7: Commit

**Objective:** Commit การเปลี่ยนแปลงทั้งหมด

**Step 1: git add และ commit**

```bash
git add -A
git commit -m "refactor: จัดหมวดหมู่ skills ใหม่ (router/ engineering/ productivity/ support/)"
```

---

## Tests / Validation

- `ls -la skills/` — ควรเหลือแค่ `README.md`, `router/`, `engineering/`, `productivity/`, `support/`
- แต่ละหมวดหมู่มี skill ครบตามตาราง
- `git status` — แสดง renamed เท่านั้น ไม่มี deleted + untracked
- `hermes skills tap add` จาก repo นี้ยังใช้งานได้ (path เปลี่ยนแต่ SKILL.md structure เหมือนเดิม)

## Risks & Open Questions

- **Git history:** `git mv` preserve history แต่คนที่ clone เก่าจะต้อง pull และอาจมี conflict ถ้าแก้ไขไฟล์ค้างไว้
- **hermes skills tap add:** Hermes tap จะ map skill name → path โดยอัตโนมัติ ไม่ได้ hardcode path ไว้ ดังนั้นย้ายได้ไม่มีปัญหา
- **ask-sphere:** ต้องอัปเดต path references ให้ตรง
