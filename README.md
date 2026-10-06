# 🌈 Kids Mode – School Tablet Launcher

A child-friendly **Kids Mode** launcher for school Android tablets, with a **Teacher Mode** and a PIN-protected **Teacher Control** dashboard. Students see only the apps the school approves, in a simple, colourful grid. Teachers manage apps, screen time, bedtime and PINs from one place.

Built for **Footprints International School** by the IT Team, with **Kotlin + Jetpack Compose + Material 3**.

---

## ✨ Features

### 👧 Kids Mode
- Full-screen launcher that shows **only the approved apps** in a smooth two-column grid
- School logo and a personal greeting (**Hello, Students!**)
- Back button is blocked, and **Settings and system-manager screens are automatically closed** if a student opens them
- **Clear Background Apps** button under the logo: stops other apps' background processes to free RAM and, with the optional helper switched on, also clears the Recents list
- Daily **screen-time limit** and **bedtime** lock screen

### 👩‍🏫 Teacher Mode
- A separate approved-app list for teachers (for example admin and teaching tools)
- Switch between Kids Mode and Teacher Mode with a PIN

### 🛠️ Teacher Control (dashboard)
- **Manage Apps:** choose which apps appear in Kids Mode and in Teacher Mode (search, allow all or none, one-tap school default list)
- **Screen time:** daily limit and usage overview
- **Bedtime:** set bedtime and wake-up times
- **Permission pop-ups never block students:** when an app asks for the camera, microphone, location and so on, the pop-up opens normally. **Blocked screens** lists any other screen that sent a student home and lets you allow it with one tap
- **PIN Management:** three separate, changeable PINs
  - Teacher Mode PIN (Kids Mode → Teacher Mode)
  - Exit to Home Screen PIN
  - Exit to Teacher Control PIN
- Child name, emergency unlock code, permission shortcuts and in-app **update checker**

### 🔐 Security
- PINs are stored as **salted SHA-256 hashes** in `EncryptedSharedPreferences`
- When a PIN is changed, the **old PIN stops working immediately**
- The three PINs must all be different from each other

### ⚡ Performance
- One background monitor service (not one per screen), with low CPU use and a slower check when the screen is off
- Settings are cached in memory, so no repeated decryption
- Shared, size-limited **icon cache** with GPU bitmaps, preloaded before the grid appears, which keeps scrolling smooth
- Releases memory when Android asks for it

### 🔄 Auto-update
The app checks `version.json` in this repository and can download and install the newer APK.

```json
{
  "versionCode": 20,
  "versionName": "1.0.20",
  "apkUrl": "https://github.com/<user>/<repo>/raw/main/Kidsmode.apk",
  "notes": "What's new in this version"
}
```

---

## 📋 Requirements

- Android **8.0 (API 26)** or newer, targeting Android 15 (API 35)
- Tested on HONOR tablets; other Android devices should work, but Recents handling differs between brands

## 🔑 Permissions

| Permission | Why |
|---|---|
| Usage access | real screen-time numbers and detecting Settings opening (granted manually) |
| Query all packages | list the launchable apps |
| Foreground service | keep Kids Mode monitoring alive |
| Kill background processes | the *Clear Background Apps* button |
| Boot completed | restore Kids Mode after a restart |
| Notifications | the "Kids Mode active" notification |
| Internet / install packages | update checker and installing updates |
| Accessibility (**optional**) | *Kids Mode Cleaner*: presses "clear all" in Recents when the button is tapped. It does not read, store or send anything on screen |

## 🚀 Setup

1. Install `Kidsmode.apk` (allow *Install unknown apps* for your browser or file manager).
2. Open the app and sign in to **Teacher Control** with the Exit to Teacher Control PIN.
3. **Change all three PINs** under *Settings → PIN Management*.
4. Grant **Usage access** when asked.
5. Pick the allowed apps in **Manage Apps**.
6. (Optional) Turn on **Kids Mode Cleaner** in *Android Settings → Accessibility* so Clear Background Apps also empties Recents. On Android 13+ you may first need *App info → ⋮ → Allow restricted settings*.
7. Set the app as the default Home app, then tap **Start Kids Mode**.

## 🏗️ Build

```bash
git clone https://github.com/<user>/<repo>.git
cd <repo>
./gradlew assembleRelease     # Windows: gradlew.bat assembleRelease
```

Requires **JDK 17** and the **Android SDK 35** (Android Studio includes both). The output file is named `Kidsmode.apk`. Judge speed on a **release** build; debug builds are much slower.

## 🧱 Project structure

```
app/src/main/java/com/kidsmode/parental/
├── KidsModeApp.kt              application + memory trimming
├── MainActivity.kt             Teacher Control entry (PIN)
├── data/PreferencesRepository  encrypted, cached settings + PINs
├── service/
│   ├── KidsMonitorService      foreground service + restriction monitor
│   ├── RecentsCleanerService   optional accessibility helper
│   └── BootReceiver            restore Kids Mode after restart
├── ui/
│   ├── kids/                   Kids Mode, Teacher Mode, shared app grid
│   ├── parent/                 PIN screens, dashboard, settings
│   ├── lock/                   screen-time / bedtime lock screen
│   └── theme/
└── util/                       usage stats, icon cache, cleaner, updater
```

## ⚠️ Limitations

This is a normal installable APK, not a Device Owner / MDM app. It uses only public Android APIs, so it **cannot fully lock down the device**: a determined student may still find ways around it (for example the Recents screen or a restart). For strict enforcement, enroll the tablets as Device Owner or use an MDM solution.

## 🔒 Note for maintainers

If this repository is **public**, never publish real PINs or the emergency code in the README or source. Change the built-in defaults before distributing the APK to students.

---

Developed by the **IT Team**, Footprints International School.
