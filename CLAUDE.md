# Broken Altar - Scripture-guided Prayer App

## Project Overview

**Broken Altar** is a Progressive Web Application (PWA) that provides scripture-guided prayer experiences based on Matthew Henry's "A Method for Prayer" and The Lord's Prayer. The app helps users engage in structured prayer with randomized prompts, audio playback, and reflection capabilities.

## Architecture

### Technology Stack
- **Frontend**: Vanilla JavaScript, HTML5, CSS3
- **Backend**: Firebase (Authentication, Firestore, Cloud Functions)
- **Audio**: Google Cloud Text-to-Speech (via Cloud Functions)
- **Security**: Web Crypto API for client-side encryption
- **PWA**: Service Worker, Web App Manifest

### Key Features
- Two prayer modes: Matthew Henry's Method and The Lord's Prayer
- Google Authentication with Firebase
- Audio playback with Text-to-Speech
- Encrypted user reflections
- Calendar view of saved prayers
- Dark/light theme support
- Offline capability (PWA)

## File Structure

```
├── index.html              # Main application entry point
├── app.js                  # Core application logic (~1740 lines)
├── style.css               # CSS variables and styling
├── manifest.json           # PWA manifest
├── service-worker.js       # PWA service worker
├── crypto-utils.js         # Client-side encryption utilities
├── firebase.json           # Firebase configuration
├── package.json            # Dependencies (Firebase v11.8.1)
├── data/
│   ├── outcome.json        # Matthew Henry prayer prompts
│   └── lord_s_prayer.json  # Lord's Prayer prompts
├── icons/
│   ├── icon-192.png        # PWA icons
│   └── icon-512.png
├── images/
│   └── red_altar_banner.svg # App banner
└── sounds/
    └── bell.mp3            # Transition bell sound
```

## Key Components

### Prayer System
- **Data Loading**: JSON files contain prayer prompts with scripture references
- **Randomization**: Random prompt selection for each prayer category
- **History**: Back/forward navigation through previous prompts
- **Reflection**: Encrypted user reflections stored in Firestore

### Authentication & Storage
- **Firebase Auth**: Google sign-in integration
- **Firestore**: User prayers and settings storage
- **Encryption**: AES-GCM encryption for user reflections
- **localStorage**: User preferences and encryption keys

### Audio Features
- **TTS Integration**: Cloud Functions proxy to Google TTS
- **Wake Lock**: Keep screen awake during playback
- **Bell Sounds**: Optional transition sounds between segments
- **Pause Control**: Configurable pause duration between segments

### UI/UX
- **Responsive Design**: Mobile-first PWA design
- **Theme Support**: Light/dark mode toggle
- **Settings Modal**: Prayer mode, category management, audio settings
- **Calendar View**: Visual prayer history with date navigation

## Development Commands

```bash
# Install dependencies
npm install

# For development, serve locally
# No build process - uses vanilla JS

# Firebase deployment (if configured)
firebase deploy
```

## Configuration

### Firebase Setup
The app requires Firebase configuration in `index.html`:
- Project ID: method25
- Authentication, Firestore, Analytics enabled
- Cloud Functions for TTS proxy

### API Keys
- ESV Bible API token for scripture lookup
- Firebase configuration (already in code)
- Google Cloud TTS (via Cloud Functions)

## Security Features

### Client-side Encryption
- AES-GCM encryption for user reflections
- Keys stored in browser localStorage
- Encrypted data stored in Firestore
- No server-side access to reflection content

### Data Protection
- User prayers require authentication
- Personal reflections encrypted before storage
- Scripture API calls use secure tokens

## Architecture Decisions

### PWA Design
- Offline-first approach with service worker
- App-like experience on mobile devices
- Caching strategy for prayer data and assets

### Client-side Encryption
- Zero-trust approach to user reflection data
- Browser-generated encryption keys
- End-to-end encryption for sensitive content

### Modular Prayer System
- Pluggable prayer modes (Matthew Henry, Lord's Prayer)
- Category-based organization
- User-configurable category selection and ordering

## Deployment Notes

This is a static PWA that can be deployed to:
- Firebase Hosting
- Netlify
- Vercel
- Any static hosting provider

Firebase backend services required:
- Authentication
- Firestore
- Cloud Functions (TTS proxy)

## User Flow

1. **Initial Load**: App loads prayer data and checks authentication
2. **Login**: Optional Google authentication for saving prayers
3. **Prayer Generation**: Random prompts displayed by category
4. **Interaction**: Users can refresh, navigate back, or add reflections
5. **Audio Playback**: TTS reading with configurable pauses
6. **Saving**: Authenticated users can save prayers with reflections
7. **History**: Calendar view shows saved prayers by date

## Security Considerations

- API tokens are exposed client-side (consider backend proxy)
- Encryption keys stored in localStorage (cleared on data wipe)
- Firebase security rules should restrict user data access
- HTTPS required for PWA and security features

## Browser Compatibility

- Modern browsers supporting:
  - Web Crypto API (encryption)
  - Wake Lock API (screen awake)
  - Service Workers (PWA)
  - ES6+ features (modern JavaScript)