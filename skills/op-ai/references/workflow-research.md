# Research Workflow

> อ้างอิงจาก quistis (research subagent)
> ใช้เมื่อ knowledge base ไม่มีคำตอบ

## Flow

```
1. Knowledge miss → skill แจ้ง admin ว่าไม่พบใน repo
2. ถาม: "ต้องการค้นหาเพิ่มไหม?"
   ├── ไม่ → จบ
   └── ใช่ → เรียก Cloud (researcher) search web
       → Cloud ค้นหา + สรุปผล
       → แสดงผลลัพธ์ให้ admin
       → ถาม: "ต้องการบันทึกเป็นความรู้ใหม่ไหม?"
           ├── ไม่ → จบ
           └── ใช่ → เรียก Aerith (scribe) เขียน YAML
               → แสดง diff → ขอ approve
```

## Cloud Agent Instructions (เมื่อเรียก)

```
@cloud ค้นหาข้อมูลเกี่ยวกับ [topic] สำหรับ OLS Cloud Support
- บริบท: OLS (OpenLandscape Cloud) เป็นผู้ให้บริการ Cloud Hosting ในไทย
- ค้นหาจาก blog.openlandscape.cloud, docs, หรือแหล่งอื่น
- สรุปเป็นภาษาไทย
- แนบลิงก์อ้างอิง
```

## Rules
- ห้ามบันทึกข้อมูลลูกค้า (IP, email, ชื่อ, เบอร์โทร) ลง knowledge/
- ห้าม commit secrets, credentials, API keys
- ต้องขอ approve จาก admin ก่อนบันทึกความรู้ใหม่
