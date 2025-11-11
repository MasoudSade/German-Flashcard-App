# 🇩🇪 German-English Flashcard App 🇬🇧

A powerful, feature-rich web-based flashcard application for learning German vocabulary with advanced learning features, spaced repetition, audio recording, and intelligent column mapping.

![Flashcard App](https://img.shields.io/badge/Version-2.3-blue) ![License](https://img.shields.io/badge/License-MIT-green) ![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black) ![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)

## ✨ Features

### 🎯 Core Features
- **📁 CSV Import** - Load vocabulary from custom CSV files with ANY column order
- **🎯 Manual Column Mapping** - Interactive UI to assign column types (NEW in v2.3!)
- **⚡ Predefined Formats** - 4 quick presets for instant setup (NEW in v2.3!)
- **🔄 Spaced Repetition** - SM-2 algorithm for optimal learning
- **💾 Progress Tracking** - Automatic localStorage persistence
- **📊 Statistics** - Real-time learning progress tracking
- **🎙️ Audio Pronunciation** - Text-to-speech for German & English
- **🎙️ Session Recording** - Record audio for offline review (NEW in v2.3!)
- **⌨️ Keyboard Shortcuts** - Fast navigation and actions

### 🚀 Advanced Features
- **▶️ Auto-Play Mode** - Hands-free learning with configurable delays
- **🔁 Loop Mode** - Continuous playback for passive learning
- **🗣️ Repeat Mode** - Repeat each card 2-5 times for reinforcement
- **⏰ Study Timer** - Pomodoro-style timed sessions (5-60 minutes)
- **📚 Sleep Timer** - Gentle bedtime learning (10-45 minutes)
- **🎯 Focus Mode** - Distraction-free fullscreen studying
- **📊 Session Statistics** - Live tracking of cards reviewed, time, pace
- **🎤 Voice Customization** - Select voices, adjust rate & pitch

### 📚 Organization Features
- **Category System** - Organize files into categories & subcategories
- **🏷️ File Mapping** - Assign CSV files to specific categories
- **🔍 Smart Filtering** - Show only unlearned cards
- **🔀 Shuffle Mode** - Randomize card order
- **✓ Mark as Learned** - Track mastered vocabulary

### 🎨 Modern UI
- **Clean Design** - Flashcard-first interface
- **Collapsible Settings** - Accordion menu with 5 organized sections
- **Quick Actions** - 4 most-used buttons always accessible
- **Responsive Layout** - Works on desktop, tablet, and mobile
- **Dark Mode Ready** - Professional purple gradient theme

## 🚀 Quick Start

### Option 1: Direct Use
1. Download `flashcard.html` and `sample_vocabulary.csv`
2. Double-click `flashcard.html` to open in your browser
3. Click "📁 Upload CSV File" and select `sample_vocabulary.csv`
4. Start learning! 🎓

### Option 2: Clone Repository
```bash
git clone https://github.com/YOUR_USERNAME/German-Flashcard-App.git
cd German-Flashcard-App
# Open flashcard.html in your browser
```

## 📋 CSV Format & Column Mapping

### 🎯 NEW in v2.3: Universal CSV Support!

The app now supports **ANY CSV format** with our new **Manual Column Mapping** feature!

### Three Ways to Load Your CSV:

#### 1. ⚡ Predefined Formats (Fastest)
Choose from 4 preset formats:
- **3-Column Standard**: German, German Example, English
- **3-Column Reverse**: English, English Example, German
- **4-Column Full**: German, German Ex., English, English Ex.
- **2-Column Simple**: German, English (no examples)

#### 2. 🎯 Manual Column Mapping (Most Flexible)
- Interactive modal shows preview of your data (10 rows)
- Click column headers to assign types
- Instant dropdown menus
- Color-coded assignments (Green=German, Blue=English, etc.)
- Perfect for custom or complex CSV files

#### 3. 🤖 Auto-Detection (Intelligent)
- AI-powered language detection
- Works for most standard formats
- Automatic fallback option

### Basic CSV Format Example:

```csv
German word,English translation,Additional details (optional)
Hallo,Hello,Common greeting
Danke,Thank you,Expression of gratitude
Brot,Bread,Food item
Wasser,Water,Beverage
```

### Extended Format (4 Columns):

```csv
German word,German sentence,English word,English sentence
Hallo,Ich sage hallo,Hello,I say hello
Wasser,Ich trinke Wasser,Water,I drink water
```

**Rules:**
- Use comma (`,`) as separator (or semicolon, pipe, tab - auto-detected!)
- At least 2 columns required
- Column order doesn't matter (use manual mapping!)
- No column headers needed (but supported)
- Save as UTF-8 encoding for special characters (ä, ö, ü)

## 🎮 How to Use

### Basic Usage
1. **Upload CSV** - Click the upload button and select your vocabulary file
2. **Choose Format** (NEW in v2.3!) - Select how to load your file:
   - Try a predefined format (fastest)
   - Use manual column mapping (full control)
   - Use auto-detection (intelligent)
3. **Study Cards** - Navigate with Next/Previous buttons or arrow keys
4. **Reveal Meaning** - Click "Show English Meaning" or press Space
5. **Mark Learned** - Press 'L' key or click "Mark as Learned" button
6. **Audio** - Press 'P' for German or 'E' for English pronunciation
7. **Record Sessions** (NEW!) - Enable recording to save audio for later

### Quick Actions (Always Visible)
- **▶️ Auto-Play** - Start automatic playback with audio
- **🔀 Shuffle** - Randomize card order
- **✓ Mark Learned** - Mark current card as learned
- **👁 Unlearned Only** - Filter to show only unlearned cards

### Settings Menu
Click **"⚙️ Settings & Options"** to access:

#### 📚 Category Management
- Create categories (e.g., "German", "French")
- Add subcategories (e.g., "A1 Vocabulary", "Business Terms")
- Assign files to categories
- View all categories in tree structure

#### 🎙️ Voice & Speech Settings
- Select German voice from available system voices
- Select English voice
- Adjust speech rate (0.5x - 1.5x)
- Adjust pitch (0.5 - 2.0)

#### ▶️ Auto-Play Settings
- Enable/disable English pronunciation
- Set delay between German & English (0.5s - 3s)
- Set delay before next card (1s - 5s)
- **🎙️ Record Session Audio** (NEW v2.3!) - Record entire session for later review
  - Automatic save on completion
  - Prompt to save/discard on manual stop
  - Download as .webm audio file
  - Play recording directly in browser

#### 🎯 Advanced Features
- **Loop Mode** - Restart from beginning automatically
- **Repeat Mode** - Play each card 2-5 times
- **Study Timer** - Auto-stop after set time (5-60 min)
- **Sleep Timer** - Gentle stop for bedtime learning (10-45 min)

#### 👁️ Display Options
- Always show English meanings (no reveal needed)
- Enter Focus Mode (fullscreen, zero distractions)
- Reset All Progress

## ⌨️ Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `←` / `→` | Previous / Next card |
| `Space` / `Enter` | Reveal English meaning |
| `P` | Pronounce German word |
| `E` | Pronounce English word |
| `L` | Mark as Learned / Unlearned |

## 📊 Learning Strategies

### For Beginners
1. Enable English pronunciation in Auto-Play
2. Set speech rate to 0.7x (slower)
3. Use Repeat Mode (3 times per card)
4. Study 10-15 minutes daily
5. Mark cards as learned only when confident

### For Intermediate Learners
1. Disable English pronunciation (test yourself)
2. Set speech rate to 0.9x
3. Use Shuffle mode for variety
4. Study 20-30 minutes daily
5. Focus on "Show Only Unlearned" cards

### For Advanced Learners
1. Use Loop Mode for background listening
2. Speech rate 1.0x or faster
3. Repeat Mode OFF (challenge yourself)
4. Study during commute/exercise
5. Create topic-specific vocabulary files

### Spaced Repetition Usage
- The app uses SM-2 algorithm automatically
- Cards appear more/less frequently based on your performance
- Review cards when "due for review" notification shows
- Trust the system - it's scientifically proven!

## 🗂️ Organizing Your Vocabulary

### Category System Example

```
📁 German
   ├─ A1 Vocabulary (beginner words)
   ├─ A2 Vocabulary (elementary words)
   ├─ Business Terms (work-related)
   └─ Travel Phrases (tourism)

📁 French
   ├─ Beginner
   └─ Cooking Terms

📁 Spanish
   └─ Travel
```

### Best Practices
- Create main categories by language
- Use subcategories for difficulty levels or topics
- Assign each CSV file to a specific category
- Keep files under 500 cards for best performance
- Name files clearly (e.g., `german_a1_vocab.csv`)

## 💾 Data Persistence

### What is Saved Automatically?
✅ **Categories & Subcategories** - All created categories
✅ **File Assignments** - Which file belongs to which category
✅ **Card Progress** - Which cards are marked as learned
✅ **Review Schedules** - Spaced repetition data

### What is NOT Saved?
❌ **CSV File Content** - You must re-upload each session
❌ **Voice Settings** - Reset each session
❌ **Auto-play Settings** - Reset each session

### Data Location
- All data stored in browser's `localStorage`
- No server, no account needed
- Privacy-friendly (stays on your device)
- Data persists until you clear browser data

## 📱 Mobile Usage

Works perfectly on mobile browsers!

1. Transfer `flashcard.html` to your phone
2. Open with any browser (Chrome, Safari, Firefox)
3. Upload CSV files from your phone
4. Study on the go!

**Mobile Tips:**
- Use Auto-Play for hands-free learning
- Enable Loop Mode for commute listening
- Quick Actions are touch-friendly
- Settings accordion saves screen space

## 🌐 Browser Compatibility

| Browser | Status | Notes |
|---------|--------|-------|
| Chrome / Edge | ✅ Fully Supported | Best experience |
| Firefox | ✅ Fully Supported | All features work |
| Safari | ✅ Fully Supported | iOS & macOS |
| Opera | ✅ Fully Supported | All features work |
| Mobile Browsers | ✅ Fully Supported | Responsive design |

**Requirements:**
- JavaScript enabled
- localStorage available (not in private/incognito mode)
- Web Speech API for audio (most modern browsers)

## 🌐 Hosting Your App Online

Want to access your flashcard app from anywhere? Check out our comprehensive hosting guides!

### Quick Start Options:

1. **[GitHub Pages](GITHUB_PAGES_SETUP.md)** (RECOMMENDED)
   - 100% FREE forever
   - 5-minute setup
   - HTTPS included
   - Perfect for beginners
   - Your app is already on GitHub!

2. **[Home Router + WireGuard VPN](WIREGUARD_SETUP.md)**
   - FREE (use your home internet)
   - Private and secure
   - Full control
   - Requires technical knowledge

3. **[Complete Hosting Guide](HOSTING_GUIDE.md)**
   - All hosting options compared
   - Domain setup instructions
   - Security best practices
   - Free and paid options

**Easiest:** Enable GitHub Pages in repository settings → Access from anywhere!

## 📚 Documentation

Comprehensive guides available:

### Getting Started
- **[HOSTING_GUIDE.md](HOSTING_GUIDE.md)** - Complete hosting solutions guide
- **[GITHUB_PAGES_SETUP.md](GITHUB_PAGES_SETUP.md)** - 5-minute setup for free hosting
- **[WIREGUARD_SETUP.md](WIREGUARD_SETUP.md)** - Private VPN access guide
- **[QUICK_START_v2.0.md](QUICK_START_v2.0.md)** - Quick start guide
- **[UPGRADE_SUMMARY.txt](UPGRADE_SUMMARY.txt)** - Upgrade information

### Version History
- **[VERSION_2.3_CHANGELOG.md](VERSION_2.3_CHANGELOG.md)** - Latest features (v2.3)
- **[VERSION_2.0_CHANGELOG.md](VERSION_2.0_CHANGELOG.md)** - Smart detection features
- **[FIXES_v2.1.md](FIXES_v2.1.md)** - Bug fixes and improvements

### Feature Guides (in `/docs` folder)
- **README.txt** - User guide and feature overview
- **CATEGORY_GUIDE.txt** - Complete category system documentation
- **VOICE_SETTINGS_GUIDE.txt** - Voice customization guide
- **AUTOPLAY_GUIDE.txt** - Auto-play feature tutorial
- **ADVANCED_FEATURES_GUIDE.txt** - All 8 advanced features explained
- **UI_REDESIGN_GUIDE.txt** - New interface documentation
- **TESTING_PERSISTENCE.txt** - How to verify data persistence

## 🛠️ Technical Stack

- **HTML5** - Structure and markup
- **CSS3** - Modern styling with gradients and animations
- **Vanilla JavaScript** - No frameworks, pure JS
- **Web Speech Synthesis API** - Audio pronunciation
- **localStorage** - Data persistence
- **FileReader API** - CSV file parsing

**Key Algorithms:**
- SM-2 Spaced Repetition Algorithm
- CSV parsing with validation
- Category tree data structure

## 🤝 Contributing

Contributions are welcome! Here are some areas for improvement:

- [ ] Multi-language support (beyond German-English)
- [ ] Export/import settings and categories
- [ ] Drag-and-drop file upload
- [ ] Image support for flashcards
- [ ] Dark theme toggle
- [ ] Offline Progressive Web App (PWA)
- [ ] Cloud sync (optional)
- [ ] Card creation UI (no CSV needed)

## 📄 License

MIT License - Feel free to use, modify, and distribute!

## 👨‍💻 Author

Created with ❤️ for language learners everywhere

## 🙏 Acknowledgments

- Spaced Repetition algorithm based on SuperMemo's SM-2
- Inspired by Anki and other flashcard systems
- Built for efficient, effective language learning

## 📞 Support

- **Bug Reports:** Open an issue on GitHub
- **Feature Requests:** Open an issue with "enhancement" label
- **Questions:** Check documentation in `/docs` folder

## 🎓 Use Cases

Perfect for:
- 📚 Language learning (German, French, Spanish, etc.)
- 🎯 Vocabulary memorization
- 📖 Exam preparation
- 🗣️ Pronunciation practice
- 🚗 Commute learning (Auto-Play mode)
- 🛌 Bedtime review (Sleep Timer)
- 🎓 Student study sessions (Study Timer)
- 👨‍🏫 Teaching aid for educators

## 🌟 Star This Project!

If you find this helpful, please ⭐ star this repository!

---

**Happy Learning! 🎉 Viel Erfolg! 🇩🇪**
