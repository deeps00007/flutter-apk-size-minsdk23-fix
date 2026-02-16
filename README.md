# 🔥 Flutter APK Size Increased After Setting minSdkVersion to 23?

## 📌 Problem

When increasing:

minSdkVersion 23


APK size may increase significantly.

Example:

30MB → 60MB

---

## 🤔 Why Does This Happen?

Starting from **Android 6.0 (API Level 23)**:

- Native libraries (`.so` files) are stored **uncompressed** inside APK.
- This improves app startup time.
- But increases APK size dramatically.

---

## 📂 What Are .so Files?

`.so` files are native compiled libraries used by:

- Flutter engine
- Plugins
- Platform channels
- JNI (Java Native Interface)

They exist for different architectures:

- armeabi-v7a
- arm64-v8a
- x86
- x86_64

---

# 📊 Real Benchmark Example

| Configuration | APK Size |
|--------------|----------|
| minSdk 21 | 30MB |
| minSdk 23 | 60MB |

---

# ✅ Solution 1 — Use Legacy Packaging

Add this inside:

android/app/build.gradle

android {
packagingOptions {
doNotStrip "/armeabi-v7a/.so"
doNotStrip "/arm64-v8a/.so"
doNotStrip "/x86/.so"
doNotStrip "/x86_64/.so"

    jniLibs {
        useLegacyPackaging = true
    }
}


}


## ✅ What This Does

- Compresses native libraries again
- Reduces APK size
- Slight startup delay (usually negligible)

---

# 🚀 Better Modern Solution (Recommended)

Instead of legacy packaging:

## Build App Bundle



flutter build appbundle


OR enable ABI split:



android {
bundle {
abi {
enableSplit = true
}
}
}


### Why This Is Better?

- Google Play delivers only required architecture
- Smaller download size
- No startup delay
- Official modern approach

---

# 📸 Before & After

Add screenshots in:

before-after/







---

# 🎯 Conclusion

If distributing APK manually → Use legacy packaging  
If publishing on Play Store → Use app bundle

---

# 🧠 Author

Deepanshu Singh  
Flutter Developer