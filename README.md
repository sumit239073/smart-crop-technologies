# 🌾 CropNexus

**AI + Drone-powered Precision Agriculture Platform for Small Farmers**

A modern, production-ready web application that enables farmers to upload drone images, view AI-generated crop health insights, and get real-time analytics through a clean, mobile-first dashboard.

![Next.js](https://img.shields.io/badge/Next.js-14.2-black?logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5.4-blue?logo=typescript)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.4-38bdf8?logo=tailwind-css)
![License](https://img.shields.io/badge/License-MIT-green)

## ✨ Features

- 🚁 **Drone Image Upload** - Drag & drop interface for aerial crop images
- 🤖 **AI-Powered Analysis** - Real-time crop health detection and NDVI heatmaps
- 📊 **Farmer Dashboard** - Comprehensive farm health metrics and visualizations
- 🗺️ **Interactive Maps** - Leaflet-based farm mapping with overlay support
- 🌐 **Bilingual Support** - English and Hindi (i18n ready)
- 🔐 **Firebase Auth** - Email, phone, and mock authentication
- 📱 **Mobile-First Design** - Responsive on all devices
- 📄 **PDF Reports** - Downloadable crop health reports
- 🎨 **Modern UI/UX** - Clean design with Framer Motion animations

## 🛠️ Tech Stack

### Frontend
- **Framework:** Next.js 14 (React 18)
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **Maps:** Leaflet + OpenStreetMap
- **Animations:** Framer Motion
- **Icons:** Lucide React
- **PDF Generation:** jsPDF

### Backend (Mock)
- **Server:** Express.js
- **File Upload:** Multer
- **CORS:** CORS middleware

### Database & Auth (Future-Ready)
- **Authentication:** Firebase Auth
- **Database:** Firebase Firestore
- **Storage:** Firebase Storage

## 📁 Project Structure

```
smart-crop-website/
├── pages/
│   ├── index.tsx                 # Landing page
│   ├── upload.tsx                # Image upload page
│   ├── reports.tsx               # Reports listing
│   ├── dashboard/
│   │   └── [farmId].tsx          # Farm dashboard
│   └── auth/
│       ├── login.tsx             # Login page
│       └── register.tsx          # Registration page
├── components/
│   ├── Navbar.tsx                # Main navigation
│   ├── Hero.tsx                  # Hero section
│   ├── MapView.tsx               # Leaflet map component
│   ├── ImageOverlayViewer.tsx    # Image analysis viewer
│   ├── HealthCard.tsx            # Health metric cards
│   └── LanguageToggle.tsx        # Language switcher
├── lib/
│   ├── api.ts                    # API client functions
│   ├── i18n.ts                   # Internationalization
│   └── firebase.ts               # Firebase configuration
├── mock-server/
│   ├── server.js                 # Express mock API
│   ├── uploads/                  # Uploaded images
│   └── sample-images/            # Sample data
├── styles/
│   └── globals.css               # Global styles
└── public/
    └── assets/                   # Static assets
```

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm/yarn
- Git

### Installation

1. **Clone the repository**
```bash
cd "C:\Users\sumit\Downloads\Smart Crop Technologies"
# or if you renamed the folder:
cd "C:\Users\sumit\Downloads\cropnexus"
```

2. **Install dependencies**
```bash
npm install
```

3. **Set up environment variables**

Copy `.env.local` and update with your Firebase credentials (optional for demo):

```env
NEXT_PUBLIC_FIREBASE_API_KEY=your-api-key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your-project-id
NEXT_PUBLIC_API_URL=http://localhost:4000
NEXT_PUBLIC_MOCK_AUTH=true
```

4. **Run development servers**

**Frontend (Next.js):**
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000)

**Backend (Mock API):**
```bash
npm run mock
```
API running on [http://localhost:4000](http://localhost:4000)

5. **Build for production**
```bash
npm run build
npm run start
```

## 📖 Usage Guide

### For Farmers

1. **Register/Login** - Create an account using email or phone number
2. **Upload Drone Image** - Go to Upload page and drag & drop your aerial farm image
3. **View Analysis** - AI processes the image and displays crop health insights
4. **Check Dashboard** - View health scores, NDVI maps, and recommendations
5. **Download Reports** - Export PDF reports for record-keeping

### For Developers

#### API Endpoints

**Mock Backend (http://localhost:4000)**

- `POST /upload-image` - Upload drone image for analysis
- `GET /status/:jobId` - Get analysis job status
- `GET /reports/:farmId` - Fetch farm reports
- `POST /upload-sensor` - Upload IoT sensor data

#### Example: Upload Image

```typescript
import { uploadImage } from '@/lib/api';

const formData = new FormData();
formData.append('image', file);
formData.append('farmId', 'farm-001');
formData.append('latitude', '28.6139');
formData.append('longitude', '77.2090');

const response = await uploadImage(formData);
console.log(response.jobId);
```

## 🎨 UI Components

### Key Components

**HealthCard** - Displays metrics with icons and trends
```tsx
<HealthCard
  title="Health Score"
  value={85}
  unit="%"
  icon={Activity}
  color="green"
  trend="up"
/>
```

**MapView** - Interactive farm map
```tsx
<MapView
  center={[28.6139, 77.2090]}
  farmPolygon={coordinates}
  markers={[...]}
/>
```

**ImageOverlayViewer** - AI analysis visualization
```tsx
<ImageOverlayViewer
  imageUrl="/path/to/image.jpg"
  detections={detections}
  showDetections={true}
/>
```

## 🌍 Internationalization

Toggle between English and Hindi using the language switcher in the navbar.

**Add new translations** in `lib/i18n.ts`:

```typescript
const translations = {
  en: {
    key: 'English text',
  },
  hi: {
    key: 'हिंदी पाठ',
  },
};
```

## 🔒 Authentication

### Mock Mode (Development)
Set `NEXT_PUBLIC_MOCK_AUTH=true` in `.env.local`
- Use any email/password
- Phone OTP is always `123456`

### Production Mode
Configure Firebase Authentication:
1. Create a Firebase project
2. Enable Email/Password and Phone authentication
3. Add Firebase config to `.env.local`
4. Set `NEXT_PUBLIC_MOCK_AUTH=false`

## 📦 Deployment

### Deploy to Vercel (Recommended)

1. **Push to GitHub**
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin your-repo-url
git push -u origin main
```

2. **Deploy to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Import your repository
   - Configure environment variables
   - Deploy!

3. **Deploy Backend**
   - Use Vercel Serverless Functions or
   - Deploy Express server to Railway, Render, or Heroku

### Environment Variables for Production

```env
NEXT_PUBLIC_FIREBASE_API_KEY=xxx
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=xxx
NEXT_PUBLIC_FIREBASE_PROJECT_ID=xxx
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=xxx
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=xxx
NEXT_PUBLIC_FIREBASE_APP_ID=xxx
NEXT_PUBLIC_API_URL=https://your-api-url.com
NEXT_PUBLIC_MAPBOX_TOKEN=(optional)
NEXT_PUBLIC_MOCK_AUTH=false
```

## 🧪 Testing

```bash
npm run test
```

## 📝 Sample Data

The mock server includes:
- 3 sample drone images
- Mock AI detection results
- Sample farm reports
- Simulated sensor data

## 🎯 Roadmap

- [ ] Real AI model integration (TensorFlow.js)
- [ ] IoT sensor dashboard
- [ ] Weather API integration
- [ ] Multi-farm management
- [ ] Mobile app (React Native)
- [ ] Advanced analytics and predictions
- [ ] Marketplace for agricultural products

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **CropNexus Team**

## 🙏 Acknowledgments

- OpenStreetMap for mapping data
- Firebase for backend services
- Vercel for hosting
- All contributors and farmers who inspired this project

## 📞 Support

For support, email contact@smartcrop.tech or open an issue on GitHub.

---

**Made with ❤️ for farmers worldwide**
