# Knowledge Writer Workflow

> อ้างอิงจาก laguna (writer subagent)
> ใช้เมื่อ admin ต้องการบันทึกความรู้ใหม่

## Flow

```
1. Admin บอก "บันทึก" หรือ "เพิ่มความรู้"
2. เรียก Aerith (scribe) → เขียน YAML entry ใหม่
3. Aerith ตรวจสอบ:
   - category ถูกต้อง (ดู category-map.md)
   - keywords ภาษาไทย 3-6 คำ
   - intent ถูกต้อง (info / incident / request)
   - answer ใช้ OLS DNA (เรียน ผู้ใช้บริการ ... ขอบคุณครับ)
   - refs มีลิงก์ blog ถ้าจำเป็น
4. แสดง diff ให้ admin ตรวจสอบ
5. ขอ approve ก่อนเขียนจริง
6. ถ้า approve → Aerith เขียนไฟล์
7. Verify: อ่านไฟล์ซ้ำ ตรวจสอบว่าเขียนถูกต้อง
```

## YAML Entry Template

```yaml
          - id: <unique-slug>
            keywords:
              - <keyword 1>
              - <keyword 2>
              - <keyword 3>
            intent: info | incident | request
            answer: |
              เรียน ผู้ใช้บริการ

              [response template]

              ขอบคุณครับ
            refs:
              - title: "<Article Title>"
                url: "https://blog.openlandscape.cloud/<slug>/"
```

## Rules
- ห้ามบันทึกข้อมูลลูกค้า (IP, email, ชื่อ, เบอร์โทร)
- keywords ต้องเป็นภาษาไทย 3-6 คำ
- answer ต้องเปิดด้วย "เรียน ผู้ใช้บริการ" และปิดด้วย "ขอบคุณครับ"
- ต้องขอ approve ก่อนเขียนจริงเสมอ
