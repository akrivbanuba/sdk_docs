# iOS Getting Started

### Requirements

* Latest stable Xcode

### Get the client token and configuration file

To start working with Banuba SDK in your project, you need to have the client token. To receive the client token please fill in our [form on banuba.com](https://www.banuba.com/face-filters-sdk) website, or contact us via [info@banuba.com](mailto:info@banuba.com).

Together with the token, you will receive a configuration file `config.json` which contains the required SDK resources defined by the token. Read more about this in [Repack your SDK archive (minify SDK size)](broken-reference) section.

### Get the Banuba SDK archive

:::info Since 1.4.0 Banuba SDK provides platform-specific packages. Packages should be preferred over archives. :::

With the client token, you will also receive the Banuba SDK archive for iOS which contains:

* Banuba Effect Player XCFramework (`BanubaEffectPlayer.xcframework`),
* BanubaSdk Xcode project,
* Effect examples located under `effects` folder.

### Repack your SDK archive (minify SDK size)

SDK release archive contains all SDK resources by default. They may consume more disk space in the finished build.

To reduce the SDK size, please use the `sdk_repacking.py` script provided with the SDK archive.

Please refer to SDK repacking **readme** in your SDK archive or to our [video guide](https://youtu.be/BOrsi2ud-A8) for more information and usage example.

### Build your project with the Banuba SDK

1. By default, Xcode provides `arm64, armv7` architectures as default. Since Banuba SDK supports only `arm64, x86_64` you should change you valid architectures and add `arm64` as excluded for `Any iOS Simulator SDK` in order to run Banuba SDK on simulators.
2. In your project, create `New Group` with name `Frameworks`. Then, open this folder in Finder and copy the following files from your SDK archive:

* `BNBEffectPlayer/bin/BanubaEffectPlayer.xcframework`.
* `BNBEffectPlayer/src/BanubaSdk/BanubaSdk/BanubaSdk/`.
* `BNBEffectPlayer/src/BanubaSdk/BanubaSdk/BanubaSdk.xcodeproj`.

1. Drag `BanubaEffectPlayer.xcframework` and `BanubaSdk.xcodeproj` from `Frameworks` folder in Finder to your Xcode project.
2. In `General` of your project add `BanubaSdk.framework` and `BanubaEffectPlayer.xcframework` to `Frameworks, Libraries, and Embedded Content`. Here this frameworks should be marked as `Embed & Sign`.
3. In `General` of `BanubaSdk.xcodeproj` replace `BanubaEffectPlayer.framework` with `BanubaEffectPlayer.xcframework` and mark it as `Do Not Embed`.
4. In `Build Phases` of your project add BanubaSdk as a dependency.
5. Make sure that you have correct `Framework Search Path` to `Frameworks` folder in your project and `BanubaSdk.xcodeproj`.
6. Now you can run your project with the Banuba SDK on your device or simulator.
