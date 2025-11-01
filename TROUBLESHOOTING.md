# 🔧 Troubleshooting Guide

Common issues and solutions for Smart Crop Technologies.

## 🚨 Installation Issues

### ❌ "npm install" fails

**Problem:** Dependencies fail to install

**Solutions:**
```bash
# 1. Clear npm cache
npm cache clean --force

# 2. Delete node_modules and lock file
rm -rf node_modules package-lock.json

# 3. Reinstall
npm install

# 4. Try using --legacy-peer-deps
npm install --legacy-peer-deps
```

### ❌ Node version too old

**Problem:** "Node.js version not supported"

**Solution:**
```bash
# Check current version
node --version

# Update Node.js to v18+
# Download from: https://nodejs.org/
```

---

## 🌐 Server Issues

### ❌ Port 3000 already in use

**Problem:** "Port 3000 is already in use"

**Solutions:**
```bash
# Windows - Find and kill process
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Or use kill-port
npx kill-port 3000

# Or use different port
PORT=3001 npm run dev
```

### ❌ Port 4000 already in use

**Problem:** Mock server won't start

**Solutions:**
```bash
# Kill process on port 4000
npx kill-port 4000

# Or modify mock-server/server.js
# Change: const PORT = 4001;
```

### ❌ Cannot connect to API

**Problem:** Frontend can't reach backend

**Checklist:**
- [ ] Mock server is running (`npm run mock`)
- [ ] Backend shows "Running on: http://localhost:4000"
- [ ] Check `.env.local`: `NEXT_PUBLIC_API_URL=http://localhost:4000`
- [ ] No CORS errors in browser console
- [ ] Firewall not blocking port 4000

**Test:**
```bash
# Open in browser
http://localhost:4000

# Should show API info JSON
```

---

## 🎨 Frontend Issues

### ❌ Page won't load / Blank screen

**Problem:** Frontend displays blank page

**Solutions:**
```bash
# 1. Check browser console for errors
# Press F12 → Console tab

# 2. Clear Next.js cache
rm -rf .next
npm run dev

# 3. Check terminal for build errors

# 4. Verify all dependencies installed
npm install
```

### ❌ Styles not applying

**Problem:** Tailwind CSS not working

**Solutions:**
```bash
# 1. Restart dev server
# Stop (Ctrl+C) and run:
npm run dev

# 2. Clear cache
rm -rf .next

# 3. Check tailwind.config.ts exists
# Verify content paths include your files

# 4. Rebuild
npm run build
```

### ❌ Images not loading

**Problem:** Sample images show broken

**Solutions:**
- Sample images are placeholders (empty files)
- Replace with real images:
  - `public/sample-crop-image.jpg`
  - `public/sample-heatmap.jpg`
- Or use placeholder service:
  ```
  https://via.placeholder.com/800x600
  ```

---

## 🗺️ Map Issues

### ❌ Map not displaying

**Problem:** Dashboard map is blank

**Solutions:**
```bash
# 1. Check browser console for errors

# 2. Verify Leaflet CSS is loaded
# Check _document.tsx has Leaflet stylesheet

# 3. Dynamic import issue - add to component:
import dynamic from 'next/dynamic';
const MapView = dynamic(() => import('@/components/MapView'), { 
  ssr: false 
});

# 4. Clear browser cache
# Ctrl+Shift+Delete → Clear cache

# 5. Try different browser
```

### ❌ "Cannot read property 'L' of undefined"

**Problem:** Leaflet error on server-side rendering

**Solution:**
- Ensure MapView uses `dynamic` import with `ssr: false`
- Check dashboard page uses dynamic import
- Leaflet only works client-side

---

## 🔐 Authentication Issues

### ❌ Login not working

**Problem:** Cannot log in

**Mock Mode Solutions:**
```bash
# 1. Verify mock mode enabled
# Check .env.local:
NEXT_PUBLIC_MOCK_AUTH=true

# 2. Any email/password should work
# Try: farmer@test.com / password123

# 3. For phone, OTP is always: 123456

# 4. Check browser console for errors

# 5. Clear localStorage
# F12 → Application → Local Storage → Clear
```

**Firebase Mode Solutions:**
```bash
# 1. Verify Firebase config in .env.local
# All NEXT_PUBLIC_FIREBASE_* variables set

# 2. Check Firebase console
# Authentication methods enabled

# 3. Domain authorized
# Firebase Console → Authentication → Settings
# Add localhost and your domain

# 4. Set mock mode false
NEXT_PUBLIC_MOCK_AUTH=false
```

### ❌ "User already exists"

**Problem:** Cannot register

**Solution:**
```bash
# Mock mode - try different email
# Firebase - user already registered
# Use login instead or reset password
```

---

## 📤 Upload Issues

### ❌ Image upload fails

**Problem:** Upload returns error

**Checklist:**
- [ ] Mock server is running
- [ ] Image size < 10MB
- [ ] Image format: JPG, JPEG, or PNG
- [ ] Farm ID provided
- [ ] Network connection active

**Debug:**
```bash
# Check backend terminal for errors
# Should show upload request

# Test upload manually:
curl -X POST http://localhost:4000/upload-image \
  -F "image=@/path/to/image.jpg" \
  -F "farmId=farm-001"
```

### ❌ "Cannot read property 'files' of null"

**Problem:** File input error

**Solution:**
- Ensure you've selected a file
- Try uploading a different image
- Check file input ref is initialized

---

## 🎯 TypeScript Issues

### ❌ Type errors in IDE

**Problem:** Red squiggly lines in VS Code

**Solutions:**
```bash
# 1. Restart TS server
# VS Code: Ctrl+Shift+P → "TypeScript: Restart TS Server"

# 2. Check tsconfig.json exists

# 3. Install type definitions
npm install --save-dev @types/react @types/node

# 4. Run type check
npm run build
```

### ❌ "Cannot find module '@/...'"

**Problem:** Path alias not working

**Solution:**
```json
// Verify tsconfig.json has:
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./*"]
    }
  }
}
```

---

## 🏗️ Build Issues

### ❌ "npm run build" fails

**Problem:** Production build errors

**Solutions:**
```bash
# 1. Check for TypeScript errors
npm run build
# Fix all errors shown

# 2. Clear cache and rebuild
rm -rf .next
npm run build

# 3. Check for missing dependencies
npm install

# 4. Verify all imports are correct
# Check for typos in import paths
```

### ❌ Out of memory error

**Problem:** "JavaScript heap out of memory"

**Solution:**
```bash
# Increase Node memory limit
# package.json:
"build": "NODE_OPTIONS='--max-old-space-size=4096' next build"

# Or run directly:
NODE_OPTIONS='--max-old-space-size=4096' npm run build
```

---

## 📱 Mobile Issues

### ❌ Layout broken on mobile

**Problem:** UI doesn't look right on phone

**Solutions:**
- Check responsive breakpoints
- Test in Chrome DevTools mobile mode
- Verify Tailwind responsive classes (`sm:`, `md:`, `lg:`)
- Check viewport meta tag in `_document.tsx`

### ❌ Touch events not working

**Problem:** Buttons/gestures don't work

**Solution:**
- Ensure proper touch event handlers
- Test on actual device, not just emulator
- Check for z-index issues

---

## 🔥 Firebase Issues

### ❌ "Firebase: Error (auth/...)"

**Problem:** Firebase authentication error

**Common Errors:**
- `auth/invalid-api-key` - Check NEXT_PUBLIC_FIREBASE_API_KEY
- `auth/network-request-failed` - Check internet connection
- `auth/too-many-requests` - Wait a few minutes
- `auth/user-not-found` - User doesn't exist, try register
- `auth/wrong-password` - Incorrect password

**Solution:**
```bash
# Verify all Firebase env variables
# Check Firebase Console → Settings
# Ensure values match exactly
```

---

## 🗄️ Database/Storage Issues

### ❌ Cannot save data

**Problem:** Data doesn't persist

**Mock Mode:**
- Data stored in memory only
- Restarting server clears data
- This is expected behavior

**Firebase Mode:**
- Check Firestore security rules
- Verify user is authenticated
- Check Firebase Console for errors

---

## 🎨 UI/UX Issues

### ❌ Icons not showing

**Problem:** Lucide icons missing

**Solution:**
```bash
# Reinstall lucide-react
npm install lucide-react

# Check import:
import { Upload } from 'lucide-react';
```

### ❌ Animations not working

**Problem:** Framer Motion animations don't play

**Solution:**
```bash
# Reinstall framer-motion
npm install framer-motion

# Check import:
import { motion } from 'framer-motion';
```

---

## 🧪 Testing Issues

### ❌ Tests failing

**Problem:** Jest tests don't pass

**Solutions:**
```bash
# 1. Install test dependencies
npm install --save-dev @testing-library/react @testing-library/jest-dom

# 2. Check jest.setup.js exists

# 3. Run tests with verbose
npm test -- --verbose

# 4. Update snapshots if needed
npm test -- -u
```

---

## 🌐 Browser Issues

### ❌ Works in Chrome but not Safari/Firefox

**Problem:** Browser compatibility

**Solutions:**
- Check browser console for specific errors
- Verify polyfills for older browsers
- Test CSS compatibility
- Use autoprefixer (already included)

### ❌ "This site can't be reached"

**Problem:** localhost not accessible

**Solutions:**
```bash
# 1. Check server is running
# Should see "ready - started server..."

# 2. Try 127.0.0.1 instead of localhost
http://127.0.0.1:3000

# 3. Check hosts file (Windows)
# C:\Windows\System32\drivers\etc\hosts
# Should have: 127.0.0.1 localhost

# 4. Disable VPN/Proxy
# May interfere with localhost
```

---

## 🔍 Debugging Tips

### General Debugging Process

1. **Check Console**
   - Browser: F12 → Console
   - Terminal: Look for errors

2. **Clear Caches**
   ```bash
   rm -rf .next
   rm -rf node_modules
   npm install
   ```

3. **Restart Everything**
   - Stop all servers (Ctrl+C)
   - Close terminal
   - Restart computer (if needed)
   - Start fresh

4. **Isolate the Problem**
   - Does it work on fresh install?
   - Is it only one page/component?
   - Does it happen in all browsers?

5. **Check Documentation**
   - README.md
   - SETUP.md
   - API.md

### Useful Commands

```bash
# Check what's running on a port (Windows)
netstat -ano | findstr :<PORT>

# Kill a process (Windows)
taskkill /PID <PID> /F

# View all npm scripts
npm run

# Check Node/npm versions
node --version
npm --version

# Verify package installation
npm list <package-name>

# Clear npm cache
npm cache clean --force
```

---

## 🆘 Still Stuck?

### Get Help

1. **Search Issues**
   - Check GitHub Issues (when available)
   - Search error message on Stack Overflow

2. **Create Issue**
   - Provide error message
   - Share console output
   - Describe steps to reproduce
   - Include environment info

3. **Contact Support**
   - Email: support@smartcrop.tech
   - Include screenshots
   - Share relevant code snippets

### Information to Provide

When asking for help, include:
- Operating System (Windows/Mac/Linux)
- Node.js version (`node --version`)
- npm version (`npm --version`)
- Browser and version
- Error message (full text)
- Steps to reproduce
- What you've already tried

---

## 📚 Additional Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Firebase Docs](https://firebase.google.com/docs)
- [Leaflet Docs](https://leafletjs.com/)

---

**Remember:** Most issues can be solved by:
1. Reading error messages carefully
2. Checking documentation
3. Restarting servers
4. Clearing caches
5. Reinstalling dependencies

**Good luck! 🍀**
