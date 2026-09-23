# Sellsuki — App Selector Pattern

**Base ID** `app-selector-104` · ใช้ได้กับทุก brand (หน้านี้แสดงทุกแบรนด์พร้อมกัน จึงไม่มี Instance ID ต่อแบรนด์)

หน้าเลือกแอปพลิเคชันหลัง login จากระบบกลาง — ผู้ใช้เห็นทุกแอปของบริษัทที่ตัวเองมีสิทธิ์เข้า แล้วเลือกเข้าอันใดอันหนึ่ง

ที่มา: Figma `CCS-2025` → section **App Selector** (`node-id=8413-22617`)
สอง frame ในไฟล์: `App Selector 3x2` (`8413:22618`) · `App Selector 4x1` (`8413:22640`)

- โครง **แถบบน + Choco** → `AppTopNav.md` (หน้านี้ไม่มี topnav / sidebar)
- โครง **หน้า List** → `oc2plus-shell-listpage.md`
- โครง **หน้ารายละเอียด** → `Detail_Pattern.md`

> หน้านี้เป็น **หน้าเต็มจอไม่มี shell** — ไม่มี topnav ไม่มี sidebar เพราะผู้ใช้ยังไม่ได้เลือกแอป
> จึงยังไม่มีบริบทของแอปใดให้ render shell

---

## 1. โครงสร้าง

```
<div>  หน้าเต็มจอ · min-height:100dvh · พื้น --page-bg
└── <div ref=wrap>  ชั้นวางภาพประกอบ · align-items:flex-end · justify-content:space-between
    │                max-width 1920px · min-width 1280px
    ├── <img>  ภาพซ้าย 600×600 ปักมุมล่างซ้าย
    ├── <img>  ภาพขวา 600×600 ปักมุมล่างขวา
    └── <section>  จัดกลางทั้งแนวตั้งและแนวนอน
        └── <div data-card>  การ์ดขาว · radius 12 · padding 32/40 · gap 32 · shadow-sm
            ├── <header>  gap 16 · จัดกลาง
            │   ├── logo บริษัท 50 × 50  (assets/sellsuki-icon.svg)
            │   └── แถวข้อความ  gap 8 · "สวัสดี!," + ชื่อผู้ใช้จริง · flex-wrap:wrap
            ├── <div data-select>  gap 12
            │   ├── ข้อความนำ "กรุณาเลือกระบบที่ต้องการเข้าใช้งาน"
            │   └── <div data-app-grid>  grid · gap 16
            │       └── <button data-app-card> × n   การ์ดสี่เหลี่ยมจัตุรัส
            └── <div data-actions>  gap 16 · ปุ่ม 2 ใบ flex:1 เท่ากัน
```

กติกา:
- การ์ดกลางจัดกลางจอทั้งสองแกน ภาพประกอบอยู่ **ชั้นล่าง** ไม่รับ pointer (`pointer-events:none`)
- ภาพประกอบปักมุมล่าง ไม่ยืดตามจอ — จอกว้างขึ้นภาพแยกออกจากกัน จอแคบลงภาพเข้าหากัน
- การ์ดแอปเป็น **สี่เหลี่ยมจัตุรัส** (`aspect-ratio:1`) กว้างเท่ากันทุกใบด้วย grid `1fr`
- ปุ่มล่างสองใบกว้างเท่ากันด้วย `flex:1` เสมอ ไม่ว่าข้อความจะยาวไม่เท่ากัน

---

## 2. Token

ค่าทั้งหมดอ่านจาก Figma variables ของ node นี้โดยตรง

| Token ใน Figma | ค่า | ใช้ที่ |
|---|---|---|
| `Colors/Background/bg-primary_hover` | `#f9fafb` | พื้นหน้า |
| `Colors/Background/bg-primary` · `Colors/bg/default` | `#ffffff` | พื้นการ์ดกลาง · พื้นการ์ดแอป |
| `Colors/Text/text-primary` | `#1f2937` | "สวัสดี!," · ข้อความนำ · ชื่อแอป |
| `Colors/Text/text-brand-primary` | `#32a9ff` | ชื่อผู้ใช้ |
| `Colors/Text/text-secondary` | `#6b7280` | คำอธิบายแอป |
| `Colors/Stroke/stroke-primary` | `#e5e7eb` | ขอบการ์ดแอป (ดูข้อ 8) |
| `Colors/Icon/icon-dark` | `#111827` | ไอคอนในปุ่ม |
| `Colors/Button/Solid/button-solid-bg` · `-border` | `#32a9ff` | ปุ่มหลัก |
| `Colors/Button/Solid/button-solid-fg` | `#ffffff` | ตัวอักษรปุ่มหลัก |
| `Colors/Button/Solid Light/button-solid_light-bg` | `#ffffff` | ปุ่มรอง |
| `Colors/Button/Solid Light/button-solid_light-border` | `#e5e7eb` | ขอบปุ่มรอง |
| `Colors/Button/Solid Light/button-solid_light-fg` | `#1f2937` | ตัวอักษรปุ่มรอง |
| `spacing-md` | `8` | gap แถวข้อความ header |
| `spacing-xl` | `16` | gap header · gap actions |
| `spacing-lg` | `12` | radius การ์ดกลาง |
| `spacing-4xl` | `32` | padding แนวตั้งการ์ดกลาง |
| `Spacing/Spacing-2xl` | `12` | gap ใน select |
| `Spacing/Spacing-6xl` | `32` | gap ระหว่าง section ในการ์ด |
| `Spacing/Spacing-4xl` | `20` | padding การ์ดแอป |
| `Spacing/Spacing-md` | `6` | gap ใน list ของการ์ดแอป |
| `Spacing/Spacing-lg` | `8` | gap ไอคอน ↔ ข้อความในปุ่ม |
| `Border-radius/radius-md` · `[Old] Radius/rounded-8px` | `8` | radius ปุ่ม · radius การ์ดแอป |
| `Shadows/shadow-sm` | 2 ชั้น | เงาการ์ดกลาง |

```css
/* shadow-sm — เงาของการ์ดกลาง */
box-shadow:
  0 1px 2px -1px rgba(10, 13, 18, .10),
  0 1px 3px  0   rgba(10, 13, 18, .10);
```

---

## 3. Typography

| ส่วน | Text style ใน Figma | ค่า |
|---|---|---|
| "สวัสดี!, <ชื่อผู้ใช้>" | `H4 - 2XL/36px - Bold` | DB HeaventRounded Bold · 36px · line-height 1 · ย่อตามจอ (ดูข้อ 9) |
| ข้อความนำ | `Body1 - Base/24px - Med` | DB HeaventRounded Med · 24px · line-height 1 |
| ชื่อแอปในการ์ด | — | DB HeaventRounded Med · 24px |
| คำอธิบายแอป | — | DB HeaventRounded Regular · 18px |
| ตัวอักษรในปุ่ม | `Body1 - Base/24px - Med` | DB HeaventRounded Med · 24px |

ทุกค่า `letter-spacing: 0`

### 3.1 ชื่อผู้ใช้

ข้อความหลัง "สวัสดี!," คือ **ชื่อผู้ใช้ที่ login เข้ามาจริง** ไม่ใช่ placeholder `Username` ตามในไฟล์
อ่านจาก **user profile ตัวเดียวกับที่ account menu ใน `AppTopNav.md` ใช้** — เปลี่ยนที่เดียวเปลี่ยนทั้งสองที่

```js
// แหล่งเดียวกับ accountName ของ account menu
asUserName: userProfile.name   // เช่น "Whitchaya Wanichon"
```

แถวคำทักทายต้องมี `flex-wrap:wrap` — ชื่อยาวบนจอแคบต้องตกบรรทัดได้ ห้าม `white-space:nowrap`

---

## 4. การ์ดกลาง

| ส่วน | ค่า |
|---|---|
| พื้น | `#ffffff` |
| radius | **12px** (`spacing-lg`) |
| padding | **32px แนวตั้ง / 40px แนวนอน** |
| gap ระหว่าง section | **32px** (`Spacing/Spacing-6xl`) — header · select · actions |
| เงา | `shadow-sm` (ดูข้อ 2) |
| ความกว้าง | ยืดตามเนื้อหา · ในไฟล์ Figma วัดได้ 712.57px (เนื้อหาใน 632.57px) |
| ตำแหน่ง | จัดกลางจอทั้งสองแกน |

การ์ดมี annotation ใน Figma ว่า **Respondsive** (sic) — ยืดหยุ่นตามจอ ไม่ fix ความกว้าง

---

## 5. การ์ดแอป

ค่าใน Figma เป็น instance ที่ถูก **ย่อไว้ 89.3%** (147.422 / 165 = 0.8934) ตารางนี้แสดงทั้งสองค่า
คอลัมน์ token คือขนาดของ component ที่ 100% · คอลัมน์ Figma คือค่าที่ instance ในไฟล์ถูกย่อลงมา
**วิธี implement อยู่ในข้อ 5.1** — คิดจากความกว้างการ์ดจริง โดย cap ไม่ให้เกิน 100%

| ส่วน | ค่า token (100%) | ที่วัดได้ใน Figma (89.3%) |
|---|---|---|
| กล่องการ์ด | **165 × 165** · `aspect-ratio:1` | 147.422 × 147.422 |
| padding | **20px** (`Spacing/Spacing-4xl`) | 17.869px |
| radius | **8px** | 7.148px |
| โลโก้แอป | **50 × 50** | 44.673px |
| gap โลโก้ ↔ ข้อความ | **6px** (`Spacing/Spacing-md`) | 5.361px |
| ชื่อแอป | **24px** Med `#1f2937` | 21.44px |
| คำอธิบาย | **18px** Regular `#6b7280` | 16.08px |
| gap ระหว่างการ์ด | **16px** | 14.295px |
| จัดวางในการ์ด | `flex-direction:column` · `align-items:center` · **`justify-content:center`** · ข้อความ `text-align:center` |

**เนื้อหาในการ์ดจัดกลางทั้งแนวตั้งและแนวนอน** — logo · ชื่อแอป · คำอธิบาย อยู่กลางกล่องทั้งชุด
ไม่ใช้ `flex:1` กับคำอธิบายเพื่อดันลงล่าง

### 5.1 ขนาดเนื้อหาโตตามความกว้างการ์ด

การ์ดใน layout 3 คอลัมน์กว้างกว่า 4 คอลัมน์ เนื้อหาจึงต้องโตตาม **แต่ห้ามเกินค่า 100% ของ component**

```
typeBox = min(cardWidth, 165)          // cap ที่ขนาด component 100%
padding = round(typeBox × 0.1212)      // 20 / 165
logo    = round(typeBox × 0.303)       // 50 / 165
name    = round(typeBox × 0.1455)      // 24 / 165
desc    = round(typeBox × 0.1091)      // 18 / 165
gap     = round(typeBox × 0.0364)      //  6 / 165
```

| layout | ความกว้างการ์ด | padding | logo | ชื่อ | คำอธิบาย |
|---|---|---|---|---|---|
| 4 คอลัมน์ @1440 | 146px | 18 | 44 | 21 | 16 |
| 3 คอลัมน์ @1440 | 200px → cap 165 | 20 | 50 | **24** | **18** |
| 2 คอลัมน์ @375 | 148px | 18 | 45 | 21 | 16 |

โลโก้แอปเป็น **ไฟล์จริง** ห้ามใส่พื้นหลัง กรอบ หรือรีคัลเลอร์
ใช้ `<brand>-icon.svg` **ชุดเดียวกับที่ Choco และหน้า Brand ใช้** ไม่แยกไฟล์ของหน้านี้

```
assets/sellsuki-icon.svg   assets/akita-icon.svg
assets/patona-icon.svg     assets/oc2plus-icon.svg
assets/sellsukipay-icon.svg  assets/shipmunk-icon.svg
```

Logo บริษัทด้านบนใช้ `assets/sellsuki-icon.svg` ขนาด **50 × 50**
(ไฟล์ใน Figma เป็น 49.3 × 55.29 ซึ่งไม่ใช่สี่เหลี่ยมจัตุรัส — ไอคอนใน repo เป็นจัตุรัส จึงใช้ 50 × 50)

เนื้อหาที่อยู่ในไฟล์:

| แอป | ชื่อ | คำอธิบาย |
|---|---|---|
| Sellsuki | Sellsuki | จัดการบริษัทและผู้ใช้งาน |
| Akita | Akita | บริการคลังสินค้าครบวงจร |
| Patona | Patona | ผู้ช่วยของคนทำธุรกิจ |
| Oc2plus | Oc2plus | เครื่องมือจัดเก็บข้อมูล สำหรับวางแผนการตลาด |

---

## 6. Layout ของตาราง — 2 แบบ

ไฟล์ Figma มีสอง frame ตามจำนวนคอลัมน์

| Frame | grid | จำนวนแอปที่รองรับ |
|---|---|---|
| `App Selector 4x1` | `repeat(4, 1fr)` · 1 แถว | ไม่เกิน 4 |
| `App Selector 3x2` | `repeat(3, 1fr)` · 2 แถว | 5–6 |

ทั้งสอง frame มี slot การ์ดไว้ **8 ช่อง** และซ่อนแถวที่สองไว้ (`hidden`) — เลือกแบบตามจำนวนแอปที่ผู้ใช้มีสิทธิ์เข้า
ถ้าเกิน 6 ให้ขึ้นแถวที่สามด้วย grid เดิม ไม่ต้องเพิ่ม frame ใหม่

**เขียนเป็น grid ที่ยืดเอง** ดีกว่าไล่ทำสองแบบแยกกัน:

```css
[data-app-grid]{ display:grid; gap:16px; grid-template-columns:repeat(4, minmax(0,1fr)); }
[data-app-grid][data-cols="3"]{ grid-template-columns:repeat(3, minmax(0,1fr)); }
```

---

## 7. ปุ่ม Actions

เรียงซ้าย → ขวา: **ออกจากระบบ (solid-light)** → **ตั้งค่าบัญชี (solid)** ทั้งสองใบ `flex:1` กว้างเท่ากัน
ทั้งสองใบเป็น `<button>` **ที่กดได้จริง** ไม่ใช่ `<span>` ที่ทำหน้าตาเหมือนปุ่ม
การ์ดแอปก็เป็น `<button>` ที่กดแล้วไปแอปนั้น

| ส่วน | ค่า |
|---|---|
| ความสูงต่ำสุด | **44px** |
| padding | `10px 16px` |
| radius | **8px** (`Border-radius/radius-md`) |
| gap ไอคอน ↔ ข้อความ | **8px** (`Spacing/Spacing-lg`) |
| ไอคอน | **24 × 24** — `heroicons/arrow-right-on-rectangle` (ออกจากระบบ) · `heroicons/cog-8-tooth` (ตั้งค่าบัญชี) |
| ตัวอักษร | 24px Med · จัดกลาง · `white-space:nowrap` |
| ปุ่มรอง | พื้น `#ffffff` · ขอบ `1px solid #e5e7eb` · ตัวอักษร `#1f2937` |
| ปุ่มหลัก | พื้น `#32a9ff` · ขอบ `1px solid #32a9ff` · ตัวอักษร `#ffffff` |

```
assets/icon-logout.svg   assets/icon-cog.svg
```

---

## 8. ภาพประกอบพื้นหลัง

| ส่วน | ค่า |
|---|---|
| จำนวน | 2 ภาพ ขนาด **600 × 600** ต่อภาพ |
| ตำแหน่ง | ปักมุม **ล่างซ้าย** และ **ล่างขวา** ด้วย `align-items:flex-end` + `justify-content:space-between` |
| ตัวครอบ | `max-width:1920px` · `min-width:1280px` |
| object-fit | `cover` |
| pointer | `pointer-events:none` — ห้ามบังการคลิกการ์ด |
| ไฟล์ | `assets/app-selector-bg-left.png` · `assets/app-selector-bg-right.png` |

จอที่แคบกว่า 1280px ให้ **ซ่อนภาพประกอบ** แล้วเหลือแต่การ์ดกลางบนพื้น `#f9fafb`

---

## 9. Responsive

| ช่วงจอ | การ์ดกลาง | ตารางแอป | ภาพประกอบ | ปุ่ม | คำทักทาย / ข้อความนำ |
|---|---|---|---|---|---|
| ≥ 1280px | `min(712px, 100vw − 48)` · padding 32/40 | 4 หรือ 3 คอลัมน์ตามจำนวนแอป | แสดง | เรียงแนวนอน · 24px | 36 / 24 |
| 901–1279px | เท่าเดิม | เท่าเดิม | **ซ่อน** | เรียงแนวนอน · 24px | 36 / 24 |
| 721–900px | เท่าเดิม | **2 คอลัมน์** | ซ่อน | เรียงแนวนอน · 24px | 30 / 20 |
| ≤ 720px | `100vw − 24` · padding **24/20** · gap **24** | 2 คอลัมน์ | ซ่อน | **เรียงลง** · 20px | 24 / 18 |

```css
@media (max-width:1279px){
  [data-appsel-art]{ display:none !important; }
}
@media (max-width:900px){
  [data-app-grid]{ grid-template-columns:repeat(2, minmax(0,1fr)) !important; }
  [data-greet]{ font-size:30px !important; }
  [data-lead]{ font-size:20px !important; }
}
@media (max-width:720px){
  [data-card]{ padding:24px 20px !important; gap:24px !important; }
  [data-actions]{ flex-direction:column !important; }
  [data-greet]{ font-size:24px !important; }
  [data-lead]{ font-size:18px !important; }
  [data-actions] button{ font-size:20px !important; }
}
```

ค่าที่ **ไม่เปลี่ยน** ทุก breakpoint:
- ปุ่มสูงต่ำสุด **44px** · radius 8 · ไอคอน 24 · gap 8
- การ์ดแอปเป็น **สี่เหลี่ยมจัตุรัส** และ gap ระหว่างการ์ด **16px**
- ขนาดเนื้อหาในการ์ดแอปคิดจากสูตรข้อ 5.1 ตามความกว้างการ์ดที่ได้จริง ไม่ต้องเขียน media query แยก

## 10. พฤติกรรม

1. เข้าหน้านี้จากระบบกลางหลัง login สำเร็จ — ยังไม่มีบริบทของแอปใด จึงไม่มี shell
2. แสดง **ทุกแอปที่ผู้ใช้มีสิทธิ์เข้า** ไม่กรองแอปใดออก (ต่างจาก Choco ใน `AppTopNav.md` ที่ซ่อนแอปที่กำลังใช้อยู่)
3. คลิกการ์ด → ไปที่แอปนั้น
4. **ออกจากระบบ** → กลับหน้า login ของระบบกลาง
5. **ตั้งค่าบัญชี** → หน้าตั้งค่าบัญชีของระบบกลาง
6. ถ้าผู้ใช้มีสิทธิ์เข้าแอปเดียว ให้พาเข้าแอปนั้นทันที ไม่ต้องแสดงหน้านี้

---

## 11. ของที่ยังต้องยืนยัน

| เรื่อง | รายละเอียด |
|---|---|
| ขอบการ์ดแอป | Figma ผูก token `Colors/Stroke/stroke-primary` ไว้กับการ์ด แต่ตั้ง **border-width = 0** ขอบที่เห็นในภาพมาจากเงาชั้น `0 0 0.447px rgba(17,24,39,.09)` — ต้องยืนยันว่าจะให้เป็นขอบ 1px จริงหรือใช้เงาอย่างเดียว |
| การ์ดแอปถูกย่อ 89.3% | instance ในไฟล์ถูก scale ไว้ ไม่ใช่ค่า token ตรง ๆ ควรแก้ที่ Figma ให้ตรงกับ token หรือระบุว่า scale เป็นส่วนหนึ่งของ spec |
| สอง frame render เหมือนกัน | ทั้ง `3x2` และ `4x1` ตอนนี้ grid เป็น `repeat(4,1fr)` แถวเดียวเหมือนกัน ชื่อ frame บอกเจตนา แต่ค่าจริงยังไม่ต่าง — ต้องแก้ frame `3x2` ให้เป็น 3 คอลัมน์ |
| state ของการ์ด | ยังไม่มี hover / focus / disabled ในไฟล์ — ต้องออกแบบเพิ่ม (แนะนำ hover ยกเงาขึ้น + ขอบเป็นสีแบรนด์ ตาม "ตัวเลือกแบบการ์ด" ใน `oc2plus-create-page.md`) |
| `one-finger-long-tap` | frame `4x1` มี instance ชื่อนี้วางอยู่ เป็น prototype hint ไม่ใช่ UI จริง — ไม่ต้อง implement |
| ภาษา | ข้อความในไฟล์เป็นไทยทั้งหมด ต้องเตรียม key สำหรับ English ตามที่ระบบรองรับ 2 ภาษา |

---

## 12. เช็กลิสต์

- [ ] พื้นหน้า `#f9fafb` · การ์ดกลางขาว radius 12 padding 32/40 gap 32 + `shadow-sm`
- [ ] การ์ดกลางจัดกลางจอทั้งสองแกน
- [ ] logo บริษัท 49.3 × 55.29 อยู่บนสุด จัดกลาง
- [ ] "สวัสดี!," 36px Bold `#1f2937` + ชื่อผู้ใช้ 36px Bold `#32a9ff` · gap 8
- [ ] ข้อความนำ 24px Med `#1f2937`
- [ ] การ์ดแอปเป็นสี่เหลี่ยมจัตุรัส · padding 20 · radius 8 · โลโก้ 50 · ชื่อ 24px Med · คำอธิบาย 18px Regular `#6b7280`
- [ ] gap ระหว่างการ์ด 16px · grid `1fr` เท่ากันทุกใบ
- [ ] โลโก้แอปใช้ไฟล์จริง ไม่ใส่พื้นหลัง/กรอบ/รีคัลเลอร์
- [ ] แสดงทุกแอปที่มีสิทธิ์ ไม่กรองออก
- [ ] ปุ่มสองใบ `flex:1` เท่ากัน · สูง 44 · radius 8 · ไอคอน 24 · gap 8 · ตัวอักษร 24px Med
- [ ] ลำดับปุ่ม ออกจากระบบ (solid-light) → ตั้งค่าบัญชี (solid)
- [ ] ภาพประกอบ 600×600 ปักมุมล่างสองข้าง · `pointer-events:none` · ซ่อนใต้ 1280px
- [ ] media query ข้อ 9 ครบ · ปุ่มยัง 44px ทุก breakpoint
- [ ] ตัวอักษรไม่ต่ำกว่า 18px
- [ ] ไอคอนใช้ไฟล์ที่ export จาก Figma ไม่วาดเอง
