# Case Processing Workflow

> อ้างอิงจาก rinoa (primary reply agent) + case-flow.md

## 1. รับเคส → Classify

```
case → Classify Type:
├── Incident
│   → Request additional information for investigation
│   → Is information sufficient?
│       ├── No → Request more info (Instance name, IP, time, error message)
│       └── Yes → Can we fix it ourselves?
│           ├── Yes → Fix internally → Reply to customer → end
│           └── No → Escalate to infra/dev team → Reply to customer → end
├── Request
│   → Select answer from Q&A knowledge base
│   → Reply to customer → end
├── Abuse Report (external)
│   → ตรวจสอบ IP (เทียบ ip-ranges.yaml)
│   ├── Commercial → forward noc@inet.co.th → end
│   └── Gate/Kory → วิเคราะห์ประเภท + compose reply → Admin ตรวจสอบ → Reply
└── Policy / Compliance
    → Check for T&C violation on Gate platform
    → Reply to customer → end
```

## 2. Platform Routing

### Core Rule
- ถาม Portal ก่อน (Gate / Kory / Commercial)
- ใช้ Public IP cross-verify เมื่อเคสเกี่ยวกับ Instance/VM/Network

### Required Information
1. Portal in use (Kory / Gate / Commercial Cloud)
2. Account Email
3. Public IP (mandatory for Instance, VM, Network, Ping, SSH/RDP, Website, Port, Security Group)
4. Symptom details or request description
5. Service-specific info (Instance name, domain, SSL order, Payment slip, etc.)

### Platform Decision Flow
```
Step 1: ถาม Portal (Kory / Gate / Commercial)
Step 2: ขอ Email + Public IP (ถ้า Instance/Network)
Step 3: Route based on Portal/IP:
├── Kory (kory.openlandscape.cloud / IP 203.154.16.0/24)
│   → Open case at pro-tracker.openlandscape.cloud
│   → Classify as Request or Incident
├── Gate (gate.openlandscape.cloud / IP in Gate ranges)
│   → Open Ticket at internal.openlandscape.cloud
│   → Classify as Request or Incident
├── Email/Verify (insufficient data)
│   → Request more info (Portal + Public IP)
│   → If only email → open as Kory case first
└── Commercial Cloud (portal.openlandscape.cloud, Commercial IP ranges)
    → Direct customer to noc@inet.co.th
```

## 3. Compose Reply

1. **อ่าน style guide** — `data/styles/{cat}-style.md` สำหรับ structure/tone
2. **อ่าน knowledge entry** — `data/knowledge/{cat}.yaml` match keywords
3. **แนบลิงก์ blog** — จาก `data/blog-index.yaml`
4. **Compose draft** — ตาม OLS DNA:
   - เปิด: "เรียน ผู้ใช้บริการ"
   - ปิด: "ขอบคุณครับ"
   - สุภาพ, เป็นทางการ, กระชับ
   - คำศัพท์เทคนิคคงภาษาอังกฤษ
   - ตอบภาษาไทย — ใช้ "ครับ"
5. **แสดง draft ให้ admin ตรวจสอบ**

## 4. Post-Case

- ถ้า admin พอใจ → output final version
- ถาม: "ต้องการบันทึกความรู้ใหม่ไหม?"
  - ถ้าใช่ → เรียก Aerith (scribe) เขียน YAML → ขอ approve
