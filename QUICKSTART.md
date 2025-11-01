# ⚡ Quick Start Guide

Get Smart Crop Technologies running in **5 minutes**!

## 🎯 TL;DR

```bash
# 1. Navigate to project
cd "C:\Users\sumit\Downloads\Smart Crop Technologies"

# 2. Install dependencies
npm install

# 3. Start frontend (Terminal 1)
npm run dev

# 4. Start backend (Terminal 2 - new window)
npm run mock

# 5. Open browser
# Frontend: http://localhost:3000
# Backend:  http://localhost:4000
```

## ✅ Verify It's Working

1. **Landing Page** - Should load at http://localhost:3000
2. **Click "Upload Drone Image"** - Navigate to upload page
3. **Login** - Use `farmer@test.com` / `password123`
4. **Upload any image** - See AI processing simulation
5. **View Dashboard** - See health metrics and map

## 🎮 Demo Credentials

**Email Login:**
- Email: `farmer@test.com`
- Password: `password123` (or any password)

**Phone Login:**
- Phone: Any number (e.g., `+91 9876543210`)
- OTP: `123456`

## 🚨 Common Issues

**"Port 3000 in use"**
```bash
npx kill-port 3000
npm run dev
```

**"Cannot find module"**
```bash
npm install
```

**"Map not loading"**
- Refresh the page
- Check you're on dashboard page

## 📚 What's Next?

- Read [SETUP.md](SETUP.md) for detailed setup
- Read [README.md](README.md) for full documentation
- Check [infra/README-deploy.md](infra/README-deploy.md) for deployment

## 🎉 That's It!

You're now running Smart Crop Technologies locally!

---

**Need help?** Check SETUP.md or create an issue.
