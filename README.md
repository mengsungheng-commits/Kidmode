# Kids Mode – School Tablet Parental Control

A lightweight **Kids Mode / Teacher Mode** app for Android phones and tablets (tested on HONOR).  
Built for schools to limit student apps, control screen time, and give teachers a separate app list.

**Developed by IT Team · Footprints International School**

---

## Features

### Kids Mode
- Full-screen child-friendly home
- Only **allowed student apps** are shown
- Large icons, simple layout
- Exit protected by PIN
- Optional daily screen-time limit
- Auto-return when student opens system **Settings** (needs Usage Access)

### Teacher Mode
- Separate home screen with **teacher-only apps**
- Open from Kids Mode with **Teacher Mode PIN**
- Return to Kids Mode **without** a PIN
- Same Settings auto-return protection as Kids Mode

### Teacher Control (admin panel)
- Screen time limits
- Manage apps (Kids list + Teacher list)
- Bedtime schedule (reminder)
- Usage information
- Child profile & access codes
- Change admin PIN
- In-app update check (GitHub `version.json`)

---

## Requirements

| Item | Detail |
|------|--------|
| Platform | Android phone / tablet |
| Language | Kotlin |
| UI | Jetpack Compose + Material 3 |
| Min SDK | As set in `app/build.gradle.kts` |

**Important permissions**
- **Usage Access** – required for Settings auto-return and usage stats  
- **Default Home app** (optional) – lock tablet into Kids Mode as home  

On HONOR: if App info shows *“The app has been restricted”*, tap **Remove restriction** before enabling Usage Access.

---

## How to use (teachers)

### Start Kids Mode
1. Open **Kids Mode** → Teacher Control  
2. Tap **Start Kids Mode**  
3. (Optional) Set as default Home when asked  

Students only see apps enabled under **Manage Apps → Kids Mode apps**.

### Open Teacher Mode
1. On Kids Mode, tap **Teacher** (top-left)  
2. Enter the **Teacher Mode PIN**  
3. Use teacher apps  

### Back to Kids Mode
1. On Teacher Mode, tap **Kids Mode** (top-left)  
2. No PIN required  

### Manage apps
1. Teacher Control → **Manage Apps**  
2. Tab **Kids Mode apps** or **Teacher Mode apps**  
3. Toggle apps On/Off  
4. Optional: **Apply school app list**

### Change Teacher Mode PIN
1. Teacher Control → **Settings**  
2. **Teacher Mode PIN (from Kids Mode)**  
3. Enter a new 4-digit PIN  

### Exit codes
Configured in **Settings** / **Change PIN** by school IT.  
Do not share Exit or admin codes with students.

---

## Setup checklist (each tablet)

```text
1. Install APK
2. Open Teacher Control → Settings
3. App Info / Permissions → Remove restriction (if shown)
4. Open Usage Access Settings → Allow usage access = ON
5. Manage Apps → set Kids + Teacher lists
6. Start Kids Mode
