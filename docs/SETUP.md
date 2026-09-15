# 🚀 JONI - Setup Guide

## Prerequisites

### Software Requirements
- Android Studio (latest version)
- JDK 11 or higher
- Node.js v16+
- npm or yarn
- Git
- Firebase CLI

### Accounts Required
- Google Cloud Account
- Firebase Account
- Facebook Developer Account
- Instagram Business Account
- YouTube Developer Account
- TikTok Developer Account

---

## Step 1: Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Create new project: "JONI-Assistant"
3. Enable following services:
   - Realtime Database
   - Cloud Firestore
   - Authentication
   - Cloud Storage
   - Cloud Functions

4. Download `google-services.json`
5. Place in `android/app/` directory

---

## Step 2: Google Cloud APIs

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create project
3. Enable APIs:
   - Cloud Speech-to-Text API
   - Google Gemini API
   - Cloud Vision API
   - Google Drive API

4. Create API keys:
   - Go to Credentials
   - Create API Key
   - Restrict to Android/Web
   - Copy keys for configuration

---

## Step 3: Social Media API Keys

### Facebook & Instagram
1. Go to [Facebook Developers](https://developers.facebook.com)
2. Create App
3. Get App ID and App Secret
4. Generate Access Tokens

### YouTube
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create OAuth 2.0 credentials
3. Get Client ID and Secret

### TikTok
1. Go to [TikTok Developer](https://developers.tiktok.com)
2. Register application
3. Get Client Key and Client Secret

---

## Step 4: Clone Repository

```bash
git clone https://github.com/basitamaar7-creator/JONI-Android-Assistant.git
cd JONI-Android-Assistant
```

---

## Step 5: Android Development Setup

### Configure local.properties

```properties
# android/local.properties
sdk.dir=/path/to/android/sdk
ndk.dir=/path/to/android/ndk
```

### Configure API Keys

Create `android/app/src/main/res/values/secrets.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="google_cloud_speech_api_key">YOUR_API_KEY</string>
    <string name="google_gemini_api_key">YOUR_API_KEY</string>
    <string name="facebook_app_id">YOUR_APP_ID</string>
    <string name="facebook_app_secret">YOUR_APP_SECRET</string>
    <string name="instagram_access_token">YOUR_ACCESS_TOKEN</string>
    <string name="youtube_api_key">YOUR_API_KEY</string>
    <string name="tiktok_client_key">YOUR_CLIENT_KEY</string>
    <string name="tiktok_client_secret">YOUR_CLIENT_SECRET</string>
</resources>
```

### Build Android App

```bash
cd android
./gradlew build
./gradlew installDebug
```

---

## Step 6: Backend Setup

### Install Dependencies

```bash
cd backend
npm install
```

### Configure Environment Variables

Create `backend/.env`:

```env
PORT=3000
NODE_ENV=development

# Firebase
FIREBASE_API_KEY=YOUR_KEY
FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
FIREBASE_PRIVATE_KEY=YOUR_PRIVATE_KEY

# Google Cloud
GOOGLE_CLOUD_API_KEY=YOUR_API_KEY
GEMINI_API_KEY=YOUR_API_KEY

# Social Media APIs
FACEBOOK_APP_ID=YOUR_APP_ID
FACEBOOK_APP_SECRET=YOUR_APP_SECRET
INSTAGRAM_ACCESS_TOKEN=YOUR_TOKEN
YOUTUBE_API_KEY=YOUR_API_KEY
TIKTOK_CLIENT_KEY=YOUR_CLIENT_KEY
TIKTOK_CLIENT_SECRET=YOUR_CLIENT_SECRET

# Database
MONGODB_URI=mongodb://localhost:27017/joni
```

### Start Backend Server

```bash
npm start
# Server runs on http://localhost:3000
```

---

## Step 7: Web Setup

### Install Dependencies

```bash
cd web
npm install
```

### Configure Environment

Create `web/.env`:

```env
REACT_APP_API_URL=http://localhost:3000
REACT_APP_FIREBASE_API_KEY=YOUR_KEY
REACT_APP_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
```

### Start Web Application

```bash
npm start
# Opens on http://localhost:3000
```

---

## Step 8: Multi-Device Cloud Sync Setup

### Firebase Realtime Database Rules

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid",
        "devices": {
          ".indexOn": ["lastSync"]
        },
        "socialMediaAccounts": {
          ".indexOn": ["platform"]
        }
      }
    }
  }
}
```

---

## Troubleshooting

### Build Errors
- Clear gradle cache: `./gradlew clean build`
- Update dependencies: `./gradlew dependencies`

### API Key Issues
- Verify API is enabled in Google Cloud Console
- Check API key restrictions
- Test API key with sample requests

### Firebase Connection
- Check internet connection
- Verify google-services.json is in correct location
- Check Firebase rules in console

### Social Media API
- Verify access tokens are not expired
- Check API quota limits
- Review rate limiting

---

## Testing

### Run Tests

```bash
# Android
cd android
./gradlew test

# Backend
cd backend
npm test

# Web
cd web
npm test
```

---

## Production Deployment

### Firebase Deployment

```bash
firebase login
firebase deploy
```

### Backend Deployment (Heroku)

```bash
heroku login
heroku create joni-backend
git push heroku main
```

### Web Deployment (Vercel)

```bash
npm install -g vercel
vercel
```

---

## Security Checklist

- [ ] API keys secured in environment variables
- [ ] Firebase rules configured for production
- [ ] SSL/HTTPS enabled
- [ ] Authentication enabled
- [ ] Rate limiting configured
- [ ] Input validation implemented
- [ ] Dependencies updated
- [ ] Security scan completed

---

## Next Steps

1. Explore [Features Guide](FEATURES.md)
2. Check [API Documentation](API_DOCUMENTATION.md)
3. Review [Architecture](ARCHITECTURE.md)
4. Start building agents in `agents/` folder

---

**Support**: If you face issues, create an issue on GitHub or contact support@joniassistant.com
