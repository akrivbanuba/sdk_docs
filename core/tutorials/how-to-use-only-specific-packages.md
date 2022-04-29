# How to use only specific packages

Since v1.4.0, Banuba SDK provides platform-specific packages. Only iOS and Android platforms are supported for now.

The SDK is packaged as CocoaPods' pods for iOS and .aar packages published to GitHub Packages for Android.

For simplicity, SDK provides a metamodule which depends on all available modules. It can be used for "quick start" and guarantee that any effect will work correctly. All Face AR SDK examples on Github use it.

Also it is possible to specify only the required modules as project dependencies but in such case it is your responsibility to specify everything required for desired effect. Please keep in mind that there are several "must have" modules:

| module name    | iOS package     | Android package               |
| -------------- | --------------- | ----------------------------- |
| sdk\_core      | BNBSdkCore      | com.banuba.sdk.sdk\_core      |
| effect\_player | BNBEffectPlayer | com.banuba.sdk.effect\_player |
| scripting      | BNBScripting    | com.banuba.sdk.scripting      |

These modules must be added every time, anything else is feature-specific and depends on your needs.

Sometimes you also may need the `sdk_api` module, for example when you want to use `BanubaSdkManager` class. This module is lightweight, so you can add it every time.

| module name | iOS package | Android package         |
| ----------- | ----------- | ----------------------- |
| sdk\_api    | BNBSdkApi   | com.banuba.sdk.sdk\_api |

Use only the modules with the same version, modules with different versions (even minor) may conflict or just work incorrectly with each other.

There are a few small examples below, demonstrating the usage in background segmentation feature only.

### iOS example

```
source 'https://github.com/sdk-banuba/banuba-sdk-podspecs.git'

target '<target name>' do
  # ...
  # must have packages
  pod 'BNBSdkCore', '=1.4.0'
  pod 'BNBEffectPlayer', '=1.4.0'
  pod 'BNBScripting', '=1.4.0'
  # optional packages
  pod 'BNBSdkApi', '=1.4.0'
  # feature-specific packages
  pod 'BNBBackground', '=1.4.0'
  # ...
end
```

See platform-specific article to find more details about packages usage.

### Android example

```
allprojects {
    repositories {
        google()
        mavenCentral()

        maven {
            name "GitHubPackages"
            url "https://maven.pkg.github.com/sdk-banuba/banuba-sdk-android"
            credentials {
                username = "sdk-banuba"
                password = "\u0067\u0068\u0070\u005f\u0033\u0057\u006a\u0059\u004a\u0067\u0071\u0054\u0058\u0058\u0068\u0074\u0051\u0033\u0075\u0038\u0051\u0046\u0036\u005a\u0067\u004f\u0041\u0053\u0064\u0046\u0032\u0045\u0046\u006a\u0030\u0036\u006d\u006e\u004a\u004a"
            }
        }
    }
}
```

```
dependencies {
    // ...
    // must have packages
    implementation "com.banuba.sdk:sdk_core:1.4.0"
    implementation "com.banuba.sdk:effect_player:1.4.0"
    implementation "com.banuba.sdk:scripting:1.4.0"
    // optional packages
    implementation "com.banuba.sdk:sdk_api:1.4.0"
    // feature-specific packages
    implementation "com.banuba.sdk:background:1.4.0"
    // ...
}
```

See platform-specific article to find more details about packages usage.
