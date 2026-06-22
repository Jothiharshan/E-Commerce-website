# 🛍️ JH  
SHOP — E-Commerce Web Application

A **full-stack, production-ready** e-commerce platform built for the JD Shop brand. Includes product catalog, cart, checkout, user auth (Admin/User roles), order tracking, and a backend API connected to your choice of database.

---

## 📁 Project Structure

```
jd-shop/
├── index.html            ← Frontend (drop into /public/)
├── server.js             ← Express backend entry point
├── package.json          ← All dependencies
├── .env.example          ← Copy to .env and fill values
├── routes/
│   ├── auth.js           ← Login, Register, JWT
│   ├── products.js       ← CRUD product management
│   ├── orders.js         ← Order creation & tracking
│   ├── users.js          ← User profile management
│   ├── cart.js           ← Cart operations
│   ├── payment.js        ← Stripe / Razorpay webhooks
│   └── admin.js          ← Admin-only dashboard API
├── models/
│   ├── User.js           ← User schema (Mongoose)
│   ├── Product.js        ← Product schema
│   └── Order.js          ← Order schema
├── middleware/
│   ├── auth.js           ← JWT verify middleware
│   └── admin.js          ← Role-based access guard
└── public/
    └── index.html        ← Copy the frontend file here
```

---

## ⚙️ 1. INSTALL DEPENDENCIES

```bash
npm install
```

---

## 🗄️ 2. DATABASE SETUP

### Option A — MongoDB (Recommended, easiest)
1. Go to https://cloud.mongodb.com → Create free cluster
2. Get connection string → paste as `MONGO_URI` in `.env`
3. In `server.js`, add:
```js
const mongoose = require('mongoose');
mongoose.connect(process.env.MONGO_URI)
  .then(() => console.log('✅ MongoDB connected'))
  .catch(err => console.error(err));
```

### Option B — MySQL
```bash
npm install mysql2
```
Create database:
```sql
CREATE DATABASE jdshop;
```
Use `MYSQL_*` vars in `.env`

### Option C — PostgreSQL
```bash
npm install pg
```
Create database:
```bash
createdb jdshop
```
Use `PG_*` vars in `.env`

---

## 🔐 3. ENVIRONMENT SETUP

```bash
cp .env.example .env
# Then open .env and fill in all values
```

---

## 🚀 4. RUN LOCALLY

```bash
# Development (with auto-reload)
npm run dev

# Production
npm start
```
App runs at: **http://localhost:5000**

---

## 📦 KEY NPM PACKAGES USED

| Package | Purpose |
|---|---|
| `express` | Web framework / API server |
| `mongoose` | MongoDB ODM |
| `mysql2` | MySQL driver |
| `pg` | PostgreSQL driver |
| `bcryptjs` | Password hashing |
| `jsonwebtoken` | JWT auth tokens |
| `cors` | Cross-origin support |
| `dotenv` | Environment variables |
| `multer` | File / image uploads |
| `express-validator` | Input validation |
| `helmet` | HTTP security headers |
| `morgan` | Request logging |
| `compression` | Gzip compression |
| `express-rate-limit` | API rate limiting |
| `nodemailer` | Order confirmation emails |
| `stripe` | Payment processing (international) |
| `razorpay` | Payment processing (India) |
| `cloudinary` | Cloud image storage |
| `cookie-parser` | Cookie handling |
| `nodemon` | Dev auto-reload |

---

## ☁️ 5. DEPLOYMENT OPTIONS

### A) Render.com (Free tier, easiest)
1. Push code to GitHub
2. Go to https://render.com → New Web Service
3. Connect repo → Set `Build Command: npm install`
4. Set `Start Command: node server.js`
5. Add all env vars from `.env`
6. Deploy ✅

### B) Railway.app (Free tier)
1. Push to GitHub
2. https://railway.app → New Project → Deploy from GitHub
3. Add environment variables
4. Auto-deploy on push ✅

### C) Vercel (Frontend only)
1. Put `index.html` in root or `/public`
2. `vercel --prod` or connect GitHub repo
3. For backend use Vercel Serverless Functions

### D) Heroku
```bash
heroku create jd-shop-prod
heroku config:set NODE_ENV=production JWT_SECRET=xxx ...
git push heroku main
```

### E) VPS (DigitalOcean / Linode / AWS EC2)
```bash
# On server:
git clone https://github.com/yourname/jd-shop.git
cd jd-shop
npm install
cp .env.example .env && nano .env

# Install PM2 for process management
npm install -g pm2
pm2 start server.js --name "jd-shop"
pm2 save && pm2 startup

# Nginx reverse proxy (port 80 → 5000)
sudo apt install nginx
# Configure /etc/nginx/sites-available/jd-shop
```

---

## 👤 6. USER ROLES

| Role | Access |
|---|---|
| **User** | Browse, buy, track orders, manage profile |
| **Admin** | All above + Add/Edit/Delete products, view all orders, manage users |

JWT token contains `role: "admin"` or `role: "user"` — middleware checks on protected routes.

---

## 🔌 7. CORE API ENDPOINTS

```
POST   /api/auth/register       → Create account
POST   /api/auth/login          → Get JWT token
GET    /api/products            → List products (with filters)
GET    /api/products/:id        → Product detail
POST   /api/products            → [Admin] Create product
PUT    /api/products/:id        → [Admin] Update product
DELETE /api/products/:id        → [Admin] Delete product
POST   /api/orders              → Place order
GET    /api/orders/my           → My orders
GET    /api/orders/:id/track    → Track order status
GET    /api/admin/orders        → [Admin] All orders
PATCH  /api/admin/orders/:id    → [Admin] Update order status
GET    /api/admin/users         → [Admin] All users
```

---

## 💳 8. PAYMENT SETUP

### Razorpay (India — Recommended)
1. Sign up at https://razorpay.com
2. Get Key ID + Key Secret from Dashboard → Settings → API Keys
3. Add to `.env` as `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET`

### Stripe (International)
1. Sign up at https://stripe.com
2. Get secret key from Dashboard → Developers → API Keys
3. Add to `.env` as `STRIPE_SECRET_KEY`

---

## 📧 9. EMAIL SETUP (Order Confirmations)
1. Enable "App Passwords" in your Gmail account
2. Set `SMTP_USER` = your Gmail
3. Set `SMTP_PASS` = 16-character app password

---

## 🖼️ 10. IMAGE UPLOADS (Cloudinary)
1. Sign up free at https://cloudinary.com
2. Get Cloud Name, API Key, API Secret from Dashboard
3. Add to `.env`
4. Images auto-optimized and served via CDN

---

## 📞 Support
Built with ❤️ for JD Shop. For issues, open a GitHub issue or contact the dev team.
