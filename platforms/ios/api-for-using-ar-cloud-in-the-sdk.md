# API for using AR cloud in the SDK

AR Cloud is a client-server solution that helps to save space in your application. This is a product used to store AR filters i.e. masks on a server-side instead of the SDK code. After being selected by the user for the first time, the filter is going to be downloaded from the server and then saved on the phone's memory.

\<a className="button button--outline button--primary" href="https://github.com/Banuba/arcloud-ios-swift"

>

Example of using AR cloud\
\


Banuba SDK AR Cloud delivery solution includes the `BanubaARCloudSDK.xcframework` with `BanubaUtilities.xcframework` libraries that should be placed into [Frameworks folder](https://github.com/Banuba/arcloud-ios-swift/tree/master/Frameworks) directory.

You can find this libraries here: [BanubaARCloudSDK.xcframework](https://github.com/Banuba/BanubaARCloudSDK-IOS), [BanubaUtilities.xcframework](https://github.com/Banuba/BanubaUtilities-iOS)

### Follow these steps to configure AR Cloud:

#### 1. Paste AR Cloud Url value

Paste AR Cloud client id value into [BanubaClientToken.swift](https://github.com/Banuba/arcloud-ios-swift/blob/master/arcloud-ios-swift/BanubaClientToken.swift#L4).

```swift
// Add your AR Cloud Url instead of empty quotes
internal let banubaArCloudURL: String = "Place your AR Cloud Url here"
```

:::info Please ask Banuba representative to provide you with **client id** for the trial period. :::
