# 🚀 Setup Guide - Smart Crop Technologies

Complete step-by-step guide to set up and run the Smart Crop Technologies platform locally.

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** 18.0.0 or higher ([Download](https://nodejs.org/))
- **npm** 8.0.0 or higher (comes with Node.js)
- **Git** ([Download](https://git-scm.com/))
- **Code Editor** (VS Code recommended)

Check versions:
```bash
node --version  # Should be v18.0.0 or higher
npm --version   # Should be 8.0.0 or higher
git --version
```

## 🛠️ Installation Steps

### 1. Navigate to Project Directory

```bash
cd "C:\Users\sumit\Downloads\Smart Crop Technologies"
```

### 2. Install Dependencies

```bash
npm install
```

This will install all required packages including:
- Next.js and React
- TypeScript
- Tailwind CSS
- Express (for mock server)
- Leaflet (for maps)
- And all other dependencies

**Expected output:** Installation should complete without errors in 2-5 minutes.

### 3. Environment Configuration

The `.env.local` file is already created. Review and update if needed:

```bash
# Open in your editor
code .env.local
```

**For development/demo**, the default settings work fine:
```env
NEXT_PUBLIC_MOCK_AUTH=true
NEXT_PUBLIC_API_URL=http://localhost:4000
```

**For production with Firebase**, update with your credentials:
```env
NEXT_PUBLIC_FIREBASE_API_KEY=your-actual-key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
# ... (see Firebase Setup section)
```

### 4. Start Development Servers

You need to run **two servers** - one for frontend, one for backend.

#### Terminal 1 - Frontend (Next.js)

```bash
npm run dev
```

**Output:**
```
ready - started server on 0.0.0.0:3000, url: http://localhost:3000
```

**Access:** Open browser to [http://localhost:3000](http://localhost:3000)

#### Terminal 2 - Backend (Mock API)

Open a **new terminal** in the same directory:

```bash
npm run mock
```

**Output:**
```
╔════════════════════════════════════════════════════════╗
║   Smart Crop Technologies - Mock API Server           ║
║   Running on: http://localhost:4000                   ║
╚════════════════════════════════════════════════════════╝
```

**Test API:** Open [http://localhost:4000](http://localhost:4000)

### 5. Verify Installation

**Frontend checks:**
1. Navigate to `http://localhost:3000`
2. You should see the landing page with hero section
3. Click "Upload Drone Image" - should navigate to upload page
4. Click language toggle (EN/हि) - text should change

**Backend checks:**
1. Navigate to `http://localhost:4000`
2. You should see API info JSON response
3. Check endpoints are listed

**Both working?** ✅ You're ready to use the application!

## 🎯 Quick Start Usage

### Test the Complete Flow

1. **Register/Login**
   - Go to `http://localhost:3000/auth/login`
   - Use any email (e.g., `farmer@test.com`) and password (e.g., `password123`)
   - Or use phone with OTP `123456`
   - Click Login

2. **Upload an Image**
   - Go to Upload page
   - Drag & drop any image (or click to select)
   - Enter Farm ID: `farm-001`
   - Click "Upload & Analyze"
   - Watch the progress bar (simulated AI processing)

3. **View Dashboard**
   - After upload completes, you'll be redirected to dashboard
   - See health metrics, map, and AI detections
   - Click "Download PDF Report"

4. **View Reports**
   - Click "Reports" in navigation
   - See all historical reports
   - Filter by date or search

## 🔧 Troubleshooting

### Issue: Port 3000 or 4000 already in use

**Solution:**
```bash
# Windows - Kill process on port
npx kill-port 3000
npx kill-port 4000

# Or use different ports
PORT=3001 npm run dev
PORT=4001 npm run mock
```

### Issue: Module not found errors

**Solution:**
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

### Issue: Map not loading

**Solution:**
- Maps use dynamic import and won't show in SSR
- Refresh the page
- Check browser console for errors
- Ensure you're on the dashboard page

### Issue: TypeScript errors

**Solution:**
```bash
# Run type check
npm run build

# If errors persist, check tsconfig.json
```

### Issue: Styles not applying

**Solution:**
```bash
# Rebuild Tailwind
npm run dev

# Or clear Next.js cache
rm -rf .next
npm run dev
```

## 🧪 Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test

# Run tests with coverage
npm run test:ci
```

## 📦 Building for Production

```bash
# Build the application
npm run build

# Start production server
npm run start
```

**Access production build:** [http://localhost:3000](http://localhost:3000)

## 🎨 Development Tips

### Hot Reload
- Frontend: Changes auto-refresh
- Backend: Restart server manually (or use `nodemon`)

### Code Formatting
```bash
# Install Prettier extension in VS Code
# Format on save is enabled
```

### Debugging
- Use React DevTools extension
- Check browser console for errors
- Backend logs appear in Terminal 2

### Adding New Pages
1. Create file in `pages/` directory
2. Use `.tsx` extension
3. Export default React component
4. Access at `/filename`

### Adding New Components
1. Create file in `components/` directory
2. Use TypeScript with proper types
3. Import and use in pages

## 📱 Mobile Testing

### Method 1: Browser DevTools
1. Open Chrome DevTools (F12)
2. Click device toolbar icon
3. Select mobile device
4. Refresh page

### Method 2: Local Network
1. Get your computer's IP address
   ```bash
   # Windows
   ipconfig
   # Look for IPv4 Address (e.g., 192.168.1.100)
   ```

2. Update `next.config.js`:
   ```javascript
   // No changes needed, Next.js allows network access by default
   ```

3. On mobile browser, navigate to:
   ```
   http://YOUR-IP:3000
   ```

## 🔐 Firebase Setup (Optional for Production)

If you want to use real Firebase instead of mock auth:

1. **Create Firebase Project**
   - Go to [Firebase Console](https://console.firebase.google.com)
   - Click "Add Project"
   - Follow wizard

2. **Enable Authentication**
   - Go to Authentication → Sign-in method
   - Enable Email/Password
   - Enable Phone (requires billing)

3. **Get Configuration**
   - Project Settings → General
   - Scroll to "Your apps"
   - Click web icon (`</>`)
   - Copy config values

4. **Update .env.local**
   ```env
   NEXT_PUBLIC_FIREBASE_API_KEY=AIza...
   NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your-app.firebaseapp.com
   NEXT_PUBLIC_FIREBASE_PROJECT_ID=your-app
   NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your-app.appspot.com
   NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=123456
   NEXT_PUBLIC_FIREBASE_APP_ID=1:123456:web:abc
   NEXT_PUBLIC_MOCK_AUTH=false
   ```

5. **Restart Server**
   ```bash
   # Stop (Ctrl+C) and restart
   npm run dev
   ```

## 📚 Project Structure Overview

```
smart-crop-website/
├── pages/              # Next.js pages (routes)
├── components/         # Reusable React components
├── lib/               # Utility functions & API
├── styles/            # Global CSS
├── public/            # Static files
├── mock-server/       # Express API server
└── infra/             # Deployment configs
```

## 🆘 Getting Help

**Common Resources:**
- Check `README.md` for overview
- Check `infra/README-deploy.md` for deployment
- Review code comments for understanding

**Still stuck?**
- Check browser console for errors
- Check terminal for server errors
- Verify all dependencies are installed
- Try deleting `node_modules` and reinstalling

## ✅ Checklist

Before you start developing:
- [ ] Node.js 18+ installed
- [ ] All dependencies installed (`npm install`)
- [ ] Frontend server running on port 3000
- [ ] Backend server running on port 4000
- [ ] Can access landing page
- [ ] Can login with mock credentials
- [ ] Can upload image
- [ ] Can view dashboard
- [ ] Maps are loading
- [ ] No console errors

**All checked?** You're ready to start! 🎉

## 🚀 Next Steps

1. **Customize the app** - Update branding, colors, content
2. **Add real AI** - Integrate actual ML models
3. **Connect Firebase** - Use real authentication
4. **Deploy** - Follow `infra/README-deploy.md`
5. **Add features** - Extend functionality

## 📞 Support

For setup help:
- Create an issue on GitHub
- Email: support@smartcrop.tech
- Check documentation in `/docs`

---

**Happy Coding! 💚🌾**
