# sphere

คลัง skill ส่วนตัวของ natti — ไว้เก็บ SKILL.md สำหรับ Hermes Agent

## โครงสร้าง

```
sphere/
├── README.md              # นี้
├── IDEA.md                # idea ดั้งเดิม
├── .gitignore
├── templates/
│   └── SKILL.md.template  # template สำหรับสร้าง skill ใหม่
└── skills/
    ├── README.md           # catalog แยกหมวด
    ├── ask-sphere/         # router — ถามว่าควรใช้ skill ไหน
    ├── op-ai/              # OP-AI OLS Support Orchestrator
    ├── qwenchance/         # context management, loop detection
    ├── management-talk/    # เขียน content สำหรับผู้บริหาร
    ├── sphere-code-review/
    ├── sphere-diagnosing-bugs/
    ├── sphere-implement/
    ├── sphere-improve-codebase-architecture/
    ├── sphere-prototype/
    ├── sphere-research/
    ├── sphere-grill-me/
    ├── sphere-grilling/
    ├── sphere-handoff/
    ├── sphere-teach/
    └── sphere-writing-great-skills/
```

## วิธีใช้

```bash
# 1. clone repo
git clone <repo-url>

# 2. เพิ่มเป็น skill source ใน Hermes
hermes skills tap add <path-to-sphere>

# 3. install skill ที่ต้องการ
hermes skills install ask-sphere
```

หรือ copy `skills/<name>/SKILL.md` ไปไว้ใน `~/.hermes/skills/<name>/` ก็ได้

## ที่มา

| Source | Skills |
|---|---|
| [mattpocock/skills](https://github.com/mattpocock/skills) | code-review, diagnosing-bugs, implement, improve-codebase-architecture, prototype, research, grill-me, grilling, handoff, teach, writing-great-skills |
| [thananon/9arm-skills](https://github.com/thananon/9arm-skills) | qwenchance, management-talk |
| สร้างเอง | ask-sphere, op-ai |
