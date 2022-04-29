# Banuba SDK iOS

Banuba SDK delivery includes the following parts: `BanubaSdk.framework`and `BanubaEffectPlayer.xcframework`.

`BanubaEffectPlayer.xcframework` provides a relativly low-level cross-platform API which is described in the API reference.

`BanubaSdk.framework` is build on the top of `BanubaEffectPlayer.xcframework` and provides the iOS-specific functionality.

`BanubaEffectPlayer.xcframework` provided in the compiled form and `BanubaSdk.framework` in sources are available for your reference and fine-tuning.

The entry point to `BanubaSdk.framework` is `BanubaSdkManager` class. This class provides the following functionality:

* Rendering layer configuration -- `setRenderTarget` (`RenderTarget` on the diagramm).
* Start/stop Effect Player -- `startEffectPlayer`, `stopEffectPlayer`.
* Continuous photo rendering (i.e. the dynamic effect applied to the frozen image) -- `startEditingImage`, `captureEditedImage`, `stopEditingImage`.
* Take a photo with the camera and apply the current effect -- `makeCameraPhoto`.
* Apply the effect to an in-memory photo (e.g. images created from files) -- `processImageData`.
* Apply the watermark while rendering -- `configureWatermark`, `removeWatermark`.
* Apply the effect to the sequence of frames in memory (e.g. video file) -- `startVideoProcessing`, `stopVideoProcessing`, `processVideoFrame`.
* Push a frame from the camera -- `push`.
* Take snapshots -- `output?.takeSnapshot`.
* Record a screen video with effects applied -- `outputService.startVideoCapturing`, `outputService.stopVideoCapturing` (`OutputService` and `SBVideoWriter` on the diagramm).
* Send frames to other destinations (e.g. via WebRTC) -- `outoutService.startForwardingFrames`, `outputService.stopForwardingFrames`.
* Camera and audio input control -- `input`(instanse of `InputService`, see the diagramm).
* Capturing the frames rendered (in binary form, used for debugging) -- `setFrameDataRecord`.
* Voice Changer (change user's voice in videos) -- `voiceChanger`.

The Effect component makes up an essential part of the SDK usage. The effect is represented as a folder with scripts and resources. Please, refer to the iOS demo app section for more details about effects.

### Configuring watermark

If you wan't to apply watermark to your photos, you should use `output?.takeSnapshot` method instead of `makeCameraPhoto`. Watermark can be used only with snapshots made with `takeSnapshot`.

```swift
guard let watermark = UIImage(named: "YOUR_WATERMARK_IMAGE") else { return }
let offset = CGPoint(x: 20.0, y: 10.0)
let watermarkInfo = WatermarkInfo(image: watermark,
    corner: .bottomLeft, offset: offset, targetNormalizedWidth: 0.7)
sdkManager.configureWatermark(watermarkInfo)
let config = OutputConfiguration(applyWatermark: true, adjustDeviceOrientation: true, 
    mirrorFrontCamera: false)
sdkManager.output?.takeSnapshot(configuration: config) {}
```

### Configuring AVAudioSession

In Banuba SDK, the AVAudioSession is set to category `.ambient` by default. You can change it to another category using the `InputService.swift` file, the `startCamera()` method.

```swift
public func startCamera() {
    configureAudioSessionWithCategory(.ambient)
    if #available(iOS 11.0, *), useARKit,
       let arSession = arSession,
       let arConfiguration = arConfiguration {
        arSession.run(arConfiguration, options: .default)
        return
    }
    cameraSessionQueue.async { [weak self] in
        guard let self = self, let session = self.cameraCaptureSession else { return }
        session.startRunning()
    }
}
```

You can modify AVAudioSession mode and the options that will be appropriate for your app’s behaviour using the `configureAudioSessionWithCategory` method.

```swift
private func configureAudioSessionWithCategory(_ category: AVAudioSession.Category) {
    let audioSharedSession = AVAudioSession.sharedInstance()
    do {
        try audioSharedSession.setCategory(category, mode: .default, options: .mixWithOthers)
        try audioSharedSession.setActive(true)
    } catch {
        print(Defaults.configureAudioSessionFailedMessage)
    }
}
```

### Reject from Apple Connect

:::note Apple may reject your app if it uses TrueDepth APIs, but doesn't include all of the information in its privacy policy required by Guideline 5.1.1 of the App Store Review Guidelines and Section 3.3.10 of the Apple Developer Program License Agreement. :::

Banuba SDK uses `ARKit`, therefore, to avoid your app rejection, please check our [privacy policy](http://banubafilters.com/privacy-policy/) where we describe the usage of ARKit and TrueDepth API.

:::info Still have any questions about FaceAR SDK for iOS? Visit our [FAQ](https://www.banuba.com/faq/) or contact our support. :::
