# 🌱 ProjectSmartFram — ระบบจัดการฟาร์มอัจฉริยะ

> ระบบจัดการและมอนิเตอร์ฟาร์มอัจฉริยะ (Smart Farm) แบบครบวงจร  
> รองรับการดูข้อมูลเซ็นเซอร์แบบ **Real-time**, ระบบสั่งการปั๊มน้ำอัตโนมัติ และการจัดการข้อมูลผ่าน Dashboard

🔗 [ดูสไลด์นำเสนอโปรเจกต์ (Canva)](https://canva.link/a4iad7hhi1i5vl6) &nbsp;|&nbsp;
🎥 [วิดีโอตัวเต็ม (Full VDO)](https://youtu.be/61h8lNIio6U) &nbsp;|&nbsp;
📱 [วิดีโอสั้น (Short VDO)](https://vt.tiktok.com/ZS9et9dQV/)

---

## 📋 สารบัญ

- [Tech Stack](#-tech-stack)
- [Features หลัก](#-features-หลัก)
- [โครงสร้างโปรเจกต์](#-โครงสร้างโปรเจกต์)
- [การติดตั้ง (Setup Guide)](#️-การติดตั้ง-setup-guide)
- [Account สำหรับ Login](#-account-สำหรับ-login)
- [Business Rules](#️-business-rules)
- [หมายเหตุสำคัญ](#️-หมายเหตุสำคัญ)
- [ทีมพัฒนา](#-ทีมพัฒนา)

---

## 💻 Tech Stack

| ส่วน | เทคโนโลยี |
| :--- | :--- |
| **Backend** | Node.js (Express) |
| **Database** | MySQL 8.0 |
| **Frontend** | HTML5, CSS3, JavaScript (Vanilla), Chart.js |
| **Infrastructure** | Docker, Docker Compose |
| **Hardware / IoT** | ESP32, เซ็นเซอร์ความชื้นดิน, อุณหภูมิ, แสง |

---

## ✨ Features หลัก

| Feature | รายละเอียด |
| :--- | :--- |
| 📊 **Dashboard Real-time** | แสดงผลค่าความชื้นดิน, อุณหภูมิ, แสงสว่าง พร้อม Badge แจ้งเตือนสถานะ |
| 💧 **ระบบควบคุมปั๊มน้ำ** | รองรับการรดน้ำอัตโนมัติ (Auto) ตามค่าความชื้น และรดน้ำด้วยมือ (Manual) |
| 📈 **ประวัติและวิเคราะห์** | ดึงข้อมูลย้อนหลังมาแสดงผลเป็นกราฟ |
| 📱 **จัดการอุปกรณ์** | เชื่อมต่อและลงทะเบียน MAC Address ของบอร์ด ESP32 เข้ากับแปลงปลูก |
| 👥 **ระบบสมาชิก** | Login, แบ่งสิทธิ์การเข้าถึงฟาร์ม (OWNER / MEMBER) |

---

## 📁 โครงสร้างโปรเจกต์

```
ProjectSmartFram/
├── backend/
│   ├── server.js         # ไฟล์รันเซิร์ฟเวอร์หลัก (API + Database)
│   └── package.json
├── frontend/
│   ├── index.html        # หน้า Dashboard หลัก
│   └── simulator.html    # จำลองการส่งข้อมูลเซ็นเซอร์จาก ESP32
├── docker-compose.yml    # ตั้งค่า Docker (Node.js + MySQL + phpMyAdmin)
├── .env                  # ตัวแปรสภาพแวดล้อม (ไม่ push ขึ้น GitHub)
└── README.md
```

---

## ⚙️ การติดตั้ง (Setup Guide)

### สิ่งที่ต้องติดตั้งก่อน

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Git](https://git-scm.com/)

---

### ขั้นตอนที่ 1 — Clone โปรเจกต์

```bash
git clone https://github.com/your-username/ProjectSmartFram.git
cd ProjectSmartFram
```

### ขั้นตอนที่ 2 — ตั้งค่าไฟล์ `.env`

สร้างไฟล์ `.env` ในโฟลเดอร์หลัก แล้วกำหนดค่าดังนี้:

```env
PORT=3000
DB_HOST=mysql
DB_PORT=3306
DB_USER=greenspace_user
DB_PASSWORD=greenspace_pass
DB_NAME=greenspace_db
JWT_SECRET=ใส่รหัสลับของคุณที่นี่
```

> ⚠️ **ห้าม** push ไฟล์ `.env` ขึ้น GitHub โดยเด็ดขาด

### ขั้นตอนที่ 3 — รันระบบด้วย Docker Compose

```bash
docker compose up -d --build
```

คำสั่งนี้จะสร้างและเปิดใช้งาน Backend และ Database พร้อมกัน

### ขั้นตอนที่ 4 — เข้าใช้งานระบบ

| บริการ | URL |
| :--- | :--- |
| **Web Dashboard** | http://localhost:3000 |
| **phpMyAdmin** | http://localhost:8080 |

---

## 👤 Account สำหรับ Login

| Username | Password | Role | สิทธิ์การใช้งาน |
| :--- | :--- | :--- | :--- |
| `admin` | `1234` | OWNER | จัดการทุกส่วนในระบบ / จัดการสมาชิกฟาร์ม |
| `gigi2` | `1234` | MEMBER | ดูข้อมูล Dashboard / สั่งรดน้ำด้วยมือ |

---

## ⚖️ Business Rules

| กิจกรรม | กฎการทำงาน |
| :--- | :--- |
| **การรดน้ำ (Auto)** | ปั๊มน้ำทำงานอัตโนมัติเมื่อค่าความชื้นดินต่ำกว่าเกณฑ์ที่ตั้งไว้ใน Settings |
| **การรดน้ำ (Manual)** | ผู้ใช้สั่งเปิดปั๊มน้ำได้ทันทีจาก Dashboard พร้อมกำหนดระยะเวลาเอง |
| **สถานะอุปกรณ์** | แสดงสถานะ Online เมื่อมีการส่งข้อมูลจาก ESP32 เข้ามาภายใน 5 นาทีล่าสุด |
| **ความปลอดภัย** | เฉพาะผู้ใช้ที่มี Token ถูกต้อง (ผ่าน Login) เท่านั้นที่แก้ไขตั้งค่าอุปกรณ์ได้ |
| **การเก็บข้อมูล** | บันทึก Log สภาพแวดล้อมทุกครั้งที่มีการส่งค่าเข้ามา และบันทึกประวัติการปั๊มน้ำทุกครั้งที่ปั๊มทำงาน |

---

## ⚠️ หมายเหตุสำคัญ

- **ไฟล์ `.env`** — ห้าม push ขึ้น GitHub เพื่อป้องกันรหัสผ่านฐานข้อมูลรั่วไหล ให้เพิ่ม `.env` ใน `.gitignore`
- **พอร์ต** — ตรวจสอบว่าไม่มีโปรแกรมอื่นรันที่พอร์ต `3000`, `3306` และ `8080` ก่อนสั่ง `docker compose up`
- **การรีเซ็ตข้อมูล** — หากต้องการล้างฐานข้อมูลทั้งหมด ใช้คำสั่ง:
  ```bash
  docker compose down -v
  ```
  > ⚠️ **ระวัง!** ข้อมูลทั้งหมดจะหายถาวร
- **Simulator** — ในหน้า `simulator.html` ให้ตั้งค่า API Endpoint ให้ตรงกับพอร์ตของ Backend (เช่น `localhost:3000`)

---

## 👨‍💻 ทีมพัฒนา

โปรเจกต์นี้เป็นส่วนหนึ่งของวิชา:
- **ICT22467** — ระบบฐานข้อมูล (DataBase)
- **CPE23567** — ระบบปฏิบัติการ (Operating System)

**มหาวิทยาลัยศรีปทุม (Sripatum University)**

| รหัสนักศึกษา | ชื่อ |
| :--- | :--- |
| 67157464 | โกวิท คำชั่ง |
| 67176861 | นราพรรณ รองราช |
| 67162014 | อธิป ซิวเซ่ง |
| 67161088 | วศินี บัวทอง |
