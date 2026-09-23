repo: BearyCenter/sellsuki.design
branch: main

## Last sync
date: 2026-08-19T07:29:07Z
deploy: https://vercel.com/sellsuki1/sellsuki-design

### Updated in this project
- sellsuki.design.dc.html — หน้า library asset 10 หน้า, header รวมเมนู dropdown, home layout ใหม่
- index.html — redirect จาก root ไปหน้าหลัก (Vercel static)
- assets/ — brand mark SVG จาก DS 2.0

## Screen map
| screen | built from |
|---|---|
| ทุกหน้า (Overview, Set up, Tokens, Brand, Assets, Skills, Design system, Component library, Storybook, Patterns, App Shell example, Design check) | sellsuki.design.dc.html |
| runtime | support.js |

## Sync history
- 2026-09-10 — แยก Widget Layout ออกเป็น sub-pattern ของ Detail page (widget-layout-110) แทนที่จะยัดไว้ใน
  Detail page — PATTERNS รองรับ field `parent` แล้ว (rail เยื้อง + เส้นซ้าย · การ์ด index ติดป้าย "sub-pattern
  ของ …" · หัวหน้า detail มีปุ่มลิงก์กลับไป pattern แม่) Detail page กลับไปจบที่ header เหมือนเดิม
  เพิ่มตัวอย่าง 2 แบรนด์ — oc2plus = Member detail, patona = รายละเอียดออเดอร์ โดยยกเฉพาะ "ข้อมูล" จาก
  Order Detail.dc.html (scenario ชำระแล้ว/CLOSED) ไม่ได้ลอก UI มาเลย ส่วนหน้าตาใช้ widget ของ DS 2.0
  และบันทึกไว้ใน WL_CONFLICTS ว่าหน้าจริงนั้นยังไม่ตรงสเปก (คอลัมน์ 300px คงที่ · gap 20 · radius 12 ·
  ตัวอักษร 14–17px · ไม่ติด data-grid/data-widget)
- 2026-09-10 — Detail page: เพิ่มระบบ Widget composition สำหรับ data-body จาก Body_Content_Pattern.md +
  Body_Widget_Pattern.md (สองไฟล์อธิบายระบบเดียวกันแต่ขัดกันเอง — data-grid string ratio vs
  grid-template-columns ต่อแถว, ชื่อ widget ไม่ตรงกัน (fields vs info), gap/radius ไม่เท่ากัน — เอกสารทั้งหมด
  บันทึกไว้ใน DETAIL_CONFLICTS ตัดสินใช้ Body_Widget_Pattern.md เป็นหลักเพราะกัน overflow ได้ตรงกว่า)
  เพิ่มตาราง Grid ratio (12/6:6/8:4/4:4:4/3:3:3:3) + Widget catalog (info/stat/table/timeline/form/
  preview/toolbar) ในหน้า "โครงสร้าง" และแทนที่ placeholder data-body เดิมด้วยตัวอย่าง Member detail จริง
  (8:4 grid — toolbar+stat×2+table ซ้าย, info×3 ขวา) ตามตัวอย่างใน Body_Content_Pattern.md §5
- 2026-09-09 — Features & Services เพิ่ม scenario ที่ 3 "ตั้งค่า Theme" (brand oc2plus คงที่) ย่อจากไฟล์จริง
  ที่ผู้ใช้ส่งมา (OC-4246 Theme Settings Shell.dc.html) — ตัด search/filter/pagination และหน้า create/edit
  ที่มี live preview ออกทั้งหมด (ไม่ใช่โครง Card 1/2 ของ pattern นี้) เหลือเฉพาะตาราง Theme + toggle active
  ต่อแถว พร้อม confirm modal เปิด/ปิดที่ก็อปปี้ข้อความจริงจากไฟล์ (CONFIRM.activate/deactivate) — กติกาต่าง
  จาก slip/payment ตรงที่เปิด Active ได้พร้อมกันหลาย Theme จึงไม่มี Card 2 และไม่มี verb สลับ
- 2026-09-09 — Features & Services: ย้อนตัวสลับแบรนด์ (oc2plus/patona toolbar) ออก — ตรวจสอบสลิป และ
  โหมดการชำระเงิน เป็นหน้าจริงของ Sellsuki เท่านั้น (อ้างอิงตัวอย่างจริงจากระบบ Patona ที่ผู้ใช้ส่งมา
  ยืนยันว่า pattern นี้ implement แยกต่อแบรนด์ ไม่ได้ใช้ token switch ข้ามแบรนด์แบบ pattern อื่น)
  hasBrandSwitch กลับเป็น false, โลโก้/ชื่อบริษัทในตัวอย่างคงที่เป็น Sellsuki
  — รอเนื้อหาจริงจาก OC-4089 Consent Config เพื่อเพิ่ม scenario ที่ 3 "ตั้งค่า Theme" (brand oc2plus)
- 2026-09-09 — Features & Services เพิ่ม service switcher (ตรวจสอบสลิป ⇄ โหมดการชำระเงิน — สถานะแยกกันคนละ
  service ไม่ทับกัน) และเปิด brand token switch แบบเดียวกับ pattern อื่น (oc2plus/patona toolbar, Instance ID,
  โลโก้/ชื่อระบบ/สีปุ่มหลักในตัวอย่างเปลี่ยนตาม brand ที่เลือก) — ปรับ hasBrandSwitch เป็น true และย้าย
  FS_PROVIDERS/FS_ACCOUNTS เดิมเข้า FS_SCENARIOS (slip/payment) ต่อ service
- 2026-09-09 — เพิ่ม pattern ใหม่ Features & Services (`features-services-109`) จาก Features&Services-pattern.md
  สกัดจาก Payment Mode (PAT-2425) และ Slip Verification — การ์ด 1 "บริการ" (current state card + options list
  เลือกผู้ให้บริการ ปุ่มเชื่อมต่ออยู่ที่แถวตัวเลือกเสมอ) + การ์ด 2 "การตั้งค่าการใช้งาน" (master switch + ตาราง
  row switch ต่อบัญชี, render เฉพาะตอนเชื่อมต่อแล้ว) พร้อม confirm modal ทุกจุดที่กระทบระบบอื่น
  (เชื่อมต่อ/สลับผู้ให้บริการ/ยกเลิกการเชื่อมต่อ) ตัวอย่างกดเล่นได้จริงด้วย mock Slip2Go / KBank OCR / SCB Connect
- 2026-09-08 — ตรวจ App Shell กับ @sellsuki-org/sellsuki-components@0.27.1 จริง (npm registry, ไม่ใช่ assumption):
  Sidebar 256⇄92px/grid auto 1fr auto/padding {spacing-2xl} 18px ตรงกับ component จริงอยู่แล้ว ไม่ต้องแก้
  แต่ Topnav ของ App Shell (ทั้งใน pattern detail และหน้า `pattern-example` เต็มจอ) ใช้มาร์กอัปคนละแบบกับ
  pattern App Topnav (56px แบบ 3-slot ทั่วไป vs 64px แบบ 7 ส่วนจริง) — แก้ให้ App Shell ใช้
  <ssk-top-navbar> ตัวเดียวกับ App Topnav ทุกที่ (64px, hamburger→logo→system name→spacer→
  search·bell·apps(Choco)·avatar) พร้อมอัปเดตตัวเลข 56px/65px ที่ค้างอยู่ใน anatomy/checklist/gap
  notes ของ App Shell, List page, Detail page ให้เหลือ 64px ค่าเดียวกันทั้งระบบ
- 2026-09-01 — แก้ที่ repo ตรง ๆ ไม่ได้ sync มาจาก canvas: เปิดหน้า Patterns (เดิมเป็น stub ติดป้าย soon)
  ด้วยเนื้อหาจริงจาก Design_Patterns_2.0.md เพิ่ม pattern Topnav / List / Create-Edit / Detail page จากเอกสาร oc2plus
  และ App Selector ที่ implement จาก Figma CCS-2025 node 8413-22617 (spec อยู่ที่ app-selector-pattern.md)
  และเพิ่ม route ใหม่ `pattern-example`
  ⚠️ ถ้า sync จาก Claude Design canvas ทับลงมาอีกครั้ง การแก้รอบนี้จะหายไป — ต้อง merge เข้า canvas ก่อน
- 2026-08-19 — push ครั้งแรกจาก BearyCenter/sellsuki.design (ก่อนหน้านี้ระบุ repo Watcharapong-cmd/sellsuki.design)
