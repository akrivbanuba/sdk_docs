# Offscreen Effect Player iOS

### Offscreen Effect Player briefly

Offscreen Effect Player (OEP) allows processing an image using the Banuba SDK, no matter where it comes from, e.g. the camera, file system, or somewhere else. OEP is a camera-independent solution that returns a processed image in the same form as it was received. This means that an input image orientation stays the same after Banuba SDK processing as it was before (depends on the options in EpImageFormat). Additionally, OEP allows drawing the processed image on an external texture.

The entry point to Offscreen Effect Player is `BNBOffscreenEffectPlayer` class. This class provides the following functionality:

* Manage image processing — `processImage`.
* Apply the effect to the processed image (e.g. camera frame image of image from disk) — `loadEffect`, `unloadEffect`.
* Manage surface size — `surfaceChanged`.
* Manage audio — `enableAudio`.
* Calling active effect methods defined in effect's script - `callJsMethod` (obsolete).
* Execute scripts (calling methods) or load JS modules into the environment of the active effect - `evalJs`.

_NOTE:_ By default the Effect Player has enabled audio, so effects will play sounds if configured. It is necessary to use manual audio only if you use OEP in conjuction with _CallKit_ framework. In this case, OEP should be configured with manual audio and OEP's audio should be enabled only when _CallKit_ notifies application that it completed initialization of its Audio session.

### Offscreen Effect Player EpImageFormat

This structure describes the format of the input and output images:

* `imageSize` - the size of the input image, should be equal to the Width, Height of the input buffer
* `orientation` - The orientation of the input image. Possible values `EPOrientationAngles0, EPOrientationAngles90, EPOrientationAngles180, EPOrientationAngles270`. See the details in the 'Image Orientation' section.
* `resultedImageOrientation` - The orientation of the output image. If it matches `orientation` then the image will be returned in the same orientation. Set to `EPOrientationAngles0` to keep OEP default orientation (portrait, head directed at the top - relies on the right `orientation` value). Possible values `EPOrientationAngles0, EPOrientationAngles90, EPOrientationAngles180, EPOrientationAngles270`. See thr details in the 'Image Orientation' section.
* `isMirrored` - If YES then the resulting image will be mirrored. See more details here.
* `needAlphaInOutput` - This parameter is used to specify that the output image should include an Alpha channel. This feature can be used if you want to get transparent background and place the output image above another image/video to imitate overlay for presentation on a whiteboard.
* `overrideOutputToBGRA` - when the input format is YUV, the output format by default will be also YUV, as all rendering is performed on the texture in the RGBA format. Since conversion to YUV takes time, this parameter lets you save a few milliseconds on image conversion.
* `outputTexture` - The Banuba SDK renders the image using the GPU, so in some cases when it is not necessary to have an access to the image's memory buffers on the application side, the format of the output image may be returned as an OGL texture, which improves performance in some cases since there is no need to sync data between GPU and CPU. Please note that as soon as `CVPixelBufferLockBaseAddress` is called, the sync will be performed, so this should be used for the cases when only output buffer rendering is necessary, e.g. output image as an image of `UIImageView`.

### Image Orientation

#### Offscreen Effect Player (OEP) surface

When you create the OEP instance, it is necessary to specify the surface size of the Effect Player.

```swift
let config = BNBEffectPlayerConfiguration.init(fxWidth: 720, fxHeight: 1280, nnEnable: .automatically , faceSearch: .good, jsDebuggerEnable: false, manualAudio: manualAudio)
let ep = BNBEffectPlayer.create(config)

effectPlayer = BNBOffscreenEffectPlayer.init(effectPlayer: ep!, offscreenWidth: width, offscreenHight: height)
```

As you can see in the source code above, the Effect Player object is used as an input parameter for `BNBOffscreenEffectPlayer.init` method. In this case, OEP is initialized with pre-created instance of the `BNBEffectPlayer`, so you can assign more listeners related to `BNBEffectPlayer`.

The surface size determines the effective area for OEP's rendering, so if the surface size is 1280x720 (width, height correspondingly) the surface will have the following look:

In the case of the OEP's surface size 720x1280 the surface will be:

:::note When the Effect Player renders the input image, it orients it according to the `orientation` parameter. It is assumed that by `orientation` parameter of `EpImageFormat` user lets Offscreen Effect Player know how the image should be rotated so that the head of the person in the picture/frame is at the top. :::

The surface size of the OEP determines the size of the output image.

If the input image is larger or smaller than the OEP's surface, the input image is zoomed in to fit the surface, e.g. if the input image is 1080x1920 and OEP's surface size is 720x1280 then the input image will be scaled without borders around the image to that surface during rendering because the ratio of the surface and the input image is the same. But if the OEP's surface is 1280x720 and the input image is 1080x1920 then after the input image is being processed there will be green borders (color depend on OGL texture options) on the output image:

:::note In order to avoid unexpected results like the zoomed output you should keep the input image ratio and the OEP's surface ratio synchronized and they should be equal. :::

The iOS application can have a fixed orientation UI or UI that can be rotated with the device orientation. For the second case it is necessary to let OEP know that it should update its surface to render image properly for further preview:

```swift
private func rotateBNBOffscreenEffectPlayer() {
   switch UIApplication.shared.statusBarOrientation {
   case .portrait:
       uiOrientation = .portrait
       effectPlayer?.surfaceChanged(renderWidth, withHeight: renderHeight)
   case .portraitUpsideDown: // Impossible case, at least no such event raised
       uiOrientation = .portraitUpsideDown
       effectPlayer?.surfaceChanged(renderWidth, withHeight: renderHeight)
   case .landscapeLeft:
       uiOrientation = .landscapeLeft
       effectPlayer?.surfaceChanged(renderHeight, withHeight: renderWidth)
   case .landscapeRight:
       uiOrientation = .landscapeRight
       effectPlayer?.surfaceChanged(renderHeight, withHeight: renderWidth)
   default:
       break
   }
}
```

#### Input image orientation

When you configure the camera you can specify the camera's output image orientation, which will in turn determine OEP's input image orientation:

```swift
if let captureConnection = output.connection(with: .video) {
    captureConnection.videoOrientation = .landscapeRight
}
```

Let us consider resolution 1280x720. The following options are available for the Portrait device orientation (device's action zone at the bottom):

* Portrait - a device's action zone at the bottom. It corresponds to the image, oriented following way:
* Portrait Upside down - the same as `Portrait`, but the image is flipped vertically
* Landscape right - a device's action zone is on the right. Note that the image from the camera is in landscape orientation and rotated by 90 degrees (counterclockwise), but the device is in portrait orientaiton.
* Landscape left - the same as `Landscape right` mode but the action zone of the device is on the left.

:::note If not configured, the output image orientation the default value is `Landscape left` the Orientation 270 degrees. :::

:::note Depending on the camera lens type (front or back), the image from the camera can be mirrored. This should be also taken into account together with the Application UI orientation.

```swift
private func getImageOrientation() -> EPOrientation {
    if outputVideoOrientation == .landscapeRight {
        if uiOrientation == .portrait {
            return cameraPosition == .front ? .angles270 : .angles90
        }
        else if uiOrientation == .portraitUpsideDown {
            return cameraPosition == .front ? .angles90 : .angles270
        }
        else if uiOrientation == .landscapeRight {
            return .angles0
        }
        // .landscapeLeft
        return .angles180
    }
    else if outputVideoOrientation == .landscapeLeft {
        if uiOrientation == .portrait {
            return cameraPosition == .front ? .angles90 : .angles270
        }
        else if uiOrientation == .portraitUpsideDown {
            return cameraPosition == .front ? .angles270 : .angles90
        }
        else if uiOrientation == .landscapeRight {
            return .angles180
        }
        // .landscapeLeft
        return .angles0
    }
    else if outputVideoOrientation == .portrait {
        if uiOrientation == .portrait {
            return .angles0
        }
        else if uiOrientation == .portraitUpsideDown {
            return .angles180
        }
        else if uiOrientation == .landscapeRight {
            return cameraPosition == .front ? .angles90 : .angles270
        }
        // .landscapeLeft
        return cameraPosition == .front ? .angles270 : .angles90
    }
    else { // .portraitUpsideDown
        if uiOrientation == .portrait {
            return .angles180
        }
        else if uiOrientation == .portraitUpsideDown {
            return .angles0
        }
        else if uiOrientation == .landscapeRight {
            return cameraPosition == .front ? .angles270 : .angles90
        }
        // .landscapeLeft
        return cameraPosition == .front ? .angles90 : .angles270
    }
}
```

:::

#### Output image orientation

For the orientation of the output image, the same logic is applicable as for the Input Image orientation, but it depends on the goals of your application. As mentioned above, if `orientation` of EpImageFormat is equal to `resultedImageOrientation` then the output image will be oriented the same way as the input image.

### Offscreen Effect Player use cases

The general usage of OEP assumes the next sequence: frames from camera fed to OEP instance, it can be used for sync or async image processing, returned image is rendered on the screen or additionally processed before rendering. Such use case is shown in the OEP iOS demo application. The sample also demonstrates asynchronous loading of effects and rendering bypassing OEP if the effect is not loaded.

Please, refer to OEP iOS demo app section for more details about Offscreen Effect Player using by the Demo application.
