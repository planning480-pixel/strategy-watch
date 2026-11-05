# Excise Strategy Watch 2570–2574

เว็บรับฟังความเห็นบุคลากรกรมสรรพสามิตต่อร่างแผนยุทธศาสตร์ ปี 2570–2574
(ให้คะแนน 18 กลยุทธ์ · สรุปผลรายภาค/พื้นที่/ส่วนกลาง · ไม่เก็บชื่อผู้ให้ความเห็น)

## ไฟล์
- `index.html` — ตัวเว็บทั้งหมด (ไฟล์เดียว) ขึ้นบน Vercel
- `firestore.rules` — กฎความปลอดภัยของฐานข้อมูล ใช้คัดลอกไปวางใน Firebase Console > Firestore > Rules

## การตั้งค่า
แก้ในกล่อง `window.SW_CONFIG` ด้านบนสุดของ `index.html`
- `FIREBASE` — รหัสเว็บแอปจาก Firebase (เว้นว่าง = โหมดตัวอย่าง เก็บในเบราว์เซอร์)
- `SHOW_SETTINGS` — `true` แสดงเมนูตั้งค่า / `false` เอาออก

## Firebase ที่ต้องเปิด
- Firestore (asia-southeast1) + วาง `firestore.rules`
- Authentication > Anonymous
- Composite indexes บนคอลเลกชัน `votes`
  1. hasComment ↑, hidden ↑, updatedAt ↓
  2. strategyId ↑, hasComment ↑, hidden ↑, updatedAt ↓
  3. unitId ↑, hasComment ↑, hidden ↑, updatedAt ↓

## การดูแล (ไม่มีหน้าตั้งค่าบน Vercel)
- ซ่อนความเห็น: Firestore > `votes` > เอกสาร > ตั้ง `hidden` = `true`
- ปิดรับคะแนน: สร้างเอกสาร `config/settings` ใส่ฟิลด์ `open` = `false`

อัปเดตเว็บ: อัปโหลด `index.html` ใหม่ทับใน GitHub แล้ว Vercel จะ deploy ให้อัตโนมัติ
