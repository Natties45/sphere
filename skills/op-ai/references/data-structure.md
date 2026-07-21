# Data Repository Structure — selfservice-repo

> โครงสร้าง data repo สำหรับ OLS Chatbot Knowledge Base
> อยู่ที่ `../selfservice-repo/` (side-by-side กับ sphere repo)

## Root Layout

```
selfservice-repo/
├── data/
│   ├── knowledge/          # ฐานความรู้ (11 YAML + 2 MD)
│   ├── styles/             # Style guides (10 MD)
│   ├── blog-index.yaml     # Blog index (Gate)
│   ├── blog-index-kory.yaml# Blog index (Kory, รอข้อมูล)
│   └── blog-archive/       # Archived blog articles
├── docs/
│   └── architecture.md     # Data schema + external links
├── auto-generated/         # Daily digests
├── export/                 # Exported documents
├── AGENTS.md               # Workspace instructions
└── README.md
```

## Knowledge YAML Schema

```yaml
categories:
  <category-key>:            # e.g., vm-instance, network-security
    name: "<Display Name>"
    triggers: |
      <when this category applies>
    sections:
      <section-key>:
        name: "<Section Name>"
        entries:
          - id: <unique-slug>
            keywords: [keyword1, keyword2, ...]  # 3-6 Thai keywords
            intent: info | incident | request
            answer: |
              เรียน ผู้ใช้บริการ
              [response template]
              ขอบคุณครับ
            refs:
              - title: "<Article Title>"
                url: "https://blog.openlandscape.cloud/<slug>/"
```

## Style Guide Schema (MD)

แต่ละไฟล์ใน `data/styles/` ประกอบด้วย:
- **Structure** — ลำดับ sections ใน response
- **Tone** — ระดับภาษา, key phrases
- **Required Elements** — links, variables, references ที่ต้องมี
- **Variant: Ticket Reply Mode** — First reply vs subsequent
- **Key Phrases** — วลีภาษาไทยที่ใช้ซ้ำ

## Blog Index Schema

```yaml
blog-index:
  <category-key>:
    - title: "<Article Title>"
      url: "https://blog.openlandscape.cloud/<slug>/"
```

## Special Files

| File | Content |
|------|---------|
| `data/knowledge/ip-ranges.yaml` | IP CIDR + portal URLs + ticket system URLs (flat structure) |
| `data/knowledge/case-flow.md` | Decision tree: classification → channel → platform routing |
| `data/knowledge/customer-scripts.md` | Thai-language scripts for customer communication |
