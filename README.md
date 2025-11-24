# 🇩🇪 German-English Flashcards v2.5.4 🇬🇧

A powerful, feature-rich flashcard application for learning German vocabulary with cloud synchronization, spaced repetition, and advanced speech synthesis.

![Version](https://img.shields.io/badge/version-2.5.4-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active-success)

---

## 📋 Table of Contents

- [Features](#-features)
- [Quick Start](#-quick-start)
- [Installation](#-installation)
- [Usage Guide](#-usage-guide)
- [Cloud Sync Setup](#-cloud-sync-setup)
- [Recent Updates](#-recent-updates-v254)
- [Technical Details](#-technical-details)
- [Keyboard Shortcuts](#-keyboard-shortcuts)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Features

### Core Features
- **📚 CSV File Import** - Import vocabulary from CSV files with intelligent column detection
- **🔄 Spaced Repetition System (SRS)** - Smart algorithm tracks learning progress
- **🎙️ Text-to-Speech** - High-quality pronunciation with Google and Microsoft voices
- **☁️ Cloud Sync** - Encrypted synchronization across multiple devices
- **📊 Progress Tracking** - Detailed statistics and learning analytics
- **🎯 Practice Mode** - Distraction-free focused learning environment
- **🌙 Dark Mode Support** - Comfortable studying in any lighting

### Advanced Features
- **🗂️ Category Management** - Organize vocabulary by topics and levels
- **🔍 Smart Search** - Find cards instantly across all categories
- **📱 Responsive Design** - Works perfectly on desktop, tablet, and mobile
- **🎨 Customizable Voices** - Choose from multiple German and English voices
- **⚡ Auto-Play Mode** - Automated pronunciation for hands-free learning
- **📈 Review Scheduling** - Optimal timing based on learning science
- **💾 Auto-Save** - Never lose your progress
- **🔐 Secure Encryption** - AES-256-GCM encryption for cloud data

---

## 🚀 Quick Start

### For First-Time Users

1. **Open the App**
   ```
   Simply open flashcard.html in your web browser
   ```

2. **Upload Your Vocabulary**
   - Click "📁 Upload CSV File"
   - Select your vocabulary file
   - Choose column mappings (German, English, etc.)

3. **Start Learning**
   - Click "🎯 Start Practice Mode"
   - Use arrow keys or buttons to navigate
   - Mark words as learned

4. **Enable Cloud Sync (Optional)**
   - Click the account button (top-right)
   - Create an account or login
   - Your data syncs automatically

---

## 💻 Installation

### Option 1: Direct Use (No Installation)
1. Download `flashcard.html`
2. Open in any modern web browser
3. Start learning immediately

### Option 2: Local Server (Recommended for Development)
```bash
# Clone the repository
git clone [repository-url]
cd German-Flashcard-App-Public

# Open with a local server (Python)
python -m http.server 8000

# Open in browser
http://localhost:8000/flashcard.html
```

### Requirements
- **Browser:** Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **Internet:** Required only for cloud sync
- **Storage:** ~5MB for app, variable for vocabulary data

---

## 📖 Usage Guide

### Uploading Vocabulary Files

**Supported Formats:**
- CSV files (UTF-8 encoded)
- Columns: German, English, Details (optional)
- Example format:
  ```csv
  German,English,Details
  Hallo,Hello,Common greeting
  Tschüss,Goodbye,Informal farewell
  ```

**Upload Steps:**
1. Click "📁 Upload CSV File"
2. Select your file
3. App auto-detects columns
4. Confirm or adjust mappings
5. Choose category and subcategory
6. Click "Load Flashcards"

### Learning Modes

#### **Practice Mode** 🎯
- Clean, distraction-free interface
- Focused on current flashcard
- Quick navigation with keyboard
- Settings accessible during practice

**Activate:** Click "🎯 Start Practice Mode"

#### **Review Mode** 📚
- Shows all flashcards in sequence
- Full navigation controls visible
- Detailed statistics panel
- Category browser accessible

### Marking Progress

**Learning States:**
- **New** 🆕 - Not yet studied
- **Learning** 📖 - Currently studying
- **Learned** ✓ - Mastered (marked as learned)
- **Due for Review** 🔔 - Ready to review based on SRS

**Actions:**
- Click ✓ button to mark as learned
- Review scheduling happens automatically
- Progress saves instantly

---

## ☁️ Cloud Sync Setup

### Setting Up Firebase (For Your Own Deployment)

1. **Create Firebase Project**
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Create new project
   - Enable Realtime Database

2. **Get Configuration**
   - Project Settings → General
   - Scroll to "Your apps" → Web app
   - Copy configuration object

3. **Update flashcard.html**
   ```javascript
   // Find the Firebase configuration section (around line 5240)
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "YOUR_PROJECT.firebaseapp.com",
       databaseURL: "https://YOUR_PROJECT.firebaseio.com",
       projectId: "YOUR_PROJECT_ID",
       storageBucket: "YOUR_PROJECT.appspot.com",
       messagingSenderId: "YOUR_SENDER_ID",
       appId: "YOUR_APP_ID"
   };
   ```

4. **Set Database Rules**
   ```json
   {
     "rules": {
       "users": {
         "$username": {
           ".read": "$username === auth.uid",
           ".write": "$username === auth.uid"
         }
       }
     }
   }
   ```

### Using Cloud Sync

1. **Create Account**
   - Click account button (top-right)
   - Choose "Sign Up"
   - Enter username (min 3 chars) and password (min 6 chars)
   - Data encrypts automatically

2. **Login**
   - Click account button
   - Enter credentials
   - Data downloads and syncs

3. **Sync Across Devices**
   - Login with same credentials on any device
   - All vocabulary and progress syncs automatically
   - Works offline, syncs when online

---

## 🆕 Recent Updates (v2.5.4)

### January 24, 2025

**🐛 Bug Fixes:**
1. Fixed Practice Mode button deformation
2. Settings menu now accessible in Practice Mode
3. Card counts display correctly in file tree

**✨ New Features:**
1. Card count shown alongside file count (e.g., "1 file, 600 cards")
2. Complete flashcard data now syncs to cloud (not just metadata)

**🔧 Improvements:**
1. Enhanced cloud sync reliability
2. Better card counting across all categories
3. Improved Practice Mode UI stability

**📖 Full Changelog:** See `CHANGELOG_2025-01-24.md`

---

## 🔧 Technical Details

### Technologies Used
- **Frontend:** Pure HTML5, CSS3, JavaScript (ES6+)
- **Speech:** Web Speech API (Google/Microsoft voices)
- **Storage:** LocalStorage API
- **Cloud:** Firebase Realtime Database
- **Encryption:** AES-256-GCM (Web Crypto API)
- **Architecture:** Single-page application (SPA)

### Browser Compatibility
| Browser | Version | Status |
|---------|---------|--------|
| Chrome  | 90+     | ✅ Fully Supported |
| Firefox | 88+     | ✅ Fully Supported |
| Safari  | 14+     | ✅ Fully Supported |
| Edge    | 90+     | ✅ Fully Supported |
| Opera   | 76+     | ✅ Fully Supported |

### Performance
- **Load Time:** < 1 second (local)
- **File Size:** ~350KB uncompressed
- **Storage:** ~2KB per 100 flashcards
- **Memory Usage:** ~10-20MB typical
- **Offline:** Full functionality except cloud sync

### Data Storage
- **LocalStorage Keys:**
  - `flashcards_{filename}` - Card data
  - `flashcard_categories` - Category structure
  - `flashcard_file_categories` - File mappings
  - `cloud_user` - Encrypted login info

---

## ⌨️ Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `→` | Next card |
| `←` | Previous card |
| `Space` | Reveal/Hide answer |
| `G` | Pronounce German |
| `E` | Pronounce English |
| `L` | Mark as learned |
| `Esc` | Exit Practice Mode |
| `S` | Open Settings |
| `F` | Toggle Focus Mode |

---

## 🔍 Troubleshooting

### Common Issues

**Issue: Cards not loading from cloud**
- **Solution:** Ensure you've uploaded data after update to v2.5.4
- Hard refresh: `Ctrl + Shift + R` (Windows) or `Cmd + Shift + R` (Mac)

**Issue: Voice not working**
- **Solution:** Check browser speech synthesis support
- Try different voice from Settings → Voice & Speech
- Ensure browser has permission for audio

**Issue: Settings not visible**
- **Solution:** Click Settings button (⚙️), then expand accordion sections
- Hard refresh if recently updated

**Issue: Progress not saving**
- **Solution:** Check LocalStorage isn't full (typical limit: 5-10MB)
- Verify browser allows LocalStorage
- Try clearing other site data

**Issue: Cloud sync failing**
- **Solution:** Check internet connection
- Verify Firebase configuration
- Re-login to refresh authentication

### Debug Mode

Open browser console (`F12`) to see detailed logs:
- Voice loading status
- File loading progress
- Cloud sync operations
- Error messages with context

---

## 🤝 Contributing

### How to Contribute
1. Fork the repository
2. Create feature branch: `git checkout -b feature-name`
3. Make your changes
4. Test thoroughly
5. Commit: `git commit -m 'Add feature'`
6. Push: `git push origin feature-name`
7. Create Pull Request

### Development Guidelines
- Follow existing code style
- Add comments for complex logic
- Test on multiple browsers
- Update documentation
- No breaking changes without discussion

### Reporting Issues
- Use GitHub Issues
- Include browser and version
- Provide steps to reproduce
- Attach screenshots if relevant
- Check existing issues first

---

## 📄 License

MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## 🙏 Acknowledgments

- Voice synthesis powered by Google and Microsoft TTS
- Firebase for cloud infrastructure
- Web Crypto API for secure encryption
- Open-source community for inspiration

---

## 📞 Support

- **Documentation:** See `/docs` folder
- **Issues:** GitHub Issues
- **Updates:** Check CHANGELOG files
- **Questions:** Open a discussion

---

## 🗺️ Roadmap

### Planned Features
- [ ] Image support for vocabulary
- [ ] Audio recording for pronunciation
- [ ] Gamification elements
- [ ] Study groups and sharing
- [ ] Mobile app versions
- [ ] More language pairs
- [ ] AI-powered suggestions

---

**Happy Learning! 🎓**

*Made with ❤️ for language learners everywhere*
