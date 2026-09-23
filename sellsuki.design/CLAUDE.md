# Project notes

## Typography — overrides the design system's 18px floor

โปรเจกต์นี้ย้ายจาก DB HeaventRounded มาใช้ **Noto Sans Thai** เป็น font หลักแล้ว
กฎ "ขนาดต่ำสุด 18px / data 20px" ของ Sellsuki DS 2.0 ผูกกับ HeaventRounded (x-height เล็กกว่ามาก)
**ไม่ใช้กับโปรเจกต์นี้** — อย่ายกกฎนั้นมาเป็น defect หรือดันขนาดขึ้นกลับไปเอง

Type scale ที่ใช้จริง (ยึดอันนี้เป็นเกณฑ์):

| role | size |
|---|---|
| hero | 30px |
| page title | 24px |
| section | 20px |
| card header | 18px |
| body / data | 16px |
| label · meta · badge · button | 15px |

ส่วนอื่นของ DS 2.0 (สี, spacing, radius, border, component pattern, iconography) ยังบังคับใช้ตามปกติ
