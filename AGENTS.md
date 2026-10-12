# AGENTS.md: ai-tools-mcp

> **กติกากลางของ org อยู่ที่ `AGENTS.base.md` ในรีโปมาตรฐานของ org (🔒 private) — อ่านก่อนไฟล์นี้**
> ไฟล์นี้เพิ่มเฉพาะกติกาของรีโปนี้
> ⚠️ เทมเพลตกลางให้ใส่ลิงก์ตรงไปยังไฟล์นั้น แต่ `AGENTS.base.md` §7 ห้ามเอ่ยชื่อรีโป private ในที่ public
> รีโปนี้ public จึงอ้างแบบไม่ระบุชื่อ และรายงานข้อขัดนี้เป็น `knowledge-drift` ไว้บนโต๊ะ `ws-001` แล้ว
>
> Metadata (status · owner · depends_on · canonical_for): [`repo.yaml`](repo.yaml)
> last_reviewed: 2026-10-12 · reviewer: `monthop-gmail/ai-tools-mcp` (AI) · อนุมัติการเปิดรีโปโดยเจ้าของงาน

## รีโปนี้คืออะไร

**contract plane ของ ecosystem** — ถือข้อตกลงเรื่อง identity · policy semantics · namespace ของ operation/resource/capability ·
audit contract · approval contract · ToolId collision · conformance criteria

**เป็นสเปกกับเกณฑ์วัด ไม่ใช่ runtime** · ไม่มีเซิร์ฟเวอร์ ไม่มี gateway ไม่มีอะไรให้ deploy
status: `active` · workstream: ยังไม่ถูกลงทะเบียน (`TBD` ใน `repo.yaml` — เป็น gap ที่รู้ตัว)

Canonical for / not canonical for: ดู [`README.md`](README.md) และ `repo.yaml: canonical_for`

## Run / test

ไม่มีโค้ด จึงไม่มีชุดทดสอบ

```bash
# ตรวจ repo.yaml กับ schema กลาง (สคริปต์อยู่ในรีโปมาตรฐานของ org 🔒)
python3 tools/validate_repo_yaml.py repo.yaml    # รันจากรีโปนั้น ชี้มาที่ไฟล์นี้
```

Default branch: `main` · Version source: `VERSION`
**`VERSION` คือเวอร์ชันของเอกสารชุดนี้ ไม่ใช่เวอร์ชันของสัญญาแต่ละใบ** — ตาม base §4 ที่แยก contract version ออกจาก release version
สัญญาแต่ละเรื่องมีเวอร์ชันของตัวเองในใบ ADR ที่นิยามมัน

## Where things live

| ต้องการ | ไปที่ |
|---|---|
| เหตุผลของการตัดสินใจทุกข้อ | `docs/decisions/NNNN-*.md` |
| คำศัพท์กลางที่สัญญาที่นี่ต้องไม่ขัด | `agent-platform` → `contracts/` (`capability/v1` · `policy/v1` · `event/v1` · `approval/v1` · `artifact/v1`) |
| รูปของ task/handoff/decision | `ai-collaboration-mcp` |
| ชุด conformance ที่รันอยู่จริง | รีโป runtime และ consumer 🔒 private (ยังไม่รับโอน — ดู README › หนี้ที่ค้าง) |

## กติกาของรีโปนี้

1. **AI ร่าง ADR ได้ แต่ตั้ง `Status: Accepted` เองไม่ได้** — `Accepted` ต้องมีชื่อผู้มีอำนาจและวันที่ · ตาม base §6
2. **ADR ที่ย้ายมาจากโต๊ะ ต้องชี้กลับไปที่กระทู้ต้นทางทุกใบ** ในช่อง `Related ws-001` · ใบที่ไม่มีตัวชี้ถือว่ายังไม่เสร็จ
   เพราะเหตุผลเต็มอยู่ในกระทู้ และคนอ่านต้องตามไปได้
3. **สัญญาที่นี่ห้ามขัดกับคำศัพท์กลางของ `agent-platform` โดยไม่ประกาศ** — ถ้าจะซอยค่าให้ละเอียดกว่า
   ต้องเขียนในใบว่าซอยมาจากค่าใด ไม่ตั้งชื่ออิสระ (ADR-0008)
4. **ห้ามเอ่ยชื่อรีโป private ในรีโปนี้** เพราะรีโปนี้ public · อ้างด้วยคำบรรยายบทบาทแทน (`รีโป runtime ของทีม gateway 🔒`)
   ตาม base §7 ซึ่งข้อ v0.1 ยังมีผลบังคับ
5. **ไม่รับโอนความเป็นเจ้าของของที่ทีมอื่นเขียนไว้ ก่อนมีใบ** — การย้ายเจ้าของก่อนมีใบคือการตัดสินใบด้วยการลงมือ
6. **รีโปนี้ไม่ implement อะไร** ถ้าข้อเสนอไหนต้องมีโค้ดจึงพิสูจน์ได้ ให้ส่งให้ทีม runtime แล้วอ้างผลของเขาเป็นหลักฐาน

## Required configuration

ไม่มี · รีโปนี้ไม่ต้องใช้ secret หรือ credential ใด

## Decisions

Rationale home: `docs/decisions/`
Cross-workstream decisions: `ws-001` → `dis-fa078bf8` · `dis-3b5cb137` · `dis-514ae7a7` · `dis-a84b7a8e` · `dec-f7cbd10c` · `dec-4e9b685e`

## Known drift / open questions

- **เทมเพลต `AGENTS.md` กลางขัดกับ base §7 เมื่อใช้ในรีโป public** — บรรทัดแรกของเทมเพลตเป็นลิงก์ที่มีชื่อรีโป private
  และ §0 สั่งให้อ่านรีโป index ซึ่งก็ private · รายงานเป็น `knowledge-drift` บน `ws-001` แล้ว
- **workstream ของรีโปนี้ยังไม่ถูกลงทะเบียน** ใน index กลาง · `repo.yaml: workstream: TBD`
- **approval contract ยังไม่มี** และเส้น write/privileged ของ runtime ติดอยู่กับมัน
- **`dec-4e9b685e` ยัง proposed** → ADR-0001 จึงยัง `Proposed` ตามไปด้วย
