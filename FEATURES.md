# 🌟 Features Guide - Smart Crop Technologies

Complete guide to all features and capabilities.

---

## 🎯 Core Features

### 1. 🚁 Drone Image Upload

**What it does:**
Upload aerial/drone images of your farm for AI-powered analysis.

**Features:**
- ✅ Drag & drop interface
- ✅ Click to browse files
- ✅ Support for JPEG, JPG, PNG
- ✅ Max file size: 10MB
- ✅ Image preview before upload
- ✅ Real-time progress tracking
- ✅ Metadata capture (farm ID, GPS coordinates)

**How to use:**
1. Navigate to Upload page
2. Drag image or click to select
3. Enter farm ID (e.g., `farm-001`)
4. Optionally add GPS coordinates
5. Click "Upload & Analyze"
6. Watch progress bar
7. Automatically redirected to dashboard when complete

**Tech Stack:**
- React `useState` for state management
- HTML5 File API
- FormData for multipart upload
- Axios for HTTP requests
- Framer Motion for animations

---

### 2. 🤖 AI-Powered Crop Analysis

**What it does:**
Analyzes uploaded images to detect crop health, diseases, pests, and weeds.

**Detection Types:**
- 🦠 **Disease Detection** - Identifies crop diseases like leaf blight
- 🐛 **Pest Detection** - Spots insect infestations (aphids, etc.)
- 🌿 **Weed Detection** - Recognizes weed growth
- ✅ **Healthy Areas** - Identifies healthy crop sections

**Analysis Metrics:**
- **Health Score** (0-100%) - Overall crop health rating
- **NDVI Average** (0.0-1.0) - Vegetation health index
- **Confidence Scores** - Detection accuracy percentage
- **Bounding Boxes** - Precise problem locations

**How it works:**
1. Image uploaded to backend
2. Mock AI processes image (~10-20 seconds)
3. Returns detections with coordinates
4. Frontend displays with visual overlays

**Future Enhancement:**
Replace mock AI with actual TensorFlow.js model for real-time inference.

---

### 3. 📊 Comprehensive Dashboard

**Overview Cards:**
- 💚 **Health Score** - Current farm health percentage
- 🌡️ **Temperature** - Real-time temperature data
- 💧 **Humidity** - Atmospheric moisture level
- 🌊 **Soil Moisture** - Ground moisture percentage

**Visual Components:**
- 🗺️ **Interactive Map** - Farm boundaries and markers
- 🖼️ **Image Overlay Viewer** - AI detections with bounding boxes
- 📈 **Trend Indicators** - Up/down from last week
- 📍 **Location Markers** - Problem areas on map

**Quick Actions:**
- Upload new scan
- View historical reports
- Download PDF report
- Switch languages

**Recommendations Panel:**
Shows prioritized action items:
- 🔴 High priority (red) - Urgent actions
- 🟡 Medium priority (yellow) - Important tasks
- 🔵 Low priority (blue) - Scheduled maintenance

---

### 4. 🗺️ Interactive Farm Mapping

**Powered by:** Leaflet + OpenStreetMap

**Features:**
- ✅ Farm boundary polygons
- ✅ Color-coded markers (healthy/warning/alert)
- ✅ Zoom and pan controls
- ✅ Click markers for details
- ✅ Legend overlay
- ✅ Responsive on mobile
- ✅ Optional Mapbox integration

**Marker Types:**
- 🟢 Green - Healthy areas
- 🟡 Yellow - Warning zones
- 🔴 Red - Critical issues

**How to use:**
1. View dashboard
2. Map shows your farm location
3. Zoom in/out with controls
4. Click markers for information
5. See legend for color meanings

---

### 5. 🖼️ Image Overlay Viewer

**View Modes:**
1. **Original** - Raw uploaded image
2. **Detections** - Bounding boxes and labels
3. **NDVI Heatmap** - Color-coded vegetation health

**Controls:**
- 🔍 Zoom In/Out
- 🔄 Reset zoom
- 💾 Download processed image
- 🔀 Switch view modes

**Detection Overlay:**
- Color-coded boxes by type
- Confidence percentage labels
- Detection counts in legend
- Hover for details

**Tech:**
- HTML5 Canvas API for drawing
- Dynamic bounding box rendering
- Image manipulation
- Export to PNG

---

### 6. 🌐 Bilingual Interface

**Supported Languages:**
- 🇬🇧 **English** - Default
- 🇮🇳 **Hindi (हिंदी)** - Full translation

**What's translated:**
- All UI text
- Navigation menus
- Form labels
- Button text
- Error messages
- Dashboard metrics
- Recommendations
- Footer content

**How to switch:**
- Click language toggle in navbar
- Choose EN or हि
- Preference saved in localStorage
- Instant UI update

**Adding new languages:**
Edit `lib/i18n.ts` and add translation object.

---

### 7. 🔐 Firebase Authentication

**Login Methods:**

**Email/Password:**
- Standard email login
- Password reset support
- Remember me option

**Phone/OTP:**
- SMS verification
- 6-digit OTP
- Country code support

**Mock Mode (Development):**
- Any email/password works
- OTP always `123456`
- No actual verification

**Features:**
- Secure authentication flow
- Session persistence
- Auto-redirect after login
- Logout functionality

---

### 8. 📄 PDF Report Generation

**Report Contents:**
- Farm information
- Health score
- Scan date
- Sensor readings
- Detection summary
- Recommendations
- Timestamp

**Format:**
- A4 size
- Professional layout
- Logo included
- Printable

**How to generate:**
1. Go to dashboard
2. Click "Download PDF Report"
3. PDF downloads automatically
4. Open with any PDF reader

**Tech:** jsPDF library

---

### 9. 📱 Mobile-First Design

**Responsive Breakpoints:**
- 📱 Mobile: < 640px
- 📱 Tablet: 640px - 1024px
- 🖥️ Desktop: > 1024px

**Mobile Features:**
- Touch-friendly buttons
- Collapsible navigation
- Mobile-optimized forms
- Swipeable galleries
- Responsive images
- Adaptive layouts

**Tested on:**
- iOS Safari
- Chrome Mobile
- Samsung Internet
- Firefox Mobile

---

### 10. 📊 Historical Reports

**Features:**
- 📅 Date filtering
- 🔍 Search by farm name or ID
- 📋 List view with summaries
- 👁️ Quick view actions
- 💾 Download individual reports
- 📈 Health score history

**Report Cards Show:**
- Farm name
- Report ID
- Timestamp
- Health score with color coding
- Summary text
- Thumbnail image

**Actions:**
- View full dashboard
- Download PDF
- Filter by date range
- Search reports

---

## 🎨 UI/UX Features

### Design Elements

**Color System:**
- Primary green for growth/success
- Amber for important actions
- Red for alerts/warnings
- Clean grays for neutrals

**Typography:**
- Inter font family
- Clear hierarchy
- Large readable text
- Accessible contrast

**Components:**
- Rounded corners (rounded-2xl)
- Soft shadows
- Smooth transitions
- Consistent spacing

**Animations:**
- Page transitions
- Card hover effects
- Loading states
- Fade-in elements

### Accessibility

**WCAG AA Compliant:**
- ✅ Keyboard navigation
- ✅ Screen reader friendly
- ✅ High contrast text
- ✅ Alt text on images
- ✅ Focus indicators
- ✅ Semantic HTML

---

## 🔧 Developer Features

### TypeScript

**Benefits:**
- Type safety
- IntelliSense support
- Fewer runtime errors
- Better documentation
- Refactoring confidence

**Coverage:**
- All components typed
- API responses typed
- Props interfaces
- Utility functions

### Code Quality

**Tools:**
- ESLint for linting
- Prettier for formatting
- TypeScript compiler
- Jest for testing

**Standards:**
- Consistent code style
- Clear naming conventions
- Modular architecture
- Reusable components

### API Integration

**Features:**
- Axios HTTP client
- Type-safe responses
- Error handling
- Loading states
- Retry logic ready

**Endpoints:**
- Upload image
- Get job status
- Fetch reports
- Upload sensor data

---

## 🚀 Performance Features

### Optimizations

**Image Loading:**
- Lazy loading
- Next.js Image component ready
- Proper sizing
- Format optimization

**Code Splitting:**
- Dynamic imports
- Route-based splitting
- Component lazy loading
- Vendor bundle optimization

**Caching:**
- Static asset caching
- API response caching ready
- Browser caching headers

**Bundle Size:**
- Tree shaking
- CSS purging
- Minimal dependencies
- Production builds optimized

---

## 🔄 Real-Time Features

### Live Updates

**Upload Progress:**
- Real-time percentage
- Status messages
- Error handling
- Success notifications

**Job Status Polling:**
- 2-second intervals
- Progress bar animation
- Auto-stop when complete
- Timeout handling

**Sensor Data:**
- Live readings (mock)
- Auto-refresh ready
- WebSocket ready for future

---

## 📦 Backend Features (Mock Server)

### API Capabilities

**File Upload:**
- Multer middleware
- Type validation
- Size limits
- Error handling

**Storage:**
- Local file system
- Organized uploads folder
- Unique filenames
- Cleanup ready

**Job Processing:**
- Async simulation
- Progress tracking
- Result generation
- Error states

**CORS:**
- Cross-origin enabled
- Configurable origins
- Headers set correctly

---

## 🎯 Future Features (Planned)

### Phase 2
- [ ] Real AI model integration
- [ ] WebSocket for live updates
- [ ] Advanced analytics dashboard
- [ ] Weather API integration
- [ ] Crop growth predictions

### Phase 3
- [ ] Multi-farm management
- [ ] Team collaboration
- [ ] Mobile app (React Native)
- [ ] WhatsApp notifications
- [ ] Marketplace integration

### Phase 4
- [ ] Drone control integration
- [ ] Automated irrigation triggers
- [ ] AI-powered recommendations
- [ ] Historical trend analysis
- [ ] Yield predictions

---

## 📚 Learn More

For detailed guides on specific features:
- **Setup:** SETUP.md
- **API:** API.md
- **Deployment:** infra/README-deploy.md
- **Troubleshooting:** TROUBLESHOOTING.md

---

**Enjoy using Smart Crop Technologies! 🌾💚**
