# 🚗 RideWave Nepal — Full-Stack Carpooling Platform

> **Stack:** HTML + CSS (Frontend) · Node.js + Express + Socket.io (Backend) · MySQL (Database)
> **Currency:** NPR — Nepali Rupees
> **Driver Demo:** Nishan Karki

---

## 📁 Project Structure

```
ridewave/
├── frontend/
│   ├── index.html          ← Main page (all sections)
│   ├── css/
│   │   └── style.css       ← All styles
│   └── js/
│       └── app.js          ← All frontend logic + API calls (NPR)
│
├── backend/
│   ├── server.js           ← Express + Socket.io entry point
│   ├── package.json
│   ├── .env.example        ← Copy to .env and fill in values
│   ├── config/
│   │   └── db.js           ← MySQL connection pool
│   ├── middleware/
│   │   └── auth.js         ← JWT authenticate + authorize
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── bookingController.js   ← Fares in NPR
│   │   ├── paymentController.js   ← Currency: NPR
│   │   ├── ratingController.js
│   │   ├── chatController.js
│   │   └── gpsController.js
│   └── routes/
│       └── index.js
│
└── database/
    └── schema.sql          ← Full MySQL schema
```

---

## ⚙️ Quick Setup

### 1. MySQL
```bash
mysql -u root -p < database/schema.sql
```

### 2. Backend
```bash
cd backend
cp .env.example .env
# Edit .env — set DB_PASSWORD, JWT_SECRET, JWT_REFRESH_SECRET
npm install
npm run dev        # Runs on http://localhost:5000
```

### 3. Frontend
```bash
# VS Code Live Server  OR
npx serve frontend -p 3000
```

---

## 💰 Fare Structure (NPR)

| Ride Type | Base Fare (NPR) |
|-----------|----------------|
| Economy   | NPR 600        |
| Comfort   | NPR 950        |
| XL        | NPR 2,000      |
| Luxury    | NPR 3,500      |

---

## 💳 Payment Methods

| Key           | Label             |
|---------------|-------------------|
| credit_card   | Credit Card       |
| debit_card    | Debit Card        |
| net_banking   | Net Banking (Nepal banks) |
| visa          | Visa Card         |
| esewa         | eSewa             |
| paypal        | PayPal            |

---

## 🔗 API Endpoints

| Method | Endpoint                        | Auth   | Description              |
|--------|---------------------------------|--------|--------------------------|
| POST   | `/api/auth/register`            | —      | Register rider/driver    |
| POST   | `/api/auth/login`               | —      | Login → JWT tokens       |
| POST   | `/api/auth/refresh`             | —      | Refresh access token     |
| POST   | `/api/auth/logout`              | —      | Invalidate token         |
| POST   | `/api/bookings`                 | ✅ JWT | Create booking (NPR)     |
| GET    | `/api/bookings`                 | ✅ JWT | My bookings              |
| GET    | `/api/bookings/:id`             | ✅ JWT | Booking detail           |
| PATCH  | `/api/bookings/:id/cancel`      | ✅ JWT | Cancel booking           |
| POST   | `/api/payments`                 | ✅ JWT | Pay in NPR               |
| GET    | `/api/payments/:bookingId`      | ✅ JWT | Payment status           |
| POST   | `/api/ratings`                  | ✅ JWT | Submit rating            |
| GET    | `/api/ratings/driver/:id`       | —      | Driver reviews           |
| GET    | `/api/chat/:bookingId`          | ✅ JWT | Chat history             |
| POST   | `/api/chat/:bookingId`          | ✅ JWT | Send message             |
| POST   | `/api/gps/update`               | Driver | Push location            |
| GET    | `/api/gps/:bookingId`           | ✅ JWT | Driver live location     |
| GET    | `/api/health`                   | —      | Health check             |

---

## 🔌 Socket.io Events

| Event             | Description                    |
|-------------------|--------------------------------|
| `join_booking`    | Join a booking room            |
| `chat_message`    | Send/receive chat message      |
| `typing`          | Show typing indicator          |
| `stop_typing`     | Hide typing indicator          |
| `driver_location` | Broadcast GPS coordinates      |

---

## 🗃️ Database Tables

| Table                | Purpose                       |
|----------------------|-------------------------------|
| users                | Riders, drivers, admins       |
| driver_profiles      | Vehicle & GPS data            |
| bookings             | Ride bookings (NPR fares)     |
| booking_passengers   | Passenger names for groups    |
| payments             | NPR payment records           |
| ratings              | Star ratings & reviews        |
| messages             | Chat per booking              |
| gps_tracking         | GPS log                       |
| refresh_tokens       | JWT refresh token store       |
