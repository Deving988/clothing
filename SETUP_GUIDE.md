# 🚀 SIDFIT — Complete Setup Guide
## 0 Budget Deployment

---

## 📁 Files You Got:
| File | Purpose |
|------|---------|
| `index.html` | Customer-facing website (Frontend) |
| `admin.html` | Admin panel — manage orders/products |
| `server.js` | Backend API (deploy on Render.com) |
| `package.json` | Node.js dependencies |
| `.env.example` | Environment variables template |

---

## STEP 1: Firebase Setup (Database) — FREE

1. Go to **https://firebase.google.com**
2. Click "Get Started" → Create project → Name it `sidfit`
3. Go to **Firestore Database** → Create database → Start in production mode
4. Go to **Project Settings** → **Service Accounts** tab
5. Click **Generate new private key** → Download JSON file
6. Open the JSON and copy these values to your `.env`:
   - `project_id` → `FIREBASE_PROJECT_ID`
   - `client_email` → `FIREBASE_CLIENT_EMAIL`
   - `private_key` → `FIREBASE_PRIVATE_KEY`

---

## STEP 2: Razorpay Setup (Payments) — FREE

1. Go to **https://razorpay.com** → Create account
2. Complete KYC (business details, bank account)
3. Dashboard → **Settings** → **API Keys** → Generate Key
4. Copy `Key ID` → `RAZORPAY_KEY_ID`
5. Copy `Key Secret` → `RAZORPAY_KEY_SECRET`
6. **Important:** Also update `RAZORPAY_KEY` in `index.html` (line with `const RAZORPAY_KEY`)

---

## STEP 3: Gmail Email Setup — FREE

1. Go to your Gmail → **Google Account Settings**
2. Security → Turn ON **2-Step Verification**
3. Security → **App Passwords** → Select "Mail" → Generate
4. Copy the 16-character password → `EMAIL_PASS` in `.env`
5. Your Gmail → `EMAIL_USER` in `.env`

---

## STEP 4: Backend Deploy on Render.com — FREE

1. Create account at **https://render.com**
2. Create a GitHub repo and push these files:
   - `server.js`
   - `package.json`
   - `.gitignore` (add `.env` to it!)
3. On Render: **New** → **Web Service** → Connect your GitHub repo
4. Settings:
   - **Build Command:** `npm install`
   - **Start Command:** `node server.js`
   - **Node Version:** 18+
5. Go to **Environment** tab → Add all variables from `.env.example`
6. Click **Deploy** → Copy your backend URL (e.g. `https://sidfit-backend.onrender.com`)

---

## STEP 5: Frontend Deploy on GitHub Pages / Vercel — FREE

### Update Backend URL first!
In `index.html`, find this line and replace:
```javascript
const BACKEND_URL = 'https://your-render-backend.onrender.com';
```
Also in `admin.html`:
```javascript
const BACKEND_URL = 'https://your-render-backend.onrender.com';
```

### GitHub Pages:
1. Create GitHub repo → Upload `index.html` and `admin.html`
2. Repo Settings → Pages → Source: main branch
3. Your site: `https://yourusername.github.io/sidfit`

### Vercel (better — custom domain):
1. **https://vercel.com** → Import GitHub repo
2. Deploy → Done
3. Add custom domain `sidfit.in` in Vercel settings

---

## STEP 6: Connect Custom Domain (sidfit.in)

### If using Vercel:
1. Vercel Dashboard → Your Project → Settings → Domains
2. Add `sidfit.in` → Follow DNS instructions
3. Go to your domain registrar (GoDaddy/BigRock) → Update DNS:
   - Add CNAME: `www` → `cname.vercel-dns.com`
   - Add A Record: `@` → `76.76.21.21`

---

## STEP 7: Admin Panel Access

- Visit: `https://sidfit.in/admin.html`
- Login with your `ADMIN_SECRET` from `.env`
- **Features:**
  - ✅ Add/Edit/Hide products
  - ✅ View all orders
  - ✅ Update order status (auto-emails customer)
  - ✅ View subscribers

---

## 🔔 Notification Flow:

```
Customer places order
       ↓
Razorpay processes payment
       ↓
Backend verifies payment signature
       ↓
✉️  Customer gets "Order Confirmed" email
✉️  YOU get "New Order" email with all details
       ↓
You update order status in Admin Panel
       ↓
✉️  Customer gets "Shipped/Delivered" email
```

---

## 📱 Keep Backend Alive (Free Tier Fix):

Render free tier sleeps after 15 mins of inactivity.
Fix this for FREE using **UptimeRobot**:

1. Go to **https://uptimerobot.com** → Create free account
2. Add New Monitor:
   - Monitor Type: HTTP(s)
   - URL: `https://your-render-backend.onrender.com`
   - Check interval: Every 14 minutes
3. Done! Backend stays awake.

---

## 💰 Cost Summary:

| Service | Cost |
|---------|------|
| Firebase (Firestore) | FREE |
| Render.com (Backend) | FREE |
| Vercel (Frontend) | FREE |
| Razorpay (Payments) | FREE setup, 2% per transaction |
| UptimeRobot | FREE |
| Domain (sidfit.in) | ~₹500-800/year ← Only this! |

---

## 🆘 Troubleshooting:

**CORS error:** Add your frontend URL to `CORS origins` in `server.js`

**Payment not working:** Make sure you're using TEST key for testing, LIVE key for real orders

**Email not sending:** Check Gmail App Password is correct, 2FA is ON

**Backend sleeping:** Setup UptimeRobot as above

---

Made with ❤️ for SIDFIT — sidfit.in 🇮🇳
