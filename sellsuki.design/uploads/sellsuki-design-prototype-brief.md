# Design Spec — sellsuki.design · Design system & asset hub

**Status:** DRAFT (Stage 2 — prototype handoff)
**Track / Size / Stack:** PRODUCT / L / design = DS 2.0 (ssk-* / brand: patona) → production = DS 1.0 (via suki-designer)
**Purpose of this doc:** brief ให้ Claude Design ขึ้น clickable prototype ได้ทันที

---

## ▶ Paste-to-Claude-Design prompt (ก๊อปไปวางได้เลย)

> สร้าง clickable prototype ของ **sellsuki.design** — internal design-system & asset hub ของ Sellsuki ที่เสิร์ฟทั้งทีม Product และ Project
> ใช้ **DS 2.0 (ssk-* components, brand: patona)** เป็น design language
> โครงสร้าง 4 zone + persistent global bar (ดู IA ด้านล่าง)
> Prototype ต้องมี: (1) global nav shell, (2) Overview/home, (3) Foundations, (4) Components index + component detail ที่โชว์ครบ 6 states, (5) Design check tool — ที่เหลือทำเป็น low-fi stub ลิงก์ถึงได้พอ
> Behavior หลักที่ต้อง interactive: **track filter = Project → ซ่อน zone BUILD ทั้งก้อน**, DS version switcher, ⌘K search, status badge ทุกหน้า
> Desktop-first, รองรับ dark/light, ทุก interactive element มี 6 states

---

## 1. Research summary (Stage 1)

**IA outline (locked) — 4 zones, nav ลึก 2 ชั้น**

```
sellsuki.design
│ global bar: ⌘K search · track filter (Product/Project) · role switcher · DS version switcher
│
├─ GET STARTED
│  ├─ Overview        /                 [B]
│  ├─ Principles      /principles       [B]
│  └─ Process         /process          [B]
├─ USE · both tracks
│  ├─ Foundations     /foundations      [B]
│  ├─ Brand           /brand            [B]
│  ├─ Assets          /assets           [B]
│  └─ Skills          /skills           [B]
├─ BUILD · product only        ← ซ่อนทั้งก้อนใน Project mode
│  ├─ Design system   /design-system    [P]
│  ├─ Components      /components        [P]
│  ├─ Patterns        /patterns         [P]
│  └─ Design check    /design-check      [P]
└─ META
   └─ Resources       /resources        [meta]
```
`[B]` both tracks · `[P]` product-only · route = kebab-case

**Key insight ที่ shape design:** ระบบเสิร์ฟ 2 track ที่ขัดกัน — Product ใช้ DS เต็ม, Project ห้ามแตะ DS ⇒ track filter ไม่ใช่ของประดับ แต่เป็นตัวบังคับ visibility (ซ่อน zone BUILD ใน Project mode) เอา hard rule ของ delivery standard มาฝังใน UI ไม่ต้องพึ่งวินัยคน

---

## 2. Screens (Stage 2)

### Screen: Global shell (nav + global bar)
- **Purpose:** โครงคงที่ทุกหน้า — top bar + left nav 4 zone
- **Global bar (persistent):** ⌘K search · track filter (Product/Project toggle) · role switcher (PO/UXUI/DEV) · DS version switcher (1.0/2.0/3.0)
- **Behavior:** track = Project → collapse/ซ่อน zone BUILD; role/version = เปลี่ยน context ของหน้า
- **6 states:** default / loading (skeleton nav) / empty (n/a) / error (search fail toast) / success (search result) / disabled (version ที่ยัง preview = greyed)
- **Components (DS 2.0):** `ssk-app-shell` / `ssk-nav` / `ssk-topbar` · ⌘K = FLAG (ดูข้อ 2.6)

### Screen: Overview `/`
- **Purpose:** ประตูแรก — บอกว่าคืออะไร + route คนเข้าตาม role/track
- **Layout:** hero statement · role+track entry cards (3 การ์ด: Product / Project / by-role) · "what's new" feed (changelog ข้าม DS+token+skill) · quick links
- **6 states:** default / loading (feed skeleton) / empty (no updates → "ยังไม่มีอัปเดต") / error (feed โหลดไม่ได้) / success / disabled
- **Components (DS 2.0):** `ssk-card` · `ssk-button` · `ssk-badge` (status) · `ssk-list`

### Screen: Foundations `/foundations` (ตัวแทน zone USE)
- **Purpose:** source of truth ของ token + craft ที่ทั้งสอง track ใช้
- **Layout:** section nav (color · type · space · grid · motion · a11y · content) · token table + live swatch · version tab
- **6 states:** default / loading / empty (category ว่าง) / error / success (copy token สำเร็จ) / disabled (token deprecated = strikethrough + badge)
- **Components (DS 2.0):** `ssk-tabs` · `ssk-table` · `ssk-color-swatch` · `ssk-copy-button`

### Screen: Components index `/components`
- **Purpose:** library ของ UI element ราย component
- **Layout:** search + filter (version · status · category) · grid ของ component card แสดง **Component ID** + status badge
- **Categories:** actions · inputs & forms · data display · feedback · navigation · layout
- **6 states:** default / loading (card skeleton) / empty (filter ไม่เจอ → "ปรับ filter") / error / success / disabled (component preview-only = badge)
- **Components (DS 2.0):** `ssk-search` · `ssk-filter-chip` · `ssk-card` · `ssk-badge`

### Screen: Component detail `/components/{id}`  ★ หน้าโชว์ 6-states
- **Purpose:** หน้าเดียวที่ demonstrate มาตรฐาน "ทุก component ครบ 6 states"
- **Layout (ตามลำดับ):** overview & when-to-use · anatomy · **states gallery (default/loading/empty/error/success/disabled)** · variants & props · a11y · code tab (DS 1.0 / DS 2.0) · tokens used (deep-link Foundations) · translation status · used-in-patterns backlink
- **6 states:** เป็น *เนื้อหา* ของหน้า (states gallery) — หน้าเองก็ต้องมี loading/error ของ live preview ด้วย
- **Components (DS 2.0):** `ssk-tabs` · `ssk-code-block` · `ssk-badge` · live `ssk-*` ตาม component ที่กำลังโชว์
- **DS Translation:** ทุก component card ต้องมี badge `DS2→DS1: มีคู่ / ไม่มี / fallback`

### Screen: Design check `/design-check`  ★ differentiator
- **Purpose:** "linter สำหรับ design" — เครื่องมือ QA ที่ Process → Stage 5 เรียกใช้
- **Layout:** submit area (paste screen/flow หรือ pick Pattern/Component ID) · checklist runner (6-states · a11y · token-only · DS translation gate · handoff-shippable) · pass/fail report ราย rule
- **6 states:** default (idle) / loading (running check) / empty (ยังไม่ submit) / error (input invalid → inline error) / success (report พร้อม) / disabled (rule ที่ n/a กับ track ปัจจุบัน)
- **Components (DS 2.0):** `ssk-upload` / `ssk-textarea` · `ssk-checklist` · `ssk-result-card` · `ssk-progress` — **interactive checker = FLAG** (ดูข้อ 2.6)

### Secondary screens (low-fi stub พอ — ลิงก์ถึงได้)
Principles · Process · Brand · Assets · Skills · Design system hub · Patterns · Resources — ทำเป็นหน้า placeholder มี header + 1-2 section จริง ลิงก์ nav ทำงาน

### 2.6 DS translation flags (เช็คก่อนขึ้น production — Stage 4 gate)
Component 3 ตัวนี้คาดว่า **DS 1.0 ยังไม่มีคู่** ต้องหา fallback ก่อน build จริง — prototype (DS 2.0) ทำได้ปกติ แต่ mark ไว้:
1. **⌘K command palette** — FLAG · fallback: search bar ธรรมดา
2. **Interactive design-check runner** — FLAG · fallback: static checklist + manual
3. **DS version switcher (global)** — FLAG · fallback: tab ระดับหน้า

---

## 3. Validate result (Stage 3) — pending
- PRODUCT: ยังไม่ได้ run AI usability — L-size ต้อง 3+ persona ก่อน finalize
- 🛑 Gate: user confirm persona ก่อน run (Stage 3)

---

## 4. Build notes สำหรับ DEV — ยังไม่เข้า Stage 4
- Entry ได้เมื่อ spec = FINAL + DS translation table ครบ (ตอนนี้ยัง DRAFT)
- Design direction / mood: **pending** — `Mood and Tone Design.md` ยังไม่ได้ถอด ⇒ prototype ใช้ DS 2.0 patona default ไปก่อน แล้วค่อย re-skin เมื่อได้ mood

## Deviation Log (Stage 4-5)
| # | What | Why | Approver | Date |
|---|---|---|---|---|
