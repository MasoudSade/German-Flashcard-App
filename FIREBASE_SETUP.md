# Firebase Cloud Sync Setup Guide

## ⏱️ Takes only 2 minutes!

Follow these simple steps to enable cloud sync for your flashcard categories.

---

## Step 1: Create Firebase Project (1 minute)

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add project"**
3. Enter project name: `flashcard-sync` (or any name you like)
4. Click **Continue**
5. Disable Google Analytics (not needed) → Click **Continue**
6. Wait for project to be created → Click **Continue**

---

## Step 2: Create Realtime Database (30 seconds)

1. In the left sidebar, click **"Realtime Database"**
2. Click **"Create Database"**
3. Select location: **United States** (or closest to you)
4. Start in **"Test mode"** → Click **Enable**

---

## Step 3: Get Your Firebase Config (30 seconds)

1. Click the **gear icon** (⚙️) next to "Project Overview"
2. Click **"Project settings"**
3. Scroll down to **"Your apps"** section
4. Click the **Web icon** `</>`
5. Enter app nickname: `flashcard-app`
6. Click **"Register app"**
7. You'll see the **firebaseConfig** object - **COPY IT**

It looks like this:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyC...",
  authDomain: "flashcard-sync-12345.firebaseapp.com",
  databaseURL: "https://flashcard-sync-12345-default-rtdb.firebaseio.com",
  projectId: "flashcard-sync-12345",
  storageBucket: "flashcard-sync-12345.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef123456"
};
```

---

## Step 4: Add Config to Flashcard App (30 seconds)

1. Open `flashcard.html` in a text editor
2. Search for: `YOUR_API_KEY_HERE`
3. You'll find this section:

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY_HERE",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.firebaseio.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

4. **REPLACE** it with your config from Step 3
5. **Save** the file

---

## ✅ Done! Now Test It

1. Open `flashcard.html` in your browser
2. Enter a username and password (create new account)
3. Create some categories
4. Open the app on another device or browser
5. Login with same username/password
6. Your categories will sync automatically! ☁️

---

## 🔐 Security Notes

- **Your data is encrypted** with your password before uploading
- **No one can read your data** without your password (not even you!)
- **Username is NOT case-sensitive**: "masoud" = "MASOUD" = "Masoud"
- **Password is case-sensitive**: "Pass123" ≠ "pass123"
- **Keep your password safe** - you cannot recover it if lost!

---

## 💡 Usage Tips

**First Device:**
1. Login with username + password
2. Create categories and add vocabulary
3. Categories auto-sync to cloud ☁️

**Second Device:**
1. Login with SAME username + password
2. Categories load automatically!
3. Any changes sync across all devices

**Skip Cloud Sync:**
- Click "Skip (Use Local Only)" to use without cloud sync
- Data will only be stored on this device
- You can enable cloud sync later

---

## 🆓 Cost

Firebase free tier includes:
- **1 GB storage** (enough for millions of flashcards!)
- **10 GB bandwidth/month**
- **100 simultaneous connections**

This is more than enough for personal use. You won't pay anything unless you have thousands of users.

---

## ❓ Troubleshooting

**Login shows "Cloud sync not configured":**
- You skipped Step 4 - add your Firebase config to flashcard.html

**"Invalid password" error:**
- Wrong password (remember it's case-sensitive!)
- OR someone else already used this username with different password
- Try a different username

**Categories not syncing:**
- Check internet connection
- Check browser console (F12) for errors
- Verify Firebase config is correct

**Want to use a different Firebase project:**
- Just replace the firebaseConfig in flashcard.html with new config

---

## 🔒 Privacy

**What gets synced to Firebase:**
- Your categories (vocabulary word pairs only)
- Your fileCategories (category assignments)
- Encrypted with AES-256-GCM encryption

**What does NOT get synced:**
- File paths
- Personal information
- Voice recordings
- Progress statistics
- Any file content outside categories

---

**Last Updated:** 2025-11-21
**Version:** 2.5 (Cloud Sync)
