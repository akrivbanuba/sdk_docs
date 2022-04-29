# Offscreen Effect Player Demo App

### Requirements

* Latest stable Android Studio
* Latest Gradle plugin
* Latest NDK

### Get the client token

To start working with the Banuba SDK Demo project for Android, you need to have the client token. To receive the **trial** client token please fill in our [form on banuba.com](https://www.banuba.com/face-filters-sdk) website, or contact us via [info@banuba.com](mailto:info@banuba.com).

:::note Before building the Android Offscreen Effect Player Demo project, place your client token inside an appropriate file in the following location:\
`src/offscreen/src/main/java/com/banuba/offscreen/app/BanubaClientToken.java` :::

#### Client token usage example

```java
final class BanubaClientToken {
    public static final String KEY = "YOUR_TOKEN_HERE";

    private BanubaClientToken() {
    }
}
```

### Get the Banuba SDK archive

With the client token, you will also receive the Banuba SDK archive for Android which contains:

* Banuba Effect Player (compiled Android library project with .aar extension),
* Android project folder (src) which contains demo apps, located in `src/app` and `src/offscreen` respectively.

### Build the Banuba SDK OEP Demo app

1. Import the Android project under `src` folder in Android Studio.

\<img src={require("@site/static/img/android/android\_getting\_started\_2.png").default} width="428px"/>

1. Select the needed application for the build.

\<img src={require("@site/static/img/android/android\_getting\_started\_8.png").default} width="381px"/>

1. Select Build Variant from the left side menu in Android Studio.

* `Debug` build variant allows to properly debug and profile app during its execution.
* `Release` build variant allows testing release variant of the application for faster performance.

\<img className="shadow--md" src={require("@site/static/img/android/android\_getting\_started\_5.png").default} width="512px"/>

### Offscreen Effect Player Demo App briefly

The application shows different conveyors for image processing when the active effect is rendered to the buffer in the memory. Additionally, it shows how to configure input image orientation for processing in the different device orientations and video frame sources.

**SURFACE** mode buttons in the picture above reflect the usage of Offscreen Effect Player with Surface texture.

Offscreen Effect Player Demo app contains the following packages:

* `camera` — the camera capture functionality. See `Camera2Simple`, `Camera2SimpleThread` and `CameraWrapper`.
* `fragments` — the fragment configuration functionality.
* `gl` — the needed Open GL ES configuration functionality.
* `orientation` — the device orientation change observing functionality.
* `render` — the rendering purpose functionality. See `CameraRenderSurfaceTexture` and `CameraRenderYUVBuffers`.

### Offscreen Effect Player notes

1.  The `BanubaSDKManager` is not used in the case of OEP. Instead, use the `OffscreenEffectPlayer` class. You can use only one static method `BanubaSdkManager.initialize(Context, BNB_KEY)` to initialize Banuba SDK with the token. See the `CameraFragment.java` class from the Offscreen Demo app. There are two cases of Banuba SDK initialization in the case of OEP: using `EffectPlayerConfiguration` or `OffscreenEffectPlayerConfig`:

    ```java
    // NOTE: for initializing the EffectPlayer inside the Offscreen Effect Player uncomment the next code block
    /*final OffscreenEffectPlayerConfig config =
        OffscreenEffectPlayerConfig.newBuilder(SIZE, mBuffersQueue).build();
    mOffscreenEffectPlayer = new OffscreenEffectPlayer(mContext, config, BNB_KEY);
    */

    BanubaSdkManager.initialize(mContext, BNB_KEY);
    mEffectPlayer = Objects.requireNonNull(EffectPlayer.create(config));
    mOffscreenEffectPlayer = new OffscreenEffectPlayer(
        mContext, mEffectPlayer, SIZE, OffscreenSimpleConfig.newBuilder(mBuffersQueue).build());
    ```

As you can see in the above source code, the `mEffectPlayer` object is used as an input parameter for the `OffscreenEffectPlayer` constructor. In this case, OEP is initialized with pre-created `EffectPlayer`. You can assign more listeners related to `EffectPlayer`.

The OEP is included in the `banuba_sdk` module that is available with sources, and you can see the structure and architecture of the OEP. The main idea is that OEP is not responsible for camera frame acquiring. OEP just processes an input image and returns the processed image synchronously either as a buffer (see the `OffscreenEffectPlayer.setImageProcessListener`) or draw a processed image on the texture (see the `OffscreenEffectPlayer.setSurfaceTexture`).

The Offscreen effect player will create a rendering surface taking the min value of `SIZE` dimensions as an OEP surface width and the max value of `SIZE` as a surface height. In the sample above we have surface size 720x1280 (width, height correspondingly).

The surface size determines the effective area for OEP's rendering. So if the surface size is 720x1280 (width, height correspondingly) the surface will have the following look:

If UI changes orientation with a size of 1280x720, the OEP surface will have the following look:

The rendering surface size of OEP determines the size of the output image.

Offscreen Effect Player automatically manages the surface size if an application changes UI orientation.

1. For processing input camera frames, use methods `OffscreenEffectPlayer.processImage` or `OffscreenEffectPlayer.processFullImageData`. The processed image you can get via `ImageProcessedListener.onImageProcessed` (see the `OffscreenEffectPlayer.setImageProcessListener` method) in the case of processed image buffer. Or the OEP can draw processed image on the texture (see the `OffscreenEffectPlayer.setSurfaceTexture`). Next methods should not be used with OEP: `BanubaSDKManager.attachSurface`, `BanubaSDKManager.effectPlayerPlay`, `BanubaSDKManager.startForwardingFrames` and other methods of `BanubaSDKManager` related with the camera frames processing.
2. For loading an effect, use the method `OffscreenEffectPlayer.loadEffect` instead of `BanubaSDKManager.loadEffect`.
3. For making `FullImageData`: Use the `OrientationHelper` class to set the right face orientation based on the camera and the image orientations.

:::note The face orientation parameter ensures the proper performance of the recognition model. The correct image orientation ensures the right image processing by the neural network. :::

The steps of `OrientationHelper` usage include:

```java
OrientationHelper.getInstance(context).startDeviceOrientationUpdates(); // starting the OrientationEventListener
...
final boolean isRequireMirroring = isFrontCamera; // this parameter should be configured externally and depend on camera facing (front/back)
int deviceOrientationAngle = OrientationHelper.getInstance(context).getDeviceOrientationAngle();
if (!isFrontCamera) {
    // this correction is needed for back camera frames correct orientation making because OEP does not know about camera facing at all
    if (deviceOrientationAngle == 0) {
        deviceOrientationAngle = 180;
    } else if (deviceOrientationAngle == 180) {
        deviceOrientationAngle = 0;
    }
}

final FullImageData.Orientation orientation = OrientationHelper.getFullImageDataOrientation(
    videoFrame.getRotation(),
    deviceOrientationAngle,
    isRequireMirroring);

FullImageData fullImageData = new FullImageData(new Size(width, height), i420Buffer.getDataY(),
        i420Buffer.getDataU(), i420Buffer.getDataV(), i420Buffer.getStrideY(),
        i420Buffer.getStrideU(), i420Buffer.getStrideV(), 1, 1, 1, orientation);
```

Where the `videoFrame` is WebRTC `VideoFrame` object but it can be any other frame object type. After `FullImageData` creation it should be passed into `OffscreenEffectPlayer.processFullImageData` method.

You also can review how the Offscreen Demo app manages the input image orientation: The application's UI orientation is necessary to determine the OEP input image orientation:

```java
mOrientationListener = new FilteredOrientationEventListener(context) {
    @MainThread
    @Override
    public void onOrientationFilteredChanged(int deviceSensorOrientation, int displaySurfaceRotation) {
        mCameraHandler.sendOrientationAngles(deviceSensorOrientation, displaySurfaceRotation);
    }
};
```

Based on this information, the input image orientation is calculated:

```java
    private ImageOrientation getImageOrientation(boolean isRequireMirroring) {
        int rotation = 90 * mDisplaySurfaceRotation;
        int deviceOrientationAngle = mDeviceOrientationAngle;

        if (mFacing == CameraCharacteristics.LENS_FACING_BACK) {
            rotation = 360 - rotation;

            if (mDeviceOrientationAngle == 0) {
                deviceOrientationAngle = 180;
            } else if (mDeviceOrientationAngle == 180) {
                deviceOrientationAngle = 0;
            }
        }

        final int imageOrientation = (mSensorOrientation + rotation) % 360;

        return ImageOrientation.getForCamera(imageOrientation, deviceOrientationAngle, mDisplaySurfaceRotation, isRequireMirroring);
    }
```

1. Use the `OffscreenEffectPlayer.callJsMethod` method instead of `BanubaSDKManager.effectManager.current().callJsMethod`. The `OffscreenEffectPlayer.callJsMethod` is obsolete use `OffscreenEffectPlayer.evalJs` method instead.
2.  The processed image may be returned by OEP via `ImageProcessedListener.onImageProcessed` callback method (see the `OffscreenEffectPlayer.setImageProcessListener` method). Also, OEP may draw the processed image on the texture (see the `OffscreenEffectPlayer.setSurfaceTexture`). So the `IEventCallback.onFrameRendered` callback is not used in the case of OEP at all. Use the `ImageProcessedListener.onImageProcessed` instead. See the `CameraRenderYUVBuffers.constructHandler` from the Offscreen Demo app sources for more details:

    ```java
    protected CameraRenderHandler constructHandler() {
        mHandler = new CameraRenderHandler(this);
        mOffscreenEffectPlayer.setImageProcessListener(result -> {
            if (mImageProcessResult != null && mBuffersQueue != null) {
                mBuffersQueue.retainBuffer(mImageProcessResult.getBuffer());
            }
            mImageProcessResult = result;
            mHandler.sendDrawFrame();
            }, mHandler);
        return mHandler;
    }
    ```

    If rendering to the texture is not used, the output image orientation will coincide with the input image orientation.
3. `ImageProcessResult` buffer represents the resulted YUV image in the follwoing layout:

where bytes per row for the Y plane is `ImageProcessResult.getPixelStride(0);`, for U and V planes correspondingly `ImageProcessResult.getPixelStride(1);` and `ImageProcessResult.getPixelStride(2);`.\
See below the code sample on how to get I420 buffer from the `ImageProcessResult`:

```java
// result -> this is an ImageProcessResult object in onImageProcessed
final ByteBuffer buffer = result.getBuffer();
mBuffersQueue.retainBuffer(buffer);

JavaI420Buffer I420buffer = JavaI420Buffer.wrap(
        result.getWidth(), result.getHeight(),
        result.getPlaneBuffer(0), result.getBytesPerRowOfPlane(0), // Y plane
        result.getPlaneBuffer(1), result.getBytesPerRowOfPlane(1), // U plane
        result.getPlaneBuffer(2), result.getBytesPerRowOfPlane(2), // V plane
        () -> {
            JniCommon.nativeFreeByteBuffer(buffer);
        });
```
