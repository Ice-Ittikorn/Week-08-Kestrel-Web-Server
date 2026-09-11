#### [Checkpoint 1.1 ทดสอบความเข้าใจ]
1. ในหน้าจอ Terminal ขณะที่เซิร์ฟเวอร์กำลังรันอยู่ ให้กดปุ่ม `Ctrl + C` เพื่อหยุดโปรแกรม
2. กลับไปที่หน้าเบราว์เซอร์แล้วกดปุ่ม **Refresh (F5)** สังเกตว่าเกิดอะไรขึ้น และอธิบายสั้นๆ ว่าทำไมจึงเป็นเช่นนั้น
   - **คำตอบ** ไม่สามารถเปิดได้ เพราะ หยุดรัน server ไปแล้ว
#### กิจกรรมที่ 2 โครงสร้างและเขียนโค้ด
<img width="705" height="191" alt="image" src="https://github.com/user-attachments/assets/c6a76a8e-eb44-40ef-a861-9eff6023e280" />

## ภารกิจท้าทาย (Micro-Challenge)
 <img width="694" height="274" alt="image" src="https://github.com/user-attachments/assets/cb0118c6-d3b9-4907-8467-8c091261a390" />

## คำถามท้ายการทดลอง (Review Questions)
1. ในสถาปัตยกรรมของ Kestrel ตัวแปร `builder` ทำหน้าที่อะไร และตัวแปร `app` ทำหน้าที่อะไร
  - builder คือตัวตั้งค่าแอปก่อน build ใช้ลงทะเบียน service, configuration, logging, ตั้งค่า Kestrel 
  - app คือแอปที่ build เสร็จเเล้วพร้อมรัน ใช้กำหนด middleware, route และสั่งเริ่มเซิร์ฟเวอร์ด้วย app.Run()
2. เปรียบเทียบความสะดวกระหว่างการสร้าง Web Server บน .NET Minimal API กับการรันผ่าน LAMP Stack (Apache + PHP) ว่ามีข้อดีข้อเสียต่างกันอย่างไรในมุมมองของงาน IoT Gateway
  - Minimal API บน Kestrel เซตอัปเร็ว โค้ดน้อย เป็น async เบา เหมาะกับอุปกรณ์ทรัพยากรจำกัด จัดการ connection พร้อมกันจากหลายเซนเซอร์ได้ดี เชื่อมกับ protocol อื่นเช่น Serial, BLE, MQTT ในโค้ดเดียวกันได้สะดวก
  - LAMP ต้องติดตั้งและ config Apache แยกจากโค้ด PHP กิน resource ต่อ request มากกว่า ไม่เหมาะกับงาน real time เท่า แต่คุ้นเคยง่ายกว่าสำหรับงานเว็บทั่วไปและมี community ใหญ่กว่า
3. นักศึกษาคิดว่าการเพิ่ม `/api/` เข้าไปใน route นั้นมีประโยชน์อย่างไรบ้าง ถ้าไม่ใส่จะเกิดปัญหาอะไรบ้าง
  - ถ้าใส่ /api/ แยกชัดระหว่าง endpoint ที่เป็นข้อมูล กับหน้าเว็บหรือไฟล์ static ตั้ง middleware, auth, หรือ rate limit เฉพาะกลุ่ม /api/ ได้ง่าย รองรับการทำ reverse proxy หรือแยก backend ในอนาคต กันไม่ให้ route ชนกับชื่อไฟล์ static 
  - ถ้าไม่ใส่ /api/ อาจเกิดปัญหา route ชนกับไฟล์ static ที่ชื่อเดียวกัน แยกยากว่า endpoint ไหนคืนข้อมูล endpoint ไหนคืนหน้าเว็บ ตั้ง security หรือ middleware เฉพาะกลุ่มยากขึ้น ขยายระบบภายหลัง เช่นทำ versioning /api/v1/ ทำได้ลำบากกว่า
