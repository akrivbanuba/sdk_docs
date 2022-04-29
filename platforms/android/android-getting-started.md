# Android Getting Started

### Requirements

* Latest stable Android Studio
* Latest Gradle plugin
* Latest NDK

### Get the client token and configuration file

To start working with the Banuba SDK in your project, you need to have the client token. To receive the client token please fill in our [form on banuba.com](https://www.banuba.com/face-filters-sdk) website, or contact us via [info@banuba.com](mailto:info@banuba.com).

Together with the token, you will receive a configuration file `config.json` which contains the required SDK resources defined by your token. Read more about this in [Repack your SDK archive (minify SDK size)](broken-reference) section.

:::note Before building your project, place your client token inside the file: `BanubaClientToken.java` :::

#### Client token usage example

```java
final class BanubaClientToken {
    public static final String KEY = "YOUR_TOKEN_HERE";

    private BanubaClientToken() {
    }
}
```

### Get the Banuba SDK archive

:::info Since 1.4.0 Banuba SDK provides platform-specific packages. Packages should be preferred over archives. :::

With the client token, you will also receive the Banuba SDK archive for Android which contains:

* Banuba Effect Player (compiled Android library project with .aar extension),
* Banuba SDK (compiled Android library project with .aar extension),
* Effect examples located under `effects` folder.

### Repack your SDK archive (minify SDK size)

The SDK release archive contains all SDK resources by default. They may consume more disk space in the finished build.

To reduce the SDK size please use `sdk_repacking.py` script provided with the SDK archive.

Please refer to SDK repacking **readme** in your SDK archive for more info and usage example.

### Build your project with Banuba SDK

1. Create the `libs` directory in your project and add `banuba_effect_player.aar` with `banuba_sdk.aar`.
2. Open build.gradle (Module: app) and add Banuba SDK dependencies for your project
3. Add `BanubaClientToken.java` to your project.
4. In `Project Structure` check `Declared Dependencies`
5. Also check our [Android Demo app](https://github.com/Banuba/quickstart-android) to use some code snippets
6. Now you can run your project with BanubaSdk on your device

### Minify the app size

After integration of Banuba SDK libraries `banuba_effect_player.aar`, `banuba_sdk.aar` your app size may increase significantly. It may happen if you use an 'android.tools' version earlier than `classpath com.android.tools.build:gradle:3.5.0`. To minify your app size, update 'android.tools' to a newer version, e.g. classpath `com.android.tools.build:gradle:4.0.1`. Then, rebuild your application and check that "**strip**" phase exists in the build log (`> Task :app:strip...`).

### Switching the face search mode

The EffectPlayer xcframework allows you to use different face tracking algorithms for low, medium and high-end device classes.

Face tracking algorithms:

* `FAST` — provides higher performance yet lower quality of face tracking.
* `GOOD` — provides better tracking quality with larger resources usage.
* `MEDIUM` — special type which uses algorithm with optimal balance of quality and performance.

See more in [API reference](pathname:///generated/javadoc/com/banuba/sdk/recognizer/FaceSearchMode.html).

The default settings as seen below are `GOOD` for high-end and medium devices and `MEDIUM` for others.

```java
FaceSearchMode faceSearchMode = FaceSearchMode.MEDIUM;
if (hardwareClass == HardwareClass.HIGH || hardwareClass == HardwareClass.MEDIUM) {
    faceSearchMode = FaceSearchMode.GOOD;
}
```

You can change the code to force usage of any face tracking mode for the desired group of devices.
