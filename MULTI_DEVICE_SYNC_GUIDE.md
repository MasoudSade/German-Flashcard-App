# 🔄 Multi-Device Sync Guide - German Flashcard App

**Your Account is Working!** 🎉
Now learn how to access your data from multiple devices.

---

## 📋 **Quick Overview**

### What You Have Now:
- ✅ Account created and logged in
- ✅ Data syncing to Firebase Cloud
- ✅ Can access from any device with login credentials

---

## 🎯 **How Cloud Sync Works**

### When You Create Categories:
```
Your Device → Upload to Firebase → ☁️ Cloud Storage
```

### When You Login on Another Device:
```
☁️ Cloud Storage → Download to Device → Shows in App
```

### Automatic Sync:
- Every time you create/edit a category → Auto-uploads
- Every time you login → Auto-downloads latest data
- Real-time synchronization

---

## 👤 **Your Account Information**

### Login Credentials:
```
Username: [your username]
Password: [your password - KEEP THIS SAFE!]
```

**IMPORTANT:**
- ⚠️ Password CANNOT be recovered if forgotten!
- ⚠️ Write it down in a password manager
- ⚠️ No password reset functionality (by design for security)

### Your Data Location:
```
Firebase Console: https://console.firebase.google.com/project/flashcard-sync-15835/database
Database URL: https://flashcard-sync-15835-default-rtdb.firebaseio.com
Your Data: Encrypted under "users/[your-username]/"
```

---

## 🧪 **Test Multi-Device Sync**

### **Test 1: Different Browser (Same Computer)**

**Step 1: Prepare Data on Current Browser**
1. Upload a vocabulary CSV file
2. Create a test category (e.g., "Test Category A1")
3. Assign your file to that category
4. Wait for sync indicator to show "☁️ Synced"
5. **Remember:** Your username and password

**Step 2: Open Different Browser**
1. Open Chrome/Firefox/Edge (whichever you're NOT using now)
2. Open `flashcard.html`
3. Enter your username and password
4. Click "Login"

**Expected Result:**
- ✅ Login successful
- ✅ See "Test Category A1" in category browser
- ✅ Category structure matches your first browser

**Note:** You'll need to re-upload CSV files on new browser (file paths are local).

---

### **Test 2: Incognito/Private Window**

**Step 1: Keep Current Session Open**
- Don't logout or close your browser

**Step 2: Open Private Window**
- Chrome: `Ctrl+Shift+N`
- Edge: `Ctrl+Shift+P`
- Firefox: `Ctrl+Shift+P`

**Step 3: Navigate to Flashcard App**
- Open `flashcard.html` in private window
- Login with your credentials

**Expected Result:**
- ✅ Same categories appear
- ✅ Both windows can work independently
- ✅ Changes in one sync to the other

---

### **Test 3: Another Computer/Device**

**Preparation:**
1. Make sure data is synced on first device
2. Note your login credentials
3. Copy `flashcard.html` to USB drive or cloud storage

**On Second Device:**
1. Copy `flashcard.html` to the device
2. Open it in browser
3. Login with SAME username and password
4. Wait for data to download

**Expected Result:**
- ✅ All categories appear automatically
- ✅ Category structure is identical
- ✅ Any changes sync between devices

---

## 📊 **What Syncs vs What Doesn't**

### ✅ Synced to Cloud (Accessible Everywhere)

| Data Type | Synced? | Details |
|-----------|---------|---------|
| Categories | ✅ Yes | Main categories and subcategories |
| File-Category Assignments | ✅ Yes | Which files belong to which categories |
| Category Structure | ✅ Yes | Full hierarchy of categories |
| Account Info | ✅ Yes | Username and password hash |

### ❌ NOT Synced (Device-Specific)

| Data Type | Synced? | Why Not? |
|-----------|---------|----------|
| CSV Files | ❌ No | Files are stored locally on each device |
| File Paths | ❌ No | Paths are specific to each device |
| Progress Tracking | ❌ No | Learned/unlearned status is local |
| Voice Settings | ❌ No | User preferences are local |
| Session Statistics | ❌ No | Study time/cards reviewed are local |

---

## 🔄 **Typical Multi-Device Workflow**

### **Device 1 (Home Computer):**
```
1. Login with username/password
2. Upload CSV files (e.g., German_A1.csv, German_A2.csv)
3. Create categories:
   - German A1
     └ A1 Vocabulary
     └ A1 Verbs
   - German A2
     └ A2 Vocabulary
4. Assign files to categories
5. Study using flashcards
6. Categories AUTO-SYNC to cloud ☁️
```

### **Device 2 (Work Laptop):**
```
1. Copy flashcard.html to work laptop
2. Login with SAME username/password
3. Categories AUTO-DOWNLOAD from cloud
4. Re-upload CSV files (German_A1.csv, German_A2.csv)
5. Files automatically assigned to existing categories
6. Study using flashcards
7. Any new categories created sync back to cloud
```

### **Device 3 (Mobile - If Using):**
```
1. Open flashcard.html on mobile browser
2. Login with credentials
3. Download and see all categories
4. Upload CSV files
5. Study on-the-go
6. Everything syncs!
```

---

## 🛡️ **Data Security & Privacy**

### Your Data is Encrypted:
```
Plain Text → AES-256-GCM Encryption → Encrypted Data → Upload to Cloud
```

### What This Means:
- ✅ Your vocabulary is encrypted BEFORE uploading
- ✅ Only YOU can decrypt it (with your password)
- ✅ Not even Firebase admins can read your data
- ✅ Zero-knowledge architecture

### Encryption Key:
- Derived from your password
- Never stored anywhere
- Changes if you change password

---

## 👀 **How to Check if Data is Syncing**

### Method 1: Sync Status Indicator
Look for the sync indicator in your app:
- ☁️ "Synced" = Data uploaded successfully
- 🔄 "Syncing..." = Upload in progress
- ⚠️ "Error syncing" = Something went wrong
- 📡 "Offline" = No internet connection

### Method 2: Firebase Console
1. Go to: https://console.firebase.google.com/project/flashcard-sync-15835/database
2. Click "Data" tab
3. Expand tree: `users` → `[your username]`
4. You should see:
   ```
   users/
     └ [your username]/
         ├ passwordHash: "sha256..."
         ├ salt: "random..."
         ├ categories: "encrypted blob..."
         ├ fileCategories: "encrypted blob..."
         └ lastModified: timestamp
   ```

### Method 3: Browser Console
1. Open flashcard.html
2. Press F12 (open console)
3. Look for messages:
   ```
   ✓ Data synced to cloud
   ✓ Data loaded from cloud
   ☁️ Synced
   ```

---

## 🔧 **Manage Your Account**

### View Account Data:
Currently the app doesn't have a dedicated "account settings" page, but you can:

1. **See sync status:** Look at the sync indicator
2. **Logout:** Close browser or clear localStorage
3. **View data in Firebase:** Check Firebase Console

### Logout:
To logout (clear local session):
1. Open browser console (F12)
2. Type: `localStorage.clear()`
3. Press Enter
4. Refresh page

### Change Password:
Not currently supported in v2.5. You would need to:
1. Create a new account with different username
2. Re-create your categories
3. Old account remains in database

### Delete Account:
Not currently supported in UI. To delete:
1. Go to Firebase Console
2. Navigate to Realtime Database
3. Find your username under "users"
4. Click ⋮ (three dots) → Delete

---

## 🎯 **Real-World Usage Scenarios**

### Scenario 1: Home & Work
```
Morning at Home:
- Study German vocabulary
- Create new categories for business terms
- Upload business German CSV

Evening at Work:
- Login on work computer
- See business German categories (auto-synced!)
- Upload same CSV file
- Continue studying from where you left off
```

### Scenario 2: Preparing for Exam
```
Week 1 (Desktop):
- Upload all vocabulary for exam
- Create comprehensive categories
- Study regularly

Week 2 (Laptop + Mobile):
- Login on laptop for library study
- Categories appear automatically
- Login on mobile for bus commute
- All vocab accessible everywhere
```

### Scenario 3: Sharing Setup (Advanced)
```
You can share categories with a friend by:
1. Both using same login credentials
2. Each person can see all categories
3. Any changes sync between you

⚠️ Not recommended for private data!
Better: Each person creates their own account
```

---

## ✅ **Verification Checklist**

After setting up multi-device sync, verify:

- [ ] Created account successfully
- [ ] Uploaded vocabulary files
- [ ] Created categories
- [ ] Assigned files to categories
- [ ] See sync indicator showing "Synced"
- [ ] Data visible in Firebase Console (encrypted)
- [ ] Can login from different browser
- [ ] Categories appear after login on different browser
- [ ] Changes in one browser sync to another
- [ ] Can logout and login again successfully

---

## 🐛 **Troubleshooting Multi-Device Issues**

### Problem: Categories don't appear on second device

**Solutions:**
1. **Check internet connection** - Both devices need internet
2. **Wait for sync** - Give it 10-30 seconds after login
3. **Check credentials** - Make sure username/password are EXACTLY the same
4. **Check Firebase Console** - Verify data exists in cloud
5. **Hard reload** - Press Ctrl+F5 on second device
6. **Check console** - Press F12, look for errors

### Problem: "Invalid password" error

**Causes:**
1. **Wrong password** - Password is case-sensitive
2. **Username already taken** - Someone else used this username
3. **Typo in username** - Username is case-insensitive but must match

**Solutions:**
- Try password carefully (case-sensitive!)
- Try different username
- Check if you already created account before

### Problem: Data not syncing between devices

**Check:**
1. **Internet connection** - Both devices online?
2. **Same account** - Using same username/password?
3. **Sync indicator** - Shows "Synced" or "Error"?
4. **Firebase Console** - Data actually in cloud?
5. **Browser console** - Any error messages?

---

## 💡 **Tips for Best Experience**

### Best Practices:
1. ✅ **Use strong password** - Keep it safe!
2. ✅ **Wait for sync** - Don't logout immediately after creating categories
3. ✅ **Check sync indicator** - Verify "Synced" before closing
4. ✅ **Keep CSV files organized** - Same folder structure on all devices
5. ✅ **Test with small data first** - Create test category, verify sync, then add more

### Recommended Workflow:
```
1. Create account (once)
2. Set up categories (once, syncs everywhere)
3. On each device: Upload CSV files to match categories
4. Study from any device
5. All progress in categories stays synced
```

---

## 📞 **Quick Reference**

### Account Access:
```
Login URL: Open flashcard.html
Username: [your username]
Password: [your password]
Database: https://flashcard-sync-15835-default-rtdb.firebaseio.com
```

### Firebase Console:
```
Project: https://console.firebase.google.com/project/flashcard-sync-15835
Database: https://console.firebase.google.com/project/flashcard-sync-15835/database
Your Data: users/[your-username]/
```

### Data Structure in Firebase:
```
users/
  └ [your-username]/
      ├ passwordHash: "encrypted"
      ├ salt: "random-string"
      ├ categories: "encrypted-json"
      ├ fileCategories: "encrypted-json"
      └ lastModified: timestamp
```

---

## 🎉 **You're All Set!**

Your flashcard app now:
- ✅ Has cloud sync enabled
- ✅ Works across multiple devices
- ✅ Keeps data encrypted and private
- ✅ Syncs automatically

**Enjoy studying German from anywhere!** 🇩🇪📚

---

*Last Updated: 2025-11-22*
*Version: 2.5 (Cloud Sync Edition)*
*Account Status: Active and Syncing*
