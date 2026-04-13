<div align="center">

<img src="https://img.shields.io/badge/AdsManager-SDK-6A0DAD?style=for-the-badge&logo=android&logoColor=white" alt="AdsManager SDK"/>

# AdsManager SDK

**A powerful, lightweight Android library for seamless Google AdMob integration.**  
Built with "Smart Logic" to maximize revenue while protecting user experience.

<br/>

[![Version](https://img.shields.io/badge/Version-1.0.0-6A0DAD?style=flat-square)](https://github.com/)
[![Min SDK](https://img.shields.io/badge/Min%20SDK-API%2021%2B-3DDC84?style=flat-square&logo=android&logoColor=white)](https://developer.android.com/)
[![Language](https://img.shields.io/badge/Language-Java%20%7C%20Kotlin-F88900?style=flat-square&logo=kotlin&logoColor=white)](https://kotlinlang.org/)
[![AdMob](https://img.shields.io/badge/Google-AdMob%20Ready-4285F4?style=flat-square&logo=google&logoColor=white)](https://admob.google.com/)
[![License](https://img.shields.io/badge/License-MIT-red?style=flat-square)](LICENSE)

<br/>

</div>

---

## ✨ Features

<table>
<tr>
<td width="50%">

**🎯 Smart 8–15 Click Logic**  
Displays ads randomly between the 8th and 15th user click. Prevents ad fatigue and protects your AdMob account from policy violations.

**🔁 Every 3 Clicks Logic**  
Fixed-interval ad strategy designed for high-engagement apps where consistent monetization is the priority.

**⚡ One-Click Force Show**  
Instantly display an interstitial for critical moments — no counters, no delays.

</td>
<td width="50%">

**🎁 Rewarded Ads with Fallback**  
Guarantees reward delivery to users even when an ad fails to load, keeping trust and retention high.

**📱 App Open Ad Support**  
High-impact full-screen ads shown on app launch or resume. Initialized at the Application level for zero latency.

**🏷️ Dynamic Banner Loading**  
Inject adaptive banners into any `ViewGroup` container with a single method call.

</td>
</tr>
</table>

---

## 📦 Installation

### Step 1 — Add the AAR File

Copy `AdsManager.aar` into your module's `libs/` directory:

```
your-project/
└── app/
    └── libs/
        └── AdsManager.aar   ✅
```

---

### Step 2 — Add Dependencies

**Kotlin DSL** (`build.gradle.kts`):
```kotlin
dependencies {
    implementation(files("libs/AdsManager.aar"))
    implementation("com.google.android.gms:play-services-ads:23.0.0")
    implementation("androidx.lifecycle:lifecycle-process:2.8.0")
}
```

**Groovy DSL** (`build.gradle`):
```groovy
dependencies {
    implementation files("libs/AdsManager.aar")
    implementation "com.google.android.gms:play-services-ads:23.0.0"
    implementation "androidx.lifecycle:lifecycle-process:2.8.0"
}
```

---

### Step 3 — Register AdMob App ID

Add your AdMob App ID inside the `<application>` tag in `AndroidManifest.xml`:

```xml
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="YOUR_ADMOB_APP_ID"/>
```

> 💡 Use `ca-app-pub-3940256099942544~3347511713` during development (Google's official test App ID).

---

## 🚀 Implementation Guide

### 1. Initialize — Application Class

Initialize the SDK once in your `Application` class to enable **App Open Ads** on every launch.

<details open>
<summary><b>Kotlin</b></summary>

```kotlin
class MyApp : Application() {
    override fun onCreate() {
        super.onCreate()
        MobileAds.initialize(this)
        AdsManager.getInstance().loadAppOpenAd(this, AdsManager.TEST_APP_OPEN)
    }
}
```
</details>

<details>
<summary><b>Java</b></summary>

```java
public class MyApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        MobileAds.initialize(this);
        AdsManager.getInstance().loadAppOpenAd(this, AdsManager.TEST_APP_OPEN);
    }
}
```
</details>

Register it in `AndroidManifest.xml`:
```xml
<application
    android:name=".MyApp"
    ... />
```

---

### 2. Interstitial Ads

Three display strategies — choose based on your app's UX needs.

<details open>
<summary><b>Kotlin</b></summary>

```kotlin
val ads = AdsManager.getInstance()

// Strategy A — Smart Random (fires between 8th and 15th click)
ads.showInterstitialWithSmartCount(this, AdsManager.TEST_INTERSTITIAL)

// Strategy B — Fixed Interval (fires every 3 clicks)
ads.showInterstitialEvery3Clicks(this, AdsManager.TEST_INTERSTITIAL)

// Strategy C — Instant (fires immediately)
ads.showInterstitialOneClick(this, AdsManager.TEST_INTERSTITIAL)
```
</details>

<details>
<summary><b>Java</b></summary>

```java
AdsManager ads = AdsManager.getInstance();

// Strategy A — Smart Random
ads.showInterstitialWithSmartCount(this, AdsManager.TEST_INTERSTITIAL);

// Strategy B — Fixed Interval
ads.showInterstitialEvery3Clicks(this, AdsManager.TEST_INTERSTITIAL);

// Strategy C — Instant
ads.showInterstitialOneClick(this, AdsManager.TEST_INTERSTITIAL);
```
</details>

---

### 3. Rewarded Ads

Show a rewarded ad and grant the reward via callback. The fallback mechanism ensures rewards are always delivered.

<details open>
<summary><b>Kotlin</b></summary>

```kotlin
AdsManager.getInstance().showRewardedWithWatchCheck(
    this,
    AdsManager.TEST_REWARDED
) { amount ->
    // Grant the reward to the user
    Toast.makeText(this, "You earned $amount coins!", Toast.LENGTH_SHORT).show()
}
```
</details>

<details>
<summary><b>Java</b></summary>

```java
AdsManager.getInstance().showRewardedWithWatchCheck(this, AdsManager.TEST_REWARDED, amount -> {
    // Grant the reward to the user
    Toast.makeText(this, "You earned " + amount + " coins!", Toast.LENGTH_SHORT).show();
});
```
</details>

---

### 4. Banner Ads

**1. Add a container in your layout XML:**
```xml
<LinearLayout
    android:id="@+id/banner_container"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:gravity="center"/>
```

**2. Load the banner:**

<details open>
<summary><b>Kotlin</b></summary>

```kotlin
val bannerContainer = findViewById<LinearLayout>(R.id.banner_container)
AdsManager.getInstance().loadBanner(this, bannerContainer, AdsManager.TEST_BANNER)
```
</details>

<details>
<summary><b>Java</b></summary>

```java
LinearLayout bannerContainer = findViewById(R.id.banner_container);
AdsManager.getInstance().loadBanner(this, bannerContainer, AdsManager.TEST_BANNER);
```
</details>

---

## 🧪 Test Ad Unit IDs

Use these constants during development. **Never ship with test IDs.**

| Ad Format | Constant | Type |
|---|---|---|
| App Open | `AdsManager.TEST_APP_OPEN` | Full-screen on launch |
| Interstitial | `AdsManager.TEST_INTERSTITIAL` | Full-screen on action |
| Rewarded | `AdsManager.TEST_REWARDED` | Opt-in with reward |
| Banner | `AdsManager.TEST_BANNER` | Inline display |

---

## ⚠️ Before Publishing

> [!WARNING]
> Replace all **Test Ad Unit IDs** with your real IDs from the [AdMob Dashboard](https://admob.google.com/) before releasing to the Play Store. Serving live ads with test IDs violates Google AdMob policy.

**Pre-release checklist:**
- [ ] Replace `TEST_APP_OPEN` with your real App Open ad unit ID
- [ ] Replace `TEST_INTERSTITIAL` with your real Interstitial ad unit ID
- [ ] Replace `TEST_REWARDED` with your real Rewarded ad unit ID
- [ ] Replace `TEST_BANNER` with your real Banner ad unit ID
- [ ] Update `APPLICATION_ID` in `AndroidManifest.xml` with your real AdMob App ID

---

## 🛠 Tech Specs

| Property | Value |
|---|---|
| Library Format | `.aar` (Android Archive) |
| Min SDK | API 21 (Android 5.0 Lollipop) |
| Target SDK | API 34+ |
| AdMob SDK | `play-services-ads:23.0.0` |
| Lifecycle | `lifecycle-process:2.8.0` |
| Languages | Java & Kotlin |

---

<div align="center">

**Developer:** Dinidu &nbsp;|&nbsp; **Studio:** Boom Studio &nbsp;|&nbsp; **Version:** 1.0.0

*Made with ❤️ by Boom Studio*

</div>
