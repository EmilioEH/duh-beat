# DuhBeat - Beat Maker Flutter Web App

A beat maker web application built with Flutter that allows users to record audio samples and trigger them.

## ✅ Project Setup Complete

Your Flutter web project is now configured with:

### Development Tools
- **Flutter SDK** - Latest stable version
- **flutter_lints** - Strict code quality rules (enabled)
- **dart_code_metrics** - Code complexity analysis
- **record** - Audio recording (Web Audio API)
- **just_audio** - Audio playback
- **provider** - State management

### Code Quality
All lint rules are configured with strict type checking enabled:
- `strict-casts: true`
- `strict-raw-types: true`
- 80+ lint rules for code consistency

Run linting with:
```bash
flutter analyze
```

## 📁 Project Structure

```
DuhBeat/
├── lib/
│   └── main.dart              # App entry point
├── web/
│   └── index.html             # Web entry point
├── pubspec.yaml               # Dependencies
├── analysis_options.yaml      # Linting rules
└── build/
    └── web/                   # Build output (for GitHub Pages)
```

## 🚀 Local Development

### Run in development mode:
```bash
flutter run -d chrome
```

### Build for production:
```bash
flutter build web --release
```

The web build output is in `build/web/` - this is what gets deployed to GitHub Pages.

## 📦 Required Web Audio Permissions

Your app needs to request microphone permissions for recording. Users will see a browser permission prompt.

## 🌐 GitHub Pages Deployment

### Option 1: Automatic Deployment (Recommended)

1. **Initialize Git Repository** (if not already done):
```bash
cd /Users/emilioharrison/Code/DuhBeat
git init
git add .
git commit -m "Initial Flutter web app setup"
```

2. **Create GitHub Repository**:
   - Go to https://github.com/new
   - Create repository named `duhbeat`
   - Don't initialize with README (since you already have one locally)

3. **Connect and Push**:
```bash
git remote add origin https://github.com/YOUR_USERNAME/duhbeat.git
git branch -M main
git push -u origin main
```

4. **Setup GitHub Pages**:
   - Go to repository Settings → Pages
   - Source: Deploy from a branch
   - Branch: main
   - Folder: / (root)
   - Click Save

5. **Create GitHub Actions Workflow** for automatic builds:

Create `.github/workflows/deploy.yml`:
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.38.9'
      
      - name: Install dependencies
        run: flutter pub get
      
      - name: Run analysis
        run: flutter analyze
      
      - name: Build web
        run: flutter build web --release --web-renderer html
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build/web
```

Your app will be available at: `https://YOUR_USERNAME.github.io/duhbeat/`

### Option 2: Manual Deployment

After building:
```bash
# Build the web app
flutter build web --release

# Copy build output to gh-pages branch (if you prefer this method)
git checkout --orphan gh-pages
git rm -rf .
git add build/web/.
git commit -m "Deploy web app"
git push -u origin gh-pages
```

Then set GitHub Pages source to the `gh-pages` branch.

## 📝 Next Steps

1. **Implement Beat Maker UI** in `lib/main.dart`:
   - Sample pads (buttons to trigger sounds)
   - Recording interface
   - Playback controls

2. **Add Audio Logic**:
   - Record audio samples using `record` package
   - Store samples in memory or browser storage
   - Implement triggering with `just_audio`

3. **Enhance Features**:
   - Sample management (save/load)
   - BPM/tempo control
   - Effects (reverb, delay, etc.)
   - Export functionality

4. **Testing**:
   - Add unit tests in `test/` folder
   - Test audio recording/playback
   - Test state management with provider

## 🔍 Available Commands

```bash
# Development
flutter run -d chrome              # Run in Chrome
flutter run -d web-server          # Run on localhost:8080

# Code Quality
flutter analyze                    # Run linter
flutter format lib/               # Format code
flutter pub get                    # Install dependencies

# Building
flutter build web --release        # Production build
flutter build web --profile        # Profile build
flutter build web --debug          # Debug build
```

## 📚 Resources

- [Flutter Web Documentation](https://flutter.dev/multi-platform/web)
- [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
- [Record Package](https://pub.dev/packages/record)
- [Just Audio Package](https://pub.dev/packages/just_audio)
- [Provider Package](https://pub.dev/packages/provider)
- [GitHub Pages](https://pages.github.com/)

## ⚠️ Browser Support

Your beat maker will work on:
- ✅ Chrome/Chromium (best support)
- ✅ Firefox
- ✅ Safari 14+
- ✅ Edge

Note: Some audio features may have limited support on Safari.

## 🐛 Troubleshooting

### Build fails with "web platform not found"
```bash
flutter config --enable-web
flutter create --platforms web .
```

### Dependencies won't resolve
```bash
flutter pub clean
flutter pub get
```

### Changes not reflecting in browser
- Clear browser cache (Cmd+Shift+Delete on macOS)
- Use incognito/private browsing mode
- Try `flutter run -d chrome --host localhost`

---

**Happy beat making! 🎵**
