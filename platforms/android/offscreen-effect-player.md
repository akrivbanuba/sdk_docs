# Offscreen Effect Player

Offscreen Effect Player (OEP) allows processing an image using Banuba SDK, no matter where it comes from: the camera, file system or somewhere else. OEP is the camera independent solution that returns a processed image in the same form as received. It means that an input image orientation stays unchanged after Banuba SDK processing. Additionally, OEP can draw the processed image on an external texture.

The entry point to Offscreen Effect Player is `OffscreenEffectPlayer` class. This class provides the following functionality:

*   Manage image processing — `processImage`, `processFullImageData`, `processFullImageDataNoSkip`, `setImageProcessListener`.

    ```java
    /**
     * Send Image to process
     * Image will be closed inside OffscreenEffectPlayer
     *
     * @param image       Android image to process
     * @param orientation describes current image orientation
     */
    public void processImage(@NonNull Image image, @NonNull ImageOrientation orientation);

    /**
     * Send Image to process
     * Image will be closed inside OffscreenEffectPlayer
     *
     * @param image             Android image to process
     * @param orientation       describes current image orientation
     * @param outputImageFormat describes output Image Format (RGBA, I420_BT601_FULL, I420_BT601_VIDEO, I420_BT709_FULL, I420_BT709_VIDEO)
     */
    public void processImage(@NonNull Image image, @NonNull ImageOrientation orientation, @NonNull OEPImageFormat outputImageFormat);

    /**
     * Send FullImageData to process. FullImageData is a container for the Image object or buffers representing image in a specific format.
     *
     * @param fullImageData     Instance of FullImageData object
     * @param releaseCallback   is called by OEP when image stored in fullImageData can be released. If releaseCallback is passed
     *                          then Image data isn't copied to improve performance. If a releaseCallback is passed and an Image
     *                          is used, undefined behavior may occur when the ImageReader is closed and then opened again. In order
     *                          to avoid this, it is necessary to call playbackStop before closing the camera and playbackPlay after opening it.
     * @param timestamp         lets you associate frame with the timestamp in order to identify it at ImageProcessedListener call
     */
    public void processFullImageData(@NonNull FullImageData fullImageData, @Nullable ReleaseCallback releaseCallback, long timestamp);

    /**
     * Send FullImageData to process. FullImageData is a container for the Image object or buffers representing image in a specific format.
     *
     * @param fullImageData     Instance of FullImageData object
     * @param releaseCallback   is called by OEP when image stored in fullImageData can be released. If releaseCallback is passed
     *                          then Image data isn't copied to improve performance. If a releaseCallback is passed and an Image
     *                          is used, undefined behavior may occur when the ImageReader is closed and then opened again. In order
     *                          to avoid this, it is necessary to call playbackStop before closing the camera and playbackPlay after opening it.
     * @param outputImageFormat OEPImageFormat - (RGBA, I420_BT601_FULL, I420_BT601_VIDEO, I420_BT709_FULL, I420_BT709_VIDEO)
     * @param timestamp         lets you associate frame with the timestamp in order to identify it at ImageProcessedListener call
     */
    public void processFullImageData(@NonNull FullImageData fullImageData, @Nullable ReleaseCallback releaseCallback, @NonNull OEPImageFormat outputImageFormat, long timestamp);

    /**
     * Meaning and parameters are the same as for processFullImageData but in that case the image will wait in the queue until processed,
     * i.e. every image is processed without drops even if another image is being processed at this moment.
     */
    public void processFullImageDataNoSkip(@NonNull FullImageData fullImageData, @Nullable ReleaseCallback releaseCallback, long timestamp);

    /**
     * Sets ImageProcessListener
     * The callback will be invoked on handler's thread.
     * Can be used together with surfaceTexture.
     * In this case OffscreenEffectPlayer will render to SurfaceTexture and send image to listener
     *
     * Passing NULL/NULL will disable prepare and send Buffers to listener
     *
     * @param listener The listener to use, or null to remove the listener.
     * @param handler  The handler on which the listener should be invoked, or null to remove the listener
     */
    public void setImageProcessListener(@Nullable ImageProcessedListener listener, @Nullable Handler handler);
    ```
*   Working with external texture = `setSurfaceTexture`.

    ```java
    /**
     * Sets SurfaceTexture
     * Can be used together with ImageProcessListener.
     * In this case OffscreenEffectPlayer will render to SurfaceTexture and send image to listener
     *
     * Passing NULL will disable render to SurfaceTexture
     *
     * @param surfaceTexture The surfaceTexture to use, or null to remove.
     */
    public void setSurfaceTexture(@Nullable SurfaceTexture surfaceTexture);    
    ```
*   Apply the effect to an processed image (e.g. camera frame image of image from disk) — `loadEffect`, `unloadEffect`.

    ```java
    /**
     * Load effect to the effect player.
     *
     * @param effectName the name of an effect (folder) in the app resource storage
     */
    public void loadEffect(@NonNull String effectName);

    /**
     * Unload active effect. The effect stays in the cache so another loading of the same effect is faster.
     */
    public void unloadEffect();
    ```
*   Calling any effect methods - `callJsMethod`.

    ```java
    /**
     * Let call methods defined in the script of the active effect, to configure effect or manage its state.
     *
     * @param method - the name of js method
     * @param parameter - the parameter to pass to the method
     *
     */
    public void callJsMethod(@NonNull String method, @NonNull String parameter);
    ```

The main advantage of `OffscreenEffectPlayer` compared to `BanubaSdkManager` is that the OEP does not depend on the camera module. Note, the best performance is achieved if OEP uses the `ExternalTexture` (see `SurfaceTexture`) as an output. In this case, the output image is returned in ARGB format. It lets you bypass GPU-CPU synchronization. If the `ExternalTexture` is not used, the output image is returned as the byte buffer in YUV I420 reduced range video format (BT.601 420v). See the `YUVConverterMod.java` and `ImageProcessResult.java` classes from delivery bundle for more details. The OEP simply expects an input image buffer to process it by Banuba SDK. In this case, the camera image acquiring should be implemented externally if necessary. The camera image acquiring implementation can be considered as the main disadvantage of OEP solution.

The Banuba SDK delivery bundle contains the OEP sources in the `offscreen` directory from the `banuba_sdk` module. The `offscreen` directory contains the following main classes:

* `OffscreenEffectPlayer` - the main class of the Offscreen Effect Player (OEP) module.
* `OffscreenEffectPlayerConfig` - the Offscreen Effect Player configuration class.
* `BufferAllocator` - the interface for buffer allocation. May be used in the application for retaining buffers.
* `ImageDebugUtils` - the utility class that allow saving an image for debuggin.
* `ImageOrientation` - the class that helps to make a proper image orientation based on the camera or image parameters.
* `ImageProcessResult` - the class of a processed image.

You can use Offscreen Effect Player with or without surface texture. Surface texture is set by the `setSurfaceTexture` method of the `OffscreenEffectPlayer` class. Please, refer to OEP Android demo app section for more details about Offscreen Effect Player usage with a Demo application.
