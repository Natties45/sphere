---
name: ask-sphere
description: Router — บอกว่า skill ไหนใน sphere ใช้ตอนไหน เหมาะกับสถานการณ์ไหน
disable-model-invocation: true
---

# Ask Sphere

Skill router สำหรับ skills ทั้งหมดใน `sphere/skills/`

## Main flow: idea → ship

1. **`sphere-grill-me`** — ปรับ idea ให้คมขึ้นก่อนเริ่ม ถ้ายังไม่มี codebase
2. **`sphere-grilling`** — ถามลึกเรื่อง plan/decision/idea
3. **`sphere-implement`** — implement ตาม spec หรือ tickets
4. **`sphere-code-review`** — review changes ก่อน commit

## On-ramps

- **มี bug ยากๆ** → **`sphere-diagnosing-bugs`** — diagnosis loop สำหรับ hard bugs
- **อยากลองของก่อน** → **`sphere-prototype`** — throwaway prototype
- **ต้องหาข้อมูลก่อน** → **`sphere-research`** — delegate reading ให้ background agent
- **architecture เริ่มรก** → **`sphere-improve-codebase-architecture`** — scan โอกาสปรับปรุง

## Context management

- **context ใกล้เต็ม / agent วน loop** → **`qwenchance`** — keep task on-track, loop detection, handoff
- **ต้องส่งต่องานข้าม session** → **`sphere-handoff`** — compact conversation เป็น handoff doc

## Productivity

- **สอน concept ให้ user** → **`sphere-teach`** — multi-session learning
- **เขียน skill เอง** → **`sphere-writing-great-skills`** — reference สำหรับ writing skills
- **เขียน content สำหรับผู้บริหาร** → **`management-talk`** — rewrite technical → leadership language

## Other

- **OP-AI OLS Support** → **`op-ai`** — support orchestration
