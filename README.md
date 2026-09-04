# ResuMate — Intelligent Resume Builder

ResuMate is a lightweight, copyright-safe resume builder packaged as an Android app with Capacitor. The current rebuild focuses on a polished mobile-first experience, local persistence, original templates, live preview, ATS analysis, writing assistance, backup and export.

## Features

- Dashboard with multiple saved resumes
- Create, edit, duplicate, rename and delete resumes
- Eight original templates: Atlas, Clarity, Vertex, Minimal, Nova, Career, Summit and Orbit
- Central resume data model with autosave
- Personal information, summary, experience, education, skills, projects, certifications, languages and achievements
- Add/delete/reorder repeated entries
- Section reordering that affects preview and print output
- Live A4 preview with zoom controls
- Design Studio: templates, accent themes, fonts, font size, spacing and margins
- Local ATS analyzer with structure checks and job-description keyword matching
- ResuMate AI Assistant with offline writing suggestions; it does not falsely claim a cloud AI provider is running
- Cover Letter workspace with save, copy and writing assistance
- JSON backup and validated import
- Print / Save as PDF using the platform print flow
- Device sharing through the Web Share API when supported
- Offline-first core editing, preview, ATS and backup

## Architecture

```text
www/index.html   UI + responsive design system
www/app.js       application state, data model, renderer and feature logic
capacitor.config.json
android/         native Capacitor Android project
.github/workflows/build-apk.yml
```

The web application has no runtime CDN dependency. Core functionality is implemented locally so editing, preview and ATS analysis do not require internet access.

## Android configuration

- App ID: `com.krapal.resumate`
- App name: `ResuMate`
- Web directory: `www`
- minSdk: 24
- compileSdk: 36
- targetSdk: 36
- Android Gradle Plugin: 8.13.0
- Gradle wrapper: 8.14.3
- CI Java: 21
- Node: 22

## Development

```bash
npm install
npm run build
npx cap sync android
```

Debug build:

```bash
cd android
./gradlew clean assembleDebug
```

Unit tests:

```bash
cd android
./gradlew test
```

## APK location

After a successful debug build:

```text
android/app/build/outputs/apk/debug/app-debug.apk
```

GitHub Actions publishes the same file as the `resumate-debug-apk` artifact.

## GitHub Actions

`.github/workflows/build-apk.yml` runs on pushes to `main` and `resumate-complete-rebuild`, or manually from Actions. It installs Android SDK 36, runs unit tests, performs a clean debug build and uploads the APK artifact.

## Export / PDF note

The app uses the browser/WebView print flow for PDF creation rather than a remote PDF service. On Android, choose **Save as PDF** from the system print UI when available. This keeps the core export path independent of a CDN or cloud API.

## Privacy and AI

Resume data is stored locally by default. The bundled ResuMate AI Assistant is explicitly an offline writing-aid layer. No provider API key is embedded in the frontend or APK. A future cloud AI integration should use a secure backend rather than exposing secrets in JavaScript.

## Copyright safety

ResuMate uses original UI, copy and template structures. It does not include proprietary source code, branding, logos or pixel-for-pixel copies of another resume-builder product.
