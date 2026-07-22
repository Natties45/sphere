---
name: agy-worker
description: "Delegate implementation work to Antigravity CLI (agy) as a subordinate worker. Use when the user wants code written, bugs fixed, or features implemented and you want to save tokens by offloading the heavy lifting to agy, with Hermes acting as manager — selecting the model, reviewing the diff, and committing only when quality passes."
version: 1.0.0
author: natti
license: MIT
metadata:
  hermes:
    tags: [antigravity, delegation, implementation, coding-agent, manager-worker]
    related_skills: [sphere-implement, sphere-code-review, antigravity-cli]
---

# agy-worker

Hermes = **Manager**, agy = **Worker**

Hermes วิเคราะห์งาน → เลือกโมเดล → ส่ง spec → agy implement → Hermes review → commit

## เมื่อไหร่ควรใช้

- งาน implement ใหญ่ๆ ที่ใช้ tokens เยอะ — ให้ agy รับไปทำแทน
- อยากประหยัด tokens (Hermes ใช้ model แพง, agy ใช้ Gemini ถูก)
- อยากได้ second opinion / cross-check จาก Gemini model
- งานที่ต้องรัน tests, build, หรือ multi-file changes

**อย่าใช้เมื่อ:**
- งานเล็กๆ แก้ 1-2 บรรทัด — ให้ Hermes ทำตรงๆ เลย
- ต้องใช้ Hermes tools ที่ agy เข้าถึงไม่ได้ (browser, computer_use, email ฯลฯ)
- งานที่ต้องถาม user ระหว่างทาง — agy ไม่สามารถใช้ `clarify` ได้

## Model Selection

จาก `agy models` จริง:

| ระดับงาน | โมเดล | ราคา | ตัวอย่างงาน |
|---------|-------|------|------------|
| **เบา** | `gemini-3.6-flash-low` | ถูกสุด | แก้ typo, rename, lint fix, refactor เล็กน้อย |
| **กลาง** | `gemini-3.6-flash-high` | กลาง | implement ตาม spec ชัดเจน, feature ใหม่ขนาดกลาง |
| **หนัก** | `gemini-3.1-pro-high` | แพงกว่า | งานซับซ้อน, architecture change, refactor ใหญ่ |
| **วิกฤต** | `claude-opus-4-6-thinking` | แพงสุด | security-sensitive, critical path, งานที่ต้อง reasoning ลึก |
| **ทางเลือก** | `gpt-oss-120b-medium` | ฟรี? | open source model, ไว้ใช้ตอน Gemini ติด |

**วิธีเลือก:** Hermes ดูจาก spec/user prompt → ถ้างานมี scope ชัดเจน ใช้ `gemini-3.6-flash-high` เป็น default ถ้างานเบามากลดเป็น `flash-low` ถ้างานซับซ้อนหรือ sensitive ขึ้นเป็น `pro-high` หรือ `opus-thinking`

## Workflow

### 1. วิเคราะห์งานและเลือกโมเดล

อ่าน spec หรือฟัง user → ตัดสินใจว่าใช้โมเดลระดับไหน

### 2. สร้าง spec file

เขียน spec ใส่ `.hermes/agy-spec.md` (relative to project root) — ระบุให้ชัด:
- สิ่งที่ต้องการให้ทำ
- ไฟล์ที่เกี่ยวข้อง
- constraints / conventions
- **ห้าม agy commit** — ให้แค่แก้ไฟล์

### 3. ส่ง agy ไป implement

ใช้ pattern:

```bash
agy -p --model <selected-model> --print-timeout 15m \
  'Read .hermes/agy-spec.md and implement it exactly. Do not commit, do not create git commits. Just modify the files.' \
  --dangerously-skip-permissions
```

รันแบบ background + notify_on_complete:

```bash
terminal(command="agy -p --model gemini-3.6-flash-high --print-timeout 15m 'Read .hermes/agy-spec.md and implement it exactly. Do not commit.' --dangerously-skip-permissions", workdir="/path/to/repo", background=true, notify_on_complete=true)
```

### 4. รอผล

ใช้ `process(action="wait", session_id=<id>)` หรือรอ notification

### 5. Review ผลงาน

ใช้ `git diff` ดูการเปลี่ยนแปลงที่ agy ทำ:

```bash
git diff
```

ตรวจ:
- ตรงตาม spec ไหม
- มี code smells หรือไม่ (ใช้หลักจาก sphere-code-review)
- tests ผ่านไหม (รันเอง)
- ไม่มี secrets หรือ credentials รั่ว

### 6. ตัดสินใจ

- **ผ่าน** → `git add -A && git commit -m "feat: <description> (via agy)"`
- **ไม่ผ่าน** → เขียน feedback กลับไปที่ `.hermes/agy-spec.md` → กลับไป step 3 (loop สูงสุด 3 รอบ)
- **ไม่ผ่าน 3 รอบ** → ทำเอง หรือถาม user

### 7. Cleanup

ลบ `.hermes/agy-spec.md` (หรือเก็บไว้เป็น reference)

## ตัวอย่างการใช้งาน

### งานเบา: แก้ lint error

```bash
# Hermes เลือก flash-low
agy -p --model gemini-3.6-flash-low --print-timeout 5m \
  'Fix all ESLint errors in src/components/Table.tsx. Do not change any logic.' \
  --dangerously-skip-permissions
```

### งานกลาง: implement feature

```bash
# Hermes เลือก flash-high
agy -p --model gemini-3.6-flash-high --print-timeout 15m \
  'Read .hermes/agy-spec.md and implement the search feature. Do not commit.' \
  --dangerously-skip-permissions
```

### งานหนัก: refactor สถาปัตยกรรม

```bash
# Hermes เลือก pro-high
agy -p --model gemini-3.1-pro-high --print-timeout 30m \
  'Read .hermes/agy-spec.md and refactor the auth module as specified. Do not commit.' \
  --dangerously-skip-permissions
```

## Pitfalls

1. **agy ไม่มี `--output-format json`** — ผลลัพธ์เป็น plain text ต้องอ่าน diff จาก `git diff` เอาเอง
2. **agy ไม่มี `--max-turns`** — ใช้ `--print-timeout` แทน (default 5m, งานหนักควรเพิ่มเป็น 15m-30m)
3. **agy ไม่สามารถใช้ Hermes tools** — ส่งแค่งานที่ใช้ terminal + file I/O เท่านั้น
4. **อย่าให้ agy commit** — agy อาจ commit ด้วย message ไม่ดี หรือ commit งานที่ไม่ผ่าน review
5. **`--dangerously-skip-permissions` จำเป็น** — ไม่งั้น agy จะรอ approve ตลอด (แต่ Hermes ต้อง review ทุกครั้งอยู่แล้ว)
6. **agy ใช้ working directory ปัจจุบัน** — ต้อง `workdir=` ให้ถูกต้อง
7. **อย่าให้ agy ทำงานพร้อมกันหลายงานใน repo เดียว** — conflicts แน่ ใช้ worktree แยกถ้าต้องการ parallel
8. **agy ไม่รู้ context ของ conversation** — ต้องใส่ทุกอย่างใน spec file ให้ครบ

## Verification Checklist

- [ ] เลือกโมเดลเหมาะสมกับงาน (เบา/กลาง/หนัก/วิกฤต)
- [ ] Spec file ครบถ้วน — ไม่ต้องให้ agy เดา
- [ ] agy ทำงานเสร็จ (exit code 0, ไม่ timeout)
- [ ] `git diff` ตรวจแล้ว — ตรง spec, ไม่มี code smells ร้ายแรง
- [ ] Tests รันผ่าน (หรืองานนั้นไม่มี tests)
- [ ] ไม่มี secrets/credentials/routes ใน diff
- [ ] Commit ด้วย message ที่อ่านรู้เรื่อง
- [ ] ลบ `.hermes/agy-spec.md` (ถ้าไม่จำเป็น)
