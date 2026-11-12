# Mission Map (Android)

The Mission Map page wrapped as an Android app with Capacitor 8. The page is in `www/index.html`. The native parts are phone reminders (Local Notifications) and phone-calendar sync (Capacitor Calendar). They only switch on inside the app, in Options > Phone.

## Build the APK without installing anything (GitHub)
This copy has fewer than 100 files so GitHub's web upload accepts it in one go. The build step regenerates the rest.
1. Create a new private GitHub repository and upload everything in this folder (the `.github` folder must be included).
2. Open the repository's Actions tab, pick "Build Android APK", press Run workflow.
3. When it finishes, download `mission-map-debug-apk` from the run page. Unzip it and copy `app-debug.apk` to your phone.
4. Open the file on the phone and allow installing from that source when Android asks.

## Build on your own computer
Needs Node 22+, JDK 21 and Android Studio (for the Android SDK).
```
npm install
npx cap sync android
npx cap open android      # then press Run in Android Studio, or: cd android && ./gradlew assembleDebug
```

## Updating the page
Replace the page with a new version from Claude:
```
node scripts/use-page.js path/to/missions.html
npx cap sync android
```
then rebuild.

## First run on the phone
- Your old data lives in the Claude page, not in the app. In the old page: Options > Backup > Save .json, then in the app: Options > Backup > Import file.
- Options > Phone > Allow notifications, then "Allow exact timing" if it is offered.
- Options > Phone > Connect phone calendar, tick the calendars to show, and optionally choose one to save your own events into.
- On phones with aggressive battery savers (Samsung, Xiaomi, Huawei, OnePlus), set Mission Map to "Unrestricted" battery so reminders are not delayed.

## Notes
- Pictures and music you add are stored inside the app on that phone only.
- Imported phone-calendar events are read-only in the app and keep their own alerts in the calendar app. Events you create in Mission Map get Mission Map reminders, and are written to the chosen calendar without alerts.
- Exact reminder timing: the app declares USE_EXACT_ALARM, which Android grants at install. If you ever publish on Google Play, Play only allows that permission for alarm and calendar apps.
