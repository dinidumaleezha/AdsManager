# 🚀 AdsManager SDK

A powerful, lightweight Android Library (AAR) designed for seamless Google AdMob integration. **AdsManager** features "Smart Logic" to balance revenue and user experience by preventing ad fatigue.

![Version](https://img.shields.io/badge/version-1.0.0-purple)
![Min SDK](https://img.shields.io/badge/minSdk-21%2B-green)
![Language](https://img.shields.io/badge/language-Java%20%7C%20Kotlin-blue)
![AdMob](https://img.shields.io/badge/AdMob-Ready-orange)

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 🎯 **Smart 8–15 Click Logic** | Displays an ad randomly between the 8th and 15th click to protect AdMob accounts. |
| 🔁 **Every 3 Clicks Logic** | A fixed interval strategy for high-engagement apps. |
| ⚡ **One-Click Force Show** | Instant ad display for critical actions. |
| 🎁 **Rewarded Ads with Fallback** | Ensures the user gets a reward even if the ad fails to load. |
| 📱 **App Open Ad Support** | High-impact ads displayed immediately upon app launch/resume. |
| 🏷️ **Dynamic Banner Loading** | Easily inject banners into any layout container. |

---

## 📦 Installation

### Step 1: Add the AAR File
Copy `AdsManager.aar` into your project's `app/libs/` directory.

### Step 2: Add Dependencies
Add these to your app-level `build.gradle` or `build.gradle.kts`:

**Kotlin DSL (`build.gradle.kts`):**
```kotlin
dependencies {
    implementation(files("libs/AdsManager.aar"))
    implementation("com.google.android.gms:play-services-ads:23.0.0")
    implementation("androidx.lifecycle:lifecycle-process:2.8.0")
}
```

**Groovy DSL (`build.gradle`):**
```groovy
dependencies {
    implementation files("libs/AdsManager.aar")
    implementation "com.google.android.gms:play-services-ads:23.0.0"
    implementation "androidx.lifecycle:lifecycle-process:2.8.0"
}
```

### Step 3: Set AdMob App ID
Add your ID inside the `<application>` tag in `AndroidManifest.xml`:

```xml
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="ca-app-pub-3940256099942544~3347511713"/>
```

---

## 🚀 Implementation Guide

### 1. Initialize in Application Class
To support **App Open Ads**, initialize the SDK in your custom `Application` class.

**Kotlin:**
```kotlin
class MyApp : Application() {
    override fun onCreate() {
        super.onCreate()
        MobileAds.initialize(this)
        // Preload App Open Ad
        AdsManager.getInstance().loadAppOpenAd(this, AdsManager.TEST_APP_OPEN)
    }
}
```

**Java:**
```java
public class MyApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        MobileAds.initialize(this);
        // Preload App Open Ad
        AdsManager.getInstance().loadAppOpenAd(this, AdsManager.TEST_APP_OPEN);
    }
}
```

---

### 2. Interstitial Ads

**Kotlin:**
```kotlin
val ads = AdsManager.getInstance()

// Logic A: Smart Random (8–15 Clicks)
ads.showInterstitialWithSmartCount(this, AdsManager.TEST_INTERSTITIAL)

// Logic B: Fixed Interval (Every 3 Clicks)
ads.showInterstitialEvery3Clicks(this, AdsManager.TEST_INTERSTITIAL)

// Logic C: Instant Show
ads.showInterstitialOneClick(this, AdsManager.TEST_INTERSTITIAL)
```

**Java:**
```java
AdsManager ads = AdsManager.getInstance();

// Logic A: Smart Random
ads.showInterstitialWithSmartCount(this, AdsManager.TEST_INTERSTITIAL);

// Logic B: Every 3 Clicks
ads.showInterstitialEvery3Clicks(this, AdsManager.TEST_INTERSTITIAL);

// Logic C: Instant Show
ads.showInterstitialOneClick(this, AdsManager.TEST_INTERSTITIAL);
```

---

### 3. Rewarded Ads (Watch & Earn)

**Kotlin:**
```kotlin
ads.showRewardedWithWatchCheck(this, AdsManager.TEST_REWARDED) { amount ->
    Toast.makeText(this, "Reward Earned!", Toast.LENGTH_SHORT).show()
}
```

**Java:**
```java
ads.showRewardedWithWatchCheck(this, AdsManager.TEST_REWARDED, amount -> {
    Toast.makeText(this, "Reward Earned!", Toast.LENGTH_SHORT).show();
});
```

---

### 4. Banner Ads

**XML Layout:**
```xml
<LinearLayout
    android:id="@+id/banner_container"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"/>
```

**Kotlin:**
```kotlin
val bannerBox = findViewById<LinearLayout>(R.id.banner_container)
AdsManager.getInstance().loadBanner(this, bannerBox, AdsManager.TEST_BANNER)
```

**Java:**
```java
LinearLayout bannerBox = findViewById(R.id.banner_container);
AdsManager.getInstance().loadBanner(this, bannerBox, AdsManager.TEST_BANNER);
```

---

## 🧪 Test Ad Unit IDs

| Ad Type | Constant |
|---|---|
| App Open | `AdsManager.TEST_APP_OPEN` |
| Interstitial | `AdsManager.TEST_INTERSTITIAL` |
| Rewarded | `AdsManager.TEST_REWARDED` |
| Banner | `AdsManager.TEST_BANNER` |

---

## 🛠 Developer Info

- **Developer:** Dinidu (Boom Studio)
- **Version:** 1.0.0 (Release)
- **Min SDK:** API 21+

---

## ⚠️ Important
For development, use the **Test IDs** provided in the `AdsManager` class. Switch to **Real Unit IDs** from your AdMob Dashboard before publishing to the Play Store.
"""

*Made with ❤️ by Boom Studio*
