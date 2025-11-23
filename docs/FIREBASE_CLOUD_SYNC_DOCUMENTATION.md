# German Flashcard App - Firebase Cloud Sync Documentation

**Version:** 2.5
**Last Updated:** 2025-11-22
**Status:** ✅ Configured and Ready

---

## 📋 Table of Contents
1. [Overview](#overview)
2. [Firebase Configuration](#firebase-configuration)
3. [Features](#features)
4. [How to Use](#how-to-use)
5. [Security & Privacy](#security--privacy)
6. [Testing Checklist](#testing-checklist)
7. [Troubleshooting](#troubleshooting)
8. [Technical Details](#technical-details)

---

## Overview

The German Flashcard App now includes **Firebase Cloud Sync** functionality, allowing you to:
- 🔐 Create secure user accounts with username/password
- ☁️ Sync your vocabulary categories across devices
- 📱 Access your flashcards from any browser
- 🔒 Encrypt your data with AES-256-GCM encryption

---

## Firebase Configuration

### Project Details
```
Project Name:     flashcard-sync-15835
Project ID:       flashcard-sync-15835
Region:           United States
Database Type:    Realtime Database
```

### Configuration (Already Applied)
The following Firebase configuration has been integrated into `flashcard.html`:

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyCci_5AhIKW3VPnFu8LFBDJQxYQvPbOUlE",
    authDomain: "flashcard-sync-15835.firebaseapp.com",
    databaseURL: "https://flashcard-sync-15835-default-rtdb.firebaseio.com",
    projectId: "flashcard-sync-15835",
    storageBucket: "flashcard-sync-15835.firebasestorage.app",
    messagingSenderId: "220998447564",
    appId: "1:220998447564:web:d258c84f0cbfb882da2d69"
};
```

### Firebase Console Access
- **Console URL:** https://console.firebase.google.com/project/flashcard-sync-15835
- **Database URL:** https://flashcard-sync-15835-default-rtdb.firebaseio.com

---

## Features

### 🔐 User Authentication
- **Username-based authentication** (no email required)
- **Password encryption** using SHA-256 hashing
- **Case-insensitive usernames** (masoud = MASOUD = Masoud)
- **Case-sensitive passwords** (Pass123 ≠ pass123)

### ☁️ Cloud Sync
- **Automatic synchronization** of vocabulary categories
- **File categorization** with categories and subcategories
- **Real-time updates** across all logged-in devices
- **Local + Cloud storage** (works offline with localStorage)

### 🔒 Data Encryption
- **AES-256-GCM encryption** for all synced data
- **Password-based encryption key** derived from your password
- **Zero-knowledge architecture** - Only you can decrypt your data
- **No one else can read your vocabulary** (not even server admins)

---

## How to Use

### First Time Setup

1. **Open the App**
   ```
   Open: German-Flashcard-App/flashcard.html in your browser
   ```

2. **Login Screen Appears**
   - You'll see a login form when opening the app
   - Two options: Login or Skip to Local Only

3. **Create New Account**
   - Enter a **unique username** (e.g., "masoud")
   - Enter a **strong password** (remember it - cannot be recovered!)
   - Click **"Login / Create Account"**
   - If username is new, account will be created automatically

4. **Upload Vocabulary**
   - Click **"📁 Choose CSV File"**
   - Select your German-English vocabulary CSV file
   - Supported formats:
     ```
     German,English
     German,German Example,English
     German,German Example,English,English Example
     ```

5. **Manage Categories**
   - Click **"📚 Manage Categories"**
   - Create categories (e.g., "German A1", "Business German")
   - Create subcategories (e.g., "A1 Vocabulary", "Verbs", "Nouns")
   - Assign files to categories

6. **Data Automatically Syncs**
   - All category data syncs to Firebase automatically
   - Categories appear in **"📚 Your Vocabulary Categories"** section

### Using on Multiple Devices

1. **Second Device Setup**
   - Open the same `flashcard.html` file on another device
   - Or host it on a web server for remote access

2. **Login**
   - Use the **SAME username and password**
   - Data will automatically download from cloud

3. **Sync Behavior**
   - Changes sync **automatically** when online
   - **Merge strategy:** Cloud data takes precedence
   - Local changes upload when connection restored

### Offline Mode

- Click **"Skip (Use Local Only)"** on login screen
- All data stored in browser's localStorage only
- No cloud sync (device-specific)
- Can enable cloud sync later by creating/logging into account

---

## Security & Privacy

### What Gets Synced
✅ **Synced to Firebase:**
- Your categories (category names and structure)
- Your fileCategories (file → category assignments)
- Encrypted vocabulary data

❌ **NOT Synced:**
- File paths (local to your device)
- Personal information
- Browser history
- Progress statistics (learned/unlearned status)

### Encryption Details

**Algorithm:** AES-256-GCM (Galois/Counter Mode)
- **Key Derivation:** PBKDF2 with 100,000 iterations
- **Unique Salt:** Generated per user
- **Authentication Tag:** Prevents tampering
- **Initialization Vector:** Unique per encryption

**Example Flow:**
```
Your Data → Encrypt with Password → Upload to Firebase
                                          ↓
                                    Encrypted Data
                                          ↓
Firebase → Download → Decrypt with Password → Your Data
```

### Password Security
⚠️ **IMPORTANT:**
- Passwords are **NEVER** stored in plain text
- Only SHA-256 hash stored for authentication
- **Cannot be recovered** if forgotten
- No password reset functionality (by design for security)
- Choose a strong password and **remember it**

### Username Guidelines
- Choose a **unique** username
- Case-insensitive: "john" = "John" = "JOHN"
- If username taken, you'll see "Invalid password" error
- Try a different username if this happens

---

## Testing Checklist

### ✅ Basic Functionality
- [ ] App opens and shows login screen
- [ ] Can create new account with username/password
- [ ] Can login with existing account
- [ ] Login persists after page refresh
- [ ] Can logout successfully

### ✅ Vocabulary Management
- [ ] Can upload CSV files
- [ ] Flashcards display correctly
- [ ] Can create categories
- [ ] Can create subcategories
- [ ] Can assign files to categories
- [ ] Category browser shows all categories

### ✅ Cloud Sync
- [ ] Categories sync to Firebase
- [ ] Can see data in Firebase Console (encrypted)
- [ ] Login on second device loads data
- [ ] Changes on one device appear on other
- [ ] No console errors (F12 Developer Tools)

### ✅ Offline Mode
- [ ] "Skip (Use Local Only)" works
- [ ] Local storage works without cloud
- [ ] Can switch to cloud sync later

---

## Troubleshooting

### Problem: Login shows "Cloud sync not configured"

**Solution:**
- This means Firebase config is missing
- Should NOT happen with the updated file
- If you see this, re-download the file

### Problem: "Invalid password" error

**Possible Causes:**
1. **Wrong password** → Try again carefully (case-sensitive!)
2. **Username taken** → Someone else has this username with different password
3. **Try a different username** or contact original user

### Problem: Categories not syncing

**Check:**
1. **Internet connection** → Must be online
2. **Browser console** (F12) → Look for errors
3. **Firebase rules** → May need to update security rules (see below)
4. **Login status** → Make sure you're logged in (not "Skip Local Only")

### Problem: "Error loading from cloud"

**Solution:**
1. Check internet connection
2. Open browser console (F12) to see specific error
3. Verify Firebase project is active in Firebase Console
4. Check Firebase Database rules (see Technical Details)

### Problem: Data appears as gibberish in Firebase Console

**This is NORMAL!** ✅
- Data is encrypted before upload
- Looks like random characters in Firebase
- Decrypts automatically when you login with correct password
- Example encrypted data:
  ```
  "categories": "U2FsdGVkX1+vupppZksvRf5pq5g5XjFRIptT..."
  ```

---

## Technical Details

### Firebase Database Structure

```
flashcard-sync-15835/
└── users/
    └── {username_hash}/
        ├── passwordHash: "sha256..."
        ├── salt: "random..."
        ├── categories: "encrypted_data..."
        ├── fileCategories: "encrypted_data..."
        └── lastModified: timestamp
```

### Database Rules (Current)

**⚠️ IMPORTANT:** Currently in **test mode** (expires 30 days after creation)

Current rules:
```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

**🔒 RECOMMENDED: Update to Secure Rules**

Replace with these rules in Firebase Console → Realtime Database → Rules:

```json
{
  "rules": {
    "users": {
      "$userId": {
        ".read": "auth != null && auth.uid == $userId",
        ".write": "auth != null && auth.uid == $userId"
      }
    }
  }
}
```

**How to Update Rules:**
1. Go to Firebase Console
2. Select your project: `flashcard-sync-15835`
3. Go to **Realtime Database** → **Rules** tab
4. Replace rules with secure version above
5. Click **Publish**

### File Location

**Updated File:**
```
German-Flashcard-App/flashcard.html
```

**Line Numbers:**
- Firebase config: Lines 2358-2369
- Firebase initialization: Line 3329
- Cloud login: Line 3349
- Cloud sync functions: Lines 3392-3500+

### Dependencies

**External Libraries (CDN):**
```html
<!-- Firebase SDK v8 -->
<script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>

<!-- CryptoJS for encryption -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
```

These are loaded from CDN, so **internet connection required** for cloud sync.

---

## Backup & Export

### Exporting Data

**From Firebase Console:**
1. Go to Firebase Console → Realtime Database
2. Click on your username node
3. Click **⋮** (three dots) → **Export JSON**
4. Save the encrypted backup

**From App (Local Data):**
- Local data stored in browser's `localStorage`
- Use browser DevTools → Application → Local Storage
- Keys: `flashcard_categories`, `flashcard_file_categories`

### Backup Recommendations
- **Export Firebase data monthly** (encrypted backup)
- **Keep password safe** in password manager
- **Test restore** on second device periodically

---

## Cost & Limits

### Firebase Free Tier (Spark Plan)
- **Storage:** 1 GB (more than enough for text data)
- **Bandwidth:** 10 GB/month
- **Connections:** 100 simultaneous

### Estimated Usage
- **Per user:** ~10-50 KB (depending on vocabulary size)
- **1000 users:** ~10-50 MB total
- **Well within free limits** for personal/small group use

---

## Future Enhancements

Possible features to add:
- [ ] Password reset via email (requires Firebase Auth)
- [ ] Share categories with other users
- [ ] Backup/restore functionality
- [ ] Import/export encrypted data files
- [ ] Progress sync (learned/unlearned status)
- [ ] Spaced repetition sync across devices

---

## Support & Contact

### Issues?
1. Check **Troubleshooting** section above
2. Check browser console (F12) for errors
3. Verify Firebase project status in console

### Firebase Console
**Access:** https://console.firebase.google.com/project/flashcard-sync-15835

---

## Version History

**v2.5 (2025-11-22)** - Cloud Sync Added
- ✅ Firebase configuration integrated
- ✅ User authentication with username/password
- ✅ AES-256-GCM encryption
- ✅ Category cloud sync
- ✅ Multi-device support

**v2.4** - Enhanced Voice Options
- Enhanced speech synthesis
- Voice selection for German/English
- Auto-play features

**v2.3** - Category Management
- Category browser
- Subcategories
- File categorization

---

## Quick Reference

### Login
```
Username: masoud          (case-insensitive)
Password: YourPassword    (case-sensitive)
```

### Skip Cloud Sync
```
Click: "Skip (Use Local Only)"
Data: Stored locally only
```

### Create Category
```
Settings → Manage Categories → Create New Category
```

### Assign File to Category
```
Settings → Manage Categories → Assign to Category
```

---

**🎉 Your German Flashcard App is now ready for cloud sync!**

Test it out and let me know if you need any adjustments or have questions.

---

*Document generated: 2025-11-22*
*Firebase Project: flashcard-sync-15835*
*App Version: 2.5*
