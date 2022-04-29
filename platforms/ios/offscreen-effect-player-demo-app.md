# Offscreen Effect Player Demo App

### Requirements

* Latest stable Xcode

### Get the client token

To start working with the Banuba SDK Demo project for iOS, you need to have the client token. To receive the **trial** client token please fill in our [form on banuba.com](https://www.banuba.com/face-filters-sdk) website, or contact us via [info@banuba.com](mailto:info@banuba.com).

### Get the Banuba SDK archive

With the client token, you will also receive the Banuba SDK archive for iOS which contains:

* Banuba Effect Player XCFramework (`BanubaEffectPlayer.xcframework`),
* BanubaSdk Xcode project,
* Effect examples located under `effects` folder.

### Build the Banuba SDK OEP Demo app

This section is fully consistent with the same section in iOS demo app (Build the Banuba SDK Demo app section). Please, refer to iOS demo app for more details.

### Run the Banuba SDK OEP Demo app

:::note Before running the iOS Offscreen Effect Player Demo project, place your client token inside appropriate file in the following location:\
`src/BanubaSdk/BanubaSdkApp/OffscreenTestApp/ViewController.swift` :::

#### Client token usage example

```swift
let bundleRoot = Bundle.init(for: BNBEffectPlayer.self).bundlePath
let dirs = [bundleRoot + "/bnb-resources", Bundle.main.bundlePath + "/effects"]
BNBUtilityManager.initialize(
    dirs,
    clientToken: "YOUR_TOKEN_HERE"
)
```

#### Effect usage example

```swift
loadingEffect = true
effectPlayer?.loadEffect("YOUR_EFFECT_NAME", completion: {
    self.loadingEffect = false
})
```

To run the SDK OEP Demo app, click `Set the active scheme` button in Xcode and choose `OffscreenTestApp`.
