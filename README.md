# ⚔️ ROV Draft Pro — Setup Guide

## โครงสร้างโปรเจกต์
```
rov-draft/
  frontend/          ← React (Vite)
    src/App.jsx
    .env             ← ใส่ VITE_API_URL
  backend/           ← Node.js + Express + MongoDB
    src/index.js
    .env             ← ใส่ MONGODB_URI
```

---

## 1. ติดตั้ง Backend

```bash
cd backend
npm install

# สร้างไฟล์ .env
cp .env.example .env
# แก้ MONGODB_URI ให้ตรงกับ MongoDB ของคุณ

npm run dev        # dev mode (nodemon)
# หรือ
npm start          # production
```

### MongoDB ฟรีด้วย MongoDB Atlas
1. ไปที่ https://cloud.mongodb.com
2. สร้าง Free Cluster
3. กด Connect → Drivers → Copy connection string
4. ใส่ใน `.env` → `MONGODB_URI=mongodb+srv://...`

---

## 2. ติดตั้ง Frontend

```bash
cd frontend
npm install

# สร้างไฟล์ .env
cp .env.example .env
# แก้ VITE_API_URL ให้ตรงกับ backend

npm run dev        # dev mode
npm run build      # build สำหรับ production
```

---

## 3. Deploy ขึ้น Server จริง

### Backend → Railway (ฟรี)
1. https://railway.app → New Project → Deploy from GitHub
2. ใส่ environment variables: `MONGODB_URI`, `PORT`
3. จะได้ URL เช่น `https://rov-draft-api.railway.app`

### Frontend → Vercel (ฟรี)
1. https://vercel.com → New Project → Import GitHub
2. ใส่ environment variable: `VITE_API_URL=https://rov-draft-api.railway.app`
3. Deploy

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | /api/heroes | ดึงฮีโร่ทั้งหมด |
| GET | /api/heroes/:id | ดึงฮีโร่ตัวเดียว |
| POST | /api/heroes | เพิ่มฮีโร่ (multipart/form-data) |
| PUT | /api/heroes/:id | แก้ไขฮีโร่ |
| PATCH | /api/heroes/:id/relations | แก้ counter/synergy |
| DELETE | /api/heroes/:id | ลบฮีโร่ |

### ตัวอย่าง POST hero
```
POST /api/heroes
Content-Type: multipart/form-data

name: "Nakroth"
role: ["Assassin"]
tier: "S"
emoji: "😈"
color: "#f87171"
image: <file>
```
