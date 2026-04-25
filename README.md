# 🌱 ProjectSmartFram (ระบบจัดการฟาร์มอัจฉริยะ)

> *This is our project for study.*
> ระบบจัดการและมอนิเตอร์ฟาร์มอัจฉริยะ (Smart Farm) แบบครบวงจร 
> รองรับการดูข้อมูลเซ็นเซอร์แบบ **Real-time**, ระบบสั่งการปั๊มน้ำอัตโนมัติ และการจัดการข้อมูลผ่าน Dashboard

🔗 **[ดูสไลด์นำเสนอโปรเจกต์ (Canva) คลิกที่นี่](https://canva.link/a4iad7hhi1i5vl6)**
🎥 **[รับชมวิดีโอตัวเต็ม (Full VDO)](https://youtu.be/61h8lNIio6U)**
📱 **[รับชมวิดีโอสั้น (Short VDO)](https://vt.tiktok.com/ZS9et9dQV/)**

---

## 💻 Tech Stack

| ส่วน | เทคโนโลยี |
| :--- | :--- |
| **Backend** | Node.js (Express) |
| **Database** | MySQL 8.0 |
| **Frontend** | HTML5, CSS3, JavaScript (Vanilla), Chart.js |
| **Infrastructure**| Docker, Docker Compose |
| **Hardware/IoT** | ESP32, เซ็นเซอร์ความชื้นดิน, อุณหภูมิ, แสง |

---

## ⚙️ การติดตั้ง (Setup Guide)

### ✅ สิ่งที่ต้องมีก่อน

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (สำหรับรันเซิร์ฟเวอร์จำลอง)
- [Git](https://git-scm.com/) สำหรับดึงโค้ด

---

### 📥 ขั้นตอนที่ 1 - Clone โปรเจค

```bash
git clone [https://github.com/your-username/ProjectSmartFram.git](https://github.com/your-username/ProjectSmartFram.git)
cd ProjectSmartFram

### ขั้นตอนที่ 2 - ตั้งค่าไฟล์ .env
สร้างไฟล์ .env ในโฟลเดอร์หลัก และกำหนดค่าพื้นฐานดังนี้:
PORT=3000
DB_HOST=mysql
DB_PORT=3306
DB_USER=greenspace_user
DB_PASSWORD=greenspace_pass
DB_NAME=greenspace_db
JWT_SECRET=ใส่รหัสลับของคุณที่นี่

### ขั้นตอนที่ 3 - รันระบบ (Docker Compose)
เปิด Terminal แล้วรันคำสั่งด้านล่างนี้ เพื่อสร้างและเปิดใช้งาน Backend และ Database ไปพร้อมๆ กัน:
Bash
docker compose up -d --build

### ขั้นตอนที่ 4 - การเข้าใช้งาน
เมื่อระบบทำงานสมบูรณ์แล้ว สามารถเข้าถึงบริการต่างๆ ได้ตามช่องทางนี้:
Web Dashboard (หน้าเว็บหลัก): เปิดไฟล์ index.html หรือเข้าผ่าน http://localhost:3000
ระบบจัดการฐานข้อมูล (phpMyAdmin): เข้าผ่าน http://localhost:8080

|Username | Password | Role | สิทธิ์การใช้งาน
| :----- | :----- | :----- | :----- |
| admin | 1234 | OWNER | จัดการทุกส่วนในระบบ / จัดการสมาชิกฟาร์ม |
| gigi2 | 1234 | MEMBER | ดูข้อมูลแดชบอร์ด / สั่งรดน้ำด้วยมือ |

ProjectSmartFram/
├── backend/              - โค้ดส่วนจัดการ API (Node.js) และเชื่อมต่อ Database
│   ├── server.js         - ไฟล์รันเซิร์ฟเวอร์หลัก
│   └── package.json
├── frontend/             - ไฟล์หน้าเว็บ Dashboard
│   ├── index.html        - หน้าจัดการฟาร์มหลัก
│   └── simulator.html    - หน้าสำหรับจำลองการส่งข้อมูลเซ็นเซอร์จาก ESP32
├── docker-compose.yml    - ไฟล์ตั้งค่าสำหรับรัน Docker (Node + MySQL)
└── README.md             - คู่มือและรายละเอียดของโปรเจกต์

Features หลัก
📊 Dashboard Real-time - แสดงผลค่าความชื้นดิน, อุณหภูมิ, แสงสว่าง พร้อม Badge แจ้งเตือนสถานะ
💧 ระบบควบคุมปั๊มน้ำ (Watering System) - รองรับการสั่งรดน้ำอัตโนมัติ (Auto) ตามค่าความชื้น และรดน้ำด้วยมือ (Manual)
📈 ประวัติและวิเคราะห์ (History & Analytics) - ดึงข้อมูลย้อนหลังมาแสดงผลเป็นกราฟสวยงาม
📱 จัดการอุปกรณ์ (Device Management) - เชื่อมต่อและลงทะเบียน MAC Address ของบอร์ด ESP32 เข้ากับแปลงปลูก
👥 ระบบสมาชิก (Farm Members) - มีระบบ Login สมาชิก และแบ่งสิทธิ์เข้าใช้งานฟาร์ม

## ⚖️ Business Rules
กิจกรรมรายละเอียดกฎการทำงานการรดน้ำ (Auto)ปั๊มน้ำจะทำงานโดยอัตโนมัติเมื่อค่าความชื้นดินต่ำกว่าเกณฑ์ที่ตั้งไว้ในหน้า Settings
การรดน้ำ (Manual)ผู้ใช้สามารถสั่งเปิดปั๊มน้ำได้ทันทีจากหน้า Dashboard โดยกำหนดระยะเวลาการทำงานได้เอง
สถานะอุปกรณ์ระบบจะแสดงสถานะ Online เมื่อมีการส่งข้อมูลจาก ESP32 เข้ามาล่าสุดภายใน 5 นาที
ความปลอดภัยเฉพาะผู้ใช้ที่มี Token ถูกต้อง (ผ่านการ Login) เท่านั้นที่สามารถแก้ไขการตั้งค่าอุปกรณ์ได้
การเก็บข้อมูลระบบจะบันทึก Log สภาพแวดล้อมทุกครั้งที่มีการส่งค่าเข้ามา และบันทึกประวัติการปั๊มน้ำทุกครั้งที่ปั๊มทำงาน

## ⚠️ หมายเหตุ (Important Notes)
ไฟล์ .env: ห้ามอัปโหลด (Push) ขึ้น GitHub โดยเด็ดขาดเพื่อความปลอดภัยของรหัสผ่านฐานข้อมูล
พอร์ตการใช้งาน: ตรวจสอบให้แน่ใจว่าไม่มีโปรแกรมอื่นรันอยู่ที่พอร์ต 3000, 3306 และ 8080 ก่อนสั่งรัน Docker
การรีเซ็ตข้อมูล: หากต้องการล้างข้อมูลในฐานข้อมูลทั้งหมด สามารถใช้คำสั่ง docker compose down -v ได้ (ระวัง! ข้อมูลจะหายถาวร)
การจำลองข้อมูล: ในหน้า simulator.html ควรตั้งค่า API Endpoint ให้ตรงกับพอร์ตที่ Backend รันอยู่จริง (เช่น localhost:3000)

## 👨‍💻 ทีมพัฒนา (Development Team)
โปรเจกต์นี้เป็นส่วนหนึ่งของวิชา ICT22467: ระบบฐานข้อมูล  และ CPE23567: ระบบปฏิบัติการ (Operating System) * มหาวิทยาลัยศรีปทุม (Sripatum University)
67157464 โกวิท คำชั่ง
67176861 นราพรรณ รองราช
67162014 อธิป ซิวเซ่ง
67161088 วศินี บัวทอง
