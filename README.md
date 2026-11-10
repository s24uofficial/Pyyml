# PyML Runner

Offline Python machine learning on Android (Kotlin + Chaquopy 17.2.0, Python 3.10, numpy / scipy / scikit-learn / matplotlib).

## Build steps

1. Install **Python 3.10** on your PC (python.org). Chaquopy needs the same Python version on the build machine.
   If Gradle can't find it, uncomment a `buildPython(...)` line in `app/build.gradle` and fix the path.
2. Install Android Studio (latest) and let it download **Android SDK Platform 35**.
3. `File > Open` and choose this `PyMLRunner` folder. Wait for Gradle sync (needs internet the first time:
   it downloads the Android wheels for numpy, scipy, scikit-learn, matplotlib).
4. `Build > Build Bundle(s) / APK(s) > Build APK(s)` and install `app/build/outputs/apk/debug/app-debug.apk`.
   Or just press Run with your phone connected (USB debugging on).

## Folder structure

```
PyMLRunner/
├── settings.gradle
├── build.gradle
├── gradle.properties
├── gradle/wrapper/gradle-wrapper.properties
└── app/
    ├── build.gradle                      <- Chaquopy + pip packages
    └── src/main/
        ├── AndroidManifest.xml
        ├── python/ml_runner.py           <- all Python / ML code
        ├── java/com/pymlrunner/app/MainActivity.kt
        └── res/
            ├── layout/activity_main.xml, item_input.xml, layout_output.xml
            ├── values/strings.xml, themes.xml
            └── drawable/ic_launcher.xml
```

## Notes

- Only the `arm64-v8a` ABI is built (all modern phones). To test on a PC emulator add `"x86_64"` to `abiFilters`.
- The scikit-learn / scipy Android wheels in Chaquopy's repository are older builds (sklearn 1.3.2, scipy 1.8.1) and are
  only published for Python 3.10 and below. They may not load on devices that run in 16 KB page-size mode.
- Command-line builds need the Gradle wrapper jar: run `gradle wrapper --gradle-version 8.9` once in this folder
  (Android Studio does not need it).
