# ai-tools-mcp — contract plane

สัญญากลางของ ecosystem สำหรับ **identity · policy · capability/resource namespace · audit · approval · conformance criteria**

รีโปนี้เก็บ **ข้อตกลงกับเกณฑ์วัด ไม่ใช่ runtime** — ไม่มีเซิร์ฟเวอร์ ไม่มี gateway ไม่มี MCP server ให้รัน
ของที่รันจริงอยู่ที่ทีม runtime และทีม consumer คนละรีโป

| | |
|---|---|
| status | `active` (specs only) |
| version source | [`VERSION`](VERSION) — release version ของเอกสารชุดนี้ · **ไม่ใช่** เวอร์ชันของสัญญาแต่ละใบ |
| rationale home | [`docs/decisions/`](docs/decisions/) |
| metadata | [`repo.yaml`](repo.yaml) |
| agent rules | [`AGENTS.md`](AGENTS.md) |

## Canonical for

- **identity / principal / actor model** — ชั้นของ credential · ชื่อที่ผู้เรียกประกาศ · บริบทของงาน และการผูกกันระหว่างชั้น
- **policy semantics** — จุดตัดสิน · default deny · operation taxonomy · เงื่อนไขของ wildcard
- **operation / resource / capability namespace** — รูปแบบค่า การซอยค่า และความสัมพันธ์กับคำศัพท์กลางของ `agent-platform`
- **audit contract** — ช่องที่ต้องมี · ช่องที่ห้ามเก็บ · ใครเป็นผู้บันทึกและจากจุดยืนไหน
- **approval contract** — ยังไม่มี ดู [ADR-0009](docs/decisions/) เมื่อเขียนแล้ว · วันนี้เป็นหนี้ที่ค้างอยู่และประกาศไว้ตรง ๆ
- **ToolId / collision rules** — การแปลงชื่อเมื่อรวม tool จากหลายต้นทาง
- **conformance criteria** — เกณฑ์ที่ hub หรือ gateway ตัวใดก็ตามถูกวัดด้วย พร้อมกติกาว่าชุดวัดต้องพิสูจน์อะไรกับตัวเอง

## Not canonical for — อยู่ที่อื่น

| เรื่อง | อยู่ที่ |
|---|---|
| คำศัพท์กลางของ capability · policy · event · artifact · approval schema | [`monthop-gmail/agent-platform`](https://github.com/monthop-gmail/agent-platform) `contracts/` |
| task · handoff · discussion · decision (coordination) | [`monthop-gmail/ai-collaboration-mcp`](https://github.com/monthop-gmail/ai-collaboration-mcp) |
| gateway runtime · connector registry · JWT/JWKS · policy engine | รีโป runtime ของทีม gateway 🔒 private |
| ชุดวัด hub conformance ที่รันอยู่จริง | รีโป consumer ในวง 🔒 private |
| Zabbix · MeshCentral · Express · RAG และ integration ของไซต์ | [`monthop-gmail/itops-mcp-hub`](https://github.com/monthop-gmail/itops-mcp-hub) (นอกวง ไม่ผูกพันเกณฑ์ที่นี่) |

## ที่มาของรีโปนี้ และเหตุที่เพิ่งเปิด

สัญญาชุดนี้ถูกตัดสินและทบทวนบนโต๊ะกลาง `ws-001` ตั้งแต่ **11 ก.ย. 2026** แต่ผลทั้งหมดอยู่ในรูป **ข้อความในกระทู้** —
ไม่มีไฟล์ ไม่มี ADR ไม่มีชุดวัด ทั้งที่รีโปนี้เป็นผู้ถือสัญญา

เปิดเมื่อ **12 ต.ค. 2026** เพื่อย้ายของที่ตัดสินไปแล้วออกจากร้อยแก้วมาเป็นไฟล์ที่อ้างอิงได้
ADR ชุดแรกจึงเกือบทั้งหมดเป็น **การย้ายที่ ไม่ใช่การตัดสินใหม่** และแต่ละใบชี้กลับไปที่กระทู้ต้นทาง

> เหตุผลที่ต้องย้าย เขียนไว้ในรีวิวของเราเอง: **ผลที่เป็นร้อยแก้วทำให้ผู้บริโภคต้อง parse ข้อความเพื่อหาสัญญา**
> ซึ่งเป็นสิ่งที่เราทักทีมอื่นไว้ แล้วทำเองอยู่สี่สัปดาห์

## ADR

ทุกใบอยู่ที่ [`docs/decisions/`](docs/decisions/) · รูปตามมาตรฐานของวง: `NNNN-kebab-title.md` พร้อมบรรทัด `**Status:**`

```
Proposed   ร่างแล้ว ยังไม่มีคนอนุมัติ — AI ร่างได้ แต่รับรองเองไม่ได้
Accepted   มีคนอนุมัติ พร้อมวันที่และผู้มีอำนาจ
Superseded มีใบใหม่แทน — ใบเก่าไม่ถูกลบ
```

| ADR | เรื่อง | Status |
|---|---|---|
| [0001](docs/decisions/0001-identity-layers-and-credential-name-binding.md) | identity สามชั้น และการผูก credential กับชื่อที่ประกาศ | Proposed |
| [0002](docs/decisions/0002-caller-declared-fields-must-be-classified.md) | ช่องที่ผู้เรียกประกาศเอง ต้องถูกจัดประเภท enforced/diagnostics | Proposed |
| [0003](docs/decisions/0003-audit-records-whether-identity-was-resolvable.md) | audit ต้องบันทึกว่าแยกตัวตนได้หรือไม่ และเป็นค่าต่อชั้น | **Accepted** |
| [0004](docs/decisions/0004-unclassified-is-not-privileged.md) | `unclassified` ไม่ใช่ `privileged` | Proposed |
| [0005](docs/decisions/0005-reserve-resource-key.md) | จองคีย์ `resource` · operation ที่มี target ต้องมีข้อที่ระบุ resource | Proposed |
| [0006](docs/decisions/0006-one-endpoint-per-connector-and-toolid-collision.md) | หนึ่ง endpoint ต่อหนึ่ง connector · ToolId ชนกันให้ reject | Proposed |
| [0007](docs/decisions/0007-conformance-criteria-need-mutants.md) | ทุกทางที่ fail ได้ ต้องมี mutant พิสูจน์ | Proposed |
| [0008](docs/decisions/0008-capability-value-format.md) | รูปแบบค่าของ capability และความสัมพันธ์กับคำศัพท์กลาง | Proposed |

## หนี้ที่ค้างและประกาศไว้

1. **approval contract** — ยังไม่มี · เส้น write/privileged ของ runtime รออันนี้อยู่
2. **ชุด conformance ของ upstream adapter** — มีอยู่แล้วที่รีโป runtime 🔒 และทีมนั้นเสนอเองว่าควรย้ายมาที่นี่ · ยังไม่รับโอน
3. **แกน target ใน policy model** — `action.resource` ของ `agent-platform` มีอยู่แล้วแต่ยังไม่มีกฎของค่า · ดู ADR-0005

## ไม่มีในรีโปนี้

ไม่มีความลับ ไม่มีโทเคน ไม่มีข้อมูลส่วนบุคคล ไม่มีเนื้อเอกสารที่จำกัดการเผยแพร่ และไม่เอ่ยชื่อรีโป private
