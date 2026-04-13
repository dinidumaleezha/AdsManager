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
| 🎯 **Smart 8–15 Click Logic** | Displays an ad randomly between the 8th and 15th click to avoid predictable patterns and protect AdMob accounts. |
| 🔁 **Every 3 Clicks Logic** | A fixed interval strategy for high-engagement apps. |
| ⚡ **One-Click Force Show** | Instant ad display for critical actions (e.g., Download button). |
| 🎁 **Rewarded Ads with Fallback** | Ensures the user gets a reward even if the ad fails to load. |
| 📱 **App Open Ad Support** | High-impact ads displayed immediately upon app launch. |
| 🏷️ **Dynamic Banner Loading** | Easily inject banners into any layout container. |

---

## 📦 Installation

### Step 1: Add the AAR File

Copy `AdsManager.aar` into your project's `app/libs/` directory.

```
app/
└── libs/
    └── AdsManager.aar  ✅
```

### Step 2: Add dependency

#### Configure Kotlin DSL `build.gradle.kts` (App level)

```kotlin
dependencies {
    implementation(files("libs/AdsManager.aar"))
    implementation("com.google.android.gms:play-services-ads:23.0.0")
    implementation("androidx.lifecycle:lifecycle-process:2.8.0")
}
```
#### Configure Groovy DSL `build.gradle` (App level)
```Java
dependencies {
    implementation files("libs/AdsManager.aar")
    implementation"com.google.android.gms:play-services-ads:23.0.0"
    implementation"androidx.lifecycle:lifecycle-process:2.8.0"
}
```

### Step 3: Set AdMob App ID

Add your AdMob App ID inside the `<application>` tag in `AndroidManifest.xml`:

```xml
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="ca-app-pub-XXXXXXXXXXXXXXXX~XXXXXXXXXX"/>
```

> ⚠️ Replace the value with your **real AdMob App ID** before publishing to the Play Store.

---

## 🚀 Implementation Guide

### 1. Initialize in Application Class

To ensure ads are pre-loaded, initialize the SDK in your `Application` class.

#### `Kotlin DSL`
```kotlin
class MyApp : Application() {
    override fun onCreate() {
        super.onCreate()

        // Initialize AdMob
        MobileAds.initialize(this)

        // Preload App Open Ad
        AdsManager.getInstance().loadAppOpenAd(this, AdsManager.TEST_APP_OPEN)
    }
}
```

#### `Groovy DSL`
```Java
class MyApp : Application() {
    override fun onCreate() {
        super.onCreate()

        // Initialize AdMob
        MobileAds.initialize(this)

        // Preload App Open Ad
        AdsManager.getInstance().loadAppOpenAd(this, AdsManager.TEST_APP_OPEN)
    }
}
```

Don't forget to register it in `AndroidManifest.xml`:

```xml
<application
    android:name=".MyApp"
    ... >
```

---

### 2. Interstitial Ads — 3 Logic Options

```kotlin
val ads = AdsManager.getInstance()

// Logic A: Smart Random (8–15 Clicks) — Recommended
btnNext.setOnClickListener {
    ads.showInterstitialWithSmartCount(this, AdsManager.TEST_INTERSTITIAL)
}

// Logic B: Fixed Interval (Every 3 Clicks)
btnView.setOnClickListener {
    ads.showInterstitialEvery3Clicks(this, AdsManager.TEST_INTERSTITIAL)
}

// Logic C: Instant Show (One Click)
btnDownload.setOnClickListener {
    ads.showInterstitialOneClick(this, AdsManager.TEST_INTERSTITIAL)
}
```

---

### 3. Rewarded Ad

```kotlin
btnUnlock.setOnClickListener {
    ads.showRewardedWithWatchCheck(this, AdsManager.TEST_REWARDED) { amount ->
        // Called on successful reward
        Toast.makeText(this, "Reward Granted!", Toast.LENGTH_SHORT).show()
    }
}
```

> 💡 The fallback ensures the reward callback fires even if the ad fails to load — no frustrated users!

---

### 4. Banner Ad

Add a `LinearLayout` container to your XML layout:

```xml
<LinearLayout
    android:id="@+id/ad_container"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"/>
```

Then load the banner dynamically in your Activity:

```kotlin
val bannerBox = findViewById<LinearLayout>(R.id.ad_container)
ads.loadBanner(this, bannerBox, AdsManager.TEST_BANNER)
```

---

## 🧪 Test Ad Unit IDs

The following test IDs are built into the `AdsManager` class for development:

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
- **Language:** Java (Fully compatible with Kotlin)
- **Min SDK:** API 21+

---

## ⚠️ Important

> Before publishing to the **Google Play Store**, replace all Test IDs with your **Real Ad Unit IDs** from the [AdMob Dashboard](https://admob.google.com/).

Using test IDs in production will result in **no revenue** and may violate AdMob policies.

---

*Made with ❤️ by Boom Studio*
