# 📡 API Documentation

Complete API reference for Smart Crop Technologies mock backend.

## Base URL

**Development:** `http://localhost:4000`  
**Production:** `https://your-api-domain.com`

## Authentication

Currently using mock authentication. All endpoints accept requests without authentication tokens.

**Future:** Will require Firebase JWT tokens in `Authorization` header.

---

## Endpoints

### 1. Health Check

Get API server information.

**Endpoint:** `GET /`

**Response:**
```json
{
  "message": "Smart Crop Technologies Mock API Server",
  "version": "1.0.0",
  "status": "running",
  "endpoints": [
    "POST /upload-image",
    "GET /status/:jobId",
    "GET /reports/:farmId",
    "POST /upload-sensor"
  ]
}
```

---

### 2. Upload Drone Image

Upload an aerial farm image for AI analysis.

**Endpoint:** `POST /upload-image`

**Content-Type:** `multipart/form-data`

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| image | File | Yes | Image file (JPEG, JPG, PNG, max 10MB) |
| farmId | String | Yes | Unique farm identifier |
| latitude | String | No | Farm latitude coordinate |
| longitude | String | No | Farm longitude coordinate |
| timestamp | String | No | ISO 8601 timestamp |

**Example Request (using fetch):**
```javascript
const formData = new FormData();
formData.append('image', file);
formData.append('farmId', 'farm-001');
formData.append('latitude', '28.6139');
formData.append('longitude', '77.2090');
formData.append('timestamp', new Date().toISOString());

const response = await fetch('http://localhost:4000/upload-image', {
  method: 'POST',
  body: formData,
});
```

**Success Response (200):**
```json
{
  "success": true,
  "jobId": "JOB-1698765432-a8b9c0d1e",
  "message": "Image uploaded successfully. Analysis started."
}
```

**Error Response (400):**
```json
{
  "success": false,
  "message": "No image file provided"
}
```

**Error Response (500):**
```json
{
  "success": false,
  "message": "Upload failed"
}
```

---

### 3. Get Job Status

Poll for analysis job status and results.

**Endpoint:** `GET /status/:jobId`

**URL Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| jobId | String | Job ID returned from upload |

**Example Request:**
```javascript
const response = await fetch('http://localhost:4000/status/JOB-1698765432-a8b9c0d1e');
```

**Response (Processing):**
```json
{
  "jobId": "JOB-1698765432-a8b9c0d1e",
  "status": "processing",
  "progress": 65,
  "result": null,
  "error": null
}
```

**Response (Completed):**
```json
{
  "jobId": "JOB-1698765432-a8b9c0d1e",
  "status": "completed",
  "progress": 100,
  "result": {
    "farmId": "farm-001",
    "timestamp": "2024-11-01T10:30:00Z",
    "healthScore": 85,
    "ndviAverage": 0.72,
    "detections": [
      {
        "id": "1",
        "type": "disease",
        "confidence": 0.89,
        "bbox": [100, 100, 150, 150],
        "label": "Leaf Blight"
      }
    ],
    "recommendations": [
      {
        "type": "pesticide",
        "priority": "high",
        "title": "Apply Pesticide",
        "description": "Detected pest infestation. Apply neem-based pesticide.",
        "icon": "AlertTriangle"
      }
    ]
  },
  "error": null
}
```

**Status Values:**
- `pending` - Job queued
- `processing` - AI analysis in progress
- `completed` - Analysis finished successfully
- `failed` - Analysis failed

**Error Response (404):**
```json
{
  "success": false,
  "message": "Job not found"
}
```

---

### 4. Get Farm Reports

Retrieve historical analysis reports for a farm.

**Endpoint:** `GET /reports/:farmId`

**URL Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| farmId | String | Unique farm identifier |

**Example Request:**
```javascript
const response = await fetch('http://localhost:4000/reports/farm-001');
```

**Success Response (200):**
```json
[
  {
    "reportId": "RPT-001",
    "farmId": "farm-001",
    "farmName": "Farm farm-001",
    "timestamp": "2024-11-01T10:30:00Z",
    "healthScore": 85,
    "imageUrl": "/sample-images/crop-sample.jpg",
    "summary": "Health score: 85%. 3 detections found."
  },
  {
    "reportId": "RPT-002",
    "farmId": "farm-001",
    "farmName": "Farm farm-001",
    "timestamp": "2024-10-25T14:20:00Z",
    "healthScore": 78,
    "imageUrl": "/sample-images/crop-sample.jpg",
    "summary": "Health score: 78%. 2 detections found."
  }
]
```

Reports are sorted by timestamp (newest first).

---

### 5. Upload Sensor Data

Submit IoT sensor data from farm devices.

**Endpoint:** `POST /upload-sensor`

**Content-Type:** `application/json`

**Request Body:**
```json
{
  "farmId": "farm-001",
  "timestamp": "2024-11-01T10:30:00Z",
  "temperature": 28.5,
  "humidity": 65,
  "soilMoisture": 42,
  "rainfall": 12.5
}
```

**Fields:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| farmId | String | Yes | Unique farm identifier |
| timestamp | String | No | ISO 8601 timestamp (defaults to now) |
| temperature | Number | No | Temperature in Celsius |
| humidity | Number | No | Humidity percentage (0-100) |
| soilMoisture | Number | No | Soil moisture percentage (0-100) |
| rainfall | Number | No | Rainfall in millimeters |

**Example Request:**
```javascript
const response = await fetch('http://localhost:4000/upload-sensor', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    farmId: 'farm-001',
    temperature: 28.5,
    humidity: 65,
    soilMoisture: 42,
    rainfall: 12.5,
  }),
});
```

**Success Response (200):**
```json
{
  "success": true,
  "message": "Sensor data uploaded successfully"
}
```

**Error Response (400):**
```json
{
  "success": false,
  "message": "Farm ID is required"
}
```

---

## Data Types

### Detection Object
```typescript
interface Detection {
  id: string;
  type: 'disease' | 'pest' | 'weed' | 'healthy';
  confidence: number; // 0.0 to 1.0
  bbox: [number, number, number, number]; // [x, y, width, height]
  label: string;
}
```

### Recommendation Object
```typescript
interface Recommendation {
  type: 'irrigation' | 'fertilizer' | 'pesticide' | 'general';
  priority: 'low' | 'medium' | 'high';
  title: string;
  description: string;
  icon?: string;
}
```

## Error Handling

All endpoints return appropriate HTTP status codes:

- `200` - Success
- `400` - Bad Request (invalid input)
- `404` - Not Found (resource doesn't exist)
- `500` - Internal Server Error

Error responses include:
```json
{
  "success": false,
  "message": "Error description"
}
```

## Rate Limiting

**Mock Server:** No rate limiting  
**Production:** TBD (typically 100 requests/minute per IP)

## CORS

Mock server allows all origins (`*`).

Production will restrict to:
- `https://smartcrop.tech`
- `https://www.smartcrop.tech`
- Custom domains

## File Upload Limits

- Max file size: **10 MB**
- Allowed formats: **JPEG, JPG, PNG**
- Stored in: `/mock-server/uploads/`

## Mock AI Behavior

The mock server simulates AI processing:
1. Image upload returns immediately with jobId
2. Job status shows progress incrementally (0% → 100%)
3. Processing takes ~10-20 seconds
4. Results are randomly generated
5. Health scores range 70-100%
6. 1-3 detections per image

## Client Implementation

### Using the API Helper

```typescript
import { uploadImage, getJobStatus, getFarmReports } from '@/lib/api';

// Upload image
const formData = new FormData();
formData.append('image', file);
formData.append('farmId', 'farm-001');
const { jobId } = await uploadImage(formData);

// Poll status
const pollStatus = async () => {
  const status = await getJobStatus(jobId);
  if (status.status === 'completed') {
    console.log('Results:', status.result);
  } else if (status.status === 'processing') {
    setTimeout(pollStatus, 2000); // Poll every 2 seconds
  }
};
pollStatus();

// Get reports
const reports = await getFarmReports('farm-001');
```

## WebSocket Support

**Not currently implemented.**

Future versions may include WebSocket for real-time updates instead of polling.

---

## Support

For API issues or questions:
- GitHub Issues: [Create issue](#)
- Email: api@smartcrop.tech
- Documentation: [README.md](README.md)

---

**Last Updated:** November 2024  
**Version:** 1.0.0
