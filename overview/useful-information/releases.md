# Releases

### \[1.4.0] - 2022-04-20

**Added**

* Face AR SDK for iOS and Android distrubution as pods or maven packages
  * iOS, Android: All Face AR SDK examples on Github are switched to pods, maven packages
* Components-based face tracking for all supported platforms (only in online mode)
* Unity: brand-new demo scene with effects carousel
* Android: restored external texture support to the `effect_player`
* Hand AR: Textured nails
* M1 simulators support restored
* Makeup API: Eyebrows makeup
* WebAR: ability to load Effect via Request
* WebAR: ability to play gif as background texture
* WebAR: Effect.preload progress listener
* WebAR: Check out our new tutorials section with extensive WebAR insides and best-practices
* Rendering Engine: glTF support

**Changed**

* iOS: Upgraded lips segmentation neural network
* B\&W lips coloring support without additional parameters
* Makeup API: reduced amount of uniforms
* WebAR: Improved WebAR archive UX
* Rendering Engine: Reduce LUT memory size
* OEP: extend supported image formats

**Fixed**

* Black screen flash on effects loading
* Android: Memory leak in the OEP
* Android: Pixel 3a crash after applying certain face filters
* Android: deadlock during video\_frame draw
* Android: Xiaomi Mi 8 Pro crash
* iOS: iPhone 13 recognized as middle-end hardware
* Fixed invisible entities for some face filters
* Effects API: `Api.drawingAreaWidth()` & `Api.drawingAreaHeight()` return 0
* Windows: Impossible to apply effect with path containing extended Unicode
* Windows, MacOS: Banuba Viewer saving video without sound
* MSAA issues in face filters
* WebAR: Fixed processing of RGB images
* WebAR: Fixed MediaStreamCapture crash on Safari 14
* Makeup API: Fixed serialization of empty textures
* Hand AR: hand skeleton false detections
* OEP: crash if imput buffer format changes
* OEP: green frame if texture is not ready
* OEP: fixed rapid camera switch

### \[1.3.1] - 2022-03-02

**Changed**

* OCV-based camera on Windows is able to select camera by index

**Fixed**

* OEP crash or black background on first сhoice of background blur
* OEP Metal crash
* `noFaceActions` & `faceActions` functions incorrect call in config.js
* Viewer v1.3.0 crash on Macbook
* WebAR: MediaStreamCapture produces black frames
* WebAR: Makeup effect crashes web page on iPhone 8, iOS 15
* WebAR: Fixed result of `ImagCapture.takePhoto`
* WebAR: Effect crashes on iOS Safari
* WebAR: Effect animations lag on iOS Safari 14
* Android alooper crash
* Photo loading black screen: buffer is not large enough for dimensions
* Incorrect face texture display when using lips correctors
* Hand skeleton can be recognized on different objects

### \[0.38.6] - 2022-02-16

**Added**

* Offscreen app perf improvement

**Changed**

* Drop any frame\_data fields on effect loading

**Fixed**

* Fix SDK work on Android 6
* Recording audio from effect\_player to file
* Crash when making photo or video from Demo App
* Avoid copy frame for the case of Banuba SDK Demo
* OEP Android FATAL EXCEPTION: CameraThread
* Distorted image after turning on blur for row stride not equal width

### \[1.3.0] - 2022-01-27

Version 1.3.0 also includes all changes from SDK v0.x releases up to v0.38.5 version. Please, refer to the changelog below.

**Added**

* Face tracking antijitter based on optical flow algorithm
* Ability to draw face mesh landmarks (and test effect)
* Face mesh lips correctors (optional)
* Face mesh eyebrows correctors (optional)
* Native Metal API support (iOS, MacOS)
* Metal multiinstance
* arm64 support with Metal backend for simulators and MacOS
* Makeup API: Lips morphing
* WebAR: Tflite libs for emscripten (3.0.1)
* WebAR: Throw error when rendering to unexpected DOM element
* unloadEffect method
* OEP: Metal YUV converter
* [SDK Manager](pathname:///generated/javadoc/manager) added to the API documentation
* AR Rings technology

**Changed**

* WebAR: TFLite delegate creation failed error now shows as warning
* WebAR: Optimized CPU and GPU usage
* WebAR: Reduced RAM usage and camera pixels retrieving time
* WebAR: Added warning if effect.evalJs is called before the effect application
* Rebuild OpenCV for Android only with required set of features
* Switch Hand Gestures and recognition to Tflite for iOS and Mac
* Android Beauty example switched to the Makeup API usage
* Face mesh correctors are controlled directly from needed effects (including Makeup API)
* Android Demo app can be built now with Java 11+ and Gradle 7+ versions
* Correct work of alpha channel blending (used in background transparency)
* OEP: Improved performance of YUV converter for Android
* Makeup API: Improved the effect activation time
* Removed copying of U and V textures for i420

**Fixed**

* Makeup API: Correctly resolve loading resources from different modules
* Makeup API: Hair blending incorrect brightness
* Makeup API: Incorrect blur behavior when comparing to 0.x version
* WebAR: Electron: Licence error 0xff00f
* WebAR: User-friendly error messages for misconfigured `locateFile`
* WebAR: Delay in loading animation on Safari
* WebAR: Makeup effect crashes iOS Safari
* WebAR: Fixed GPU memory leak
* Various crashes in the Offscreen Effect Player (OEP)
* SDK v1.1.0 crashed on unload effect in the Android quickstart app
* Incorrect work of Api.playVideoRange
* Windows: Effects cannot be enabled when extended Unicode is used in the app's location name
* Windows: OEP-desktop-c-api example build has failed to launch
* Android Demo app has crashed on switching effects and closing activity
* iOS: `sdkManager.output?.takeSnapshot` method not working in sdk 1.x
* iOS: Distorted videos/snapshots when using non-standard RenderSize

### \[0.38.5] - 2021-12-14

**Added**

* EffectPlayer sound playback recording

**Changed**

* Android: Updated lips segmentation neural network

**Fixed**

* Incorrect shiny lips application
* OEP: fix YUV aliasing

### \[1.2.1] - 2021-12-01

**Fixed**

* iOS: x86\_64 simulator support
* Makeup API: Incorrect display of blurred background
* Makeup API: Incorrect virtual background ratio in landscape mode
* Virtual background: Incorrect alpha blending when using transparent images

### \[1.2.0] - 2021-11-24

Version 1.2.0 also includes all changes from SDK v0.x releases up to v0.38.4 version. Please, refer to the changelog below.

**Added**

* Hand gestures and Hand skelet model for all platforms
* Light Streaks effect support in Scene (1.x versions)
* Add warning if version of neural nework and FaceAR SDK are different
* Face skin segmentation neural netrowk for Tflite (all platforms except iOS and MacOS)
* Makeup API: Eyelashes 3D support
* Android: Automatically select RGB or YUV camera mode (better performance on some low and mid-end devices)
* WebAR: Ability to enable heavy hair neural network
* Error message when trying to load an old effect (from 0.x versions)
* Ruler (distance to face) effect
* Introduce `evalJs` for calling effect methods from the application
* iOS: Support of hair segmentation in landscape mode
* Ability to combine Face AR effects with virtual background in runtime
* Eval js support for OEP

**Changed**

* New Tflite lips neural network (all platforms except iOS and MacOS)
* WebAR: Optimized Image processing
* Remove unnecessary libraries and dependencies
* iOS, MacOS: Switch face tracking neural network to Tflite
* Android: Updated hair segmentation neural network
* New body segmentation (v2) neural network is enabled by default

**Fixed**

* WebAR: Fixed Emscripten auto GC
* WebAR: Added ability to release WASM memory
* WebAR: Fixed Photo editing
* WebAR: Hand segmentation and gestures support
* WebAR: Fixed Next.js compatibility
* Remove unneeded iteration for hair recolor
* The second call of BNBUtilityManager.initialize or BanubaSdkManager.inialize causes crash in the release
* Eyes segmentation nn perf incorrect display
* Makeup API: Fixed Hair coloring algorithm
* Various OEP fixes
* Imgui display on Windows
* Effects fix for Safari 15

### \[1.1.1] - 2021-10-19

**Added**

* Makeup API: Beauty morphings

**Changed**

* Makeup API: Blur algorithm

**Fixed**

* callJsMethod fails when pass parameters

### \[0.38.4] - 2021-11-02

**Fixed**

* `full_image_from_yuv_i420_img` is too slow

### \[0.38.3] - 2021-10-07

**Added**

* `face_search_mode` in the EffectPlayer API
* Windows: Sign and add description to EffectPlayer dlls
* i420 yuv pixel format support

**Changed**

* Improved face tracking performance
* New tflite hair segmentation neural network for Android and Windows

**Fixed**

* Morphings behaviour at the screen edges

### \[0.38.2] - 2021-09-16

**Added**

* iOS 15 support

### \[1.1.0] - 2021-09-30

Version 1.1.0 also includes all changes from SDK v0.x releases up to v0.38 version.

**Added**

* Makeup API support
* Action Units Multi-face support
* Full Body Segmentation v2 neural network (for all platforms)
* Windows: Added description to dlls
* Windows: Sign Banuba SDK dlls
* Face triggers support (mouth open, smile, etc.)
* iOS: Effect info UI in SDK Demo app
* iOS 15 support
* Api.isMirroring()
* WebAR: Distance to phone support

**Changed**

* Android: Updated lips segmentation neural network
* Skin segmentation neural network support on all platforms (including Web)

**Fixed**

* nn\_api Lips aliasing
* WebAR: iOS 13 does not show video stream

### \[0.38.1] - 2021-08-17

**Added**

* C API documentation + deadlock fixes (Windows)

### \[0.38.0] - 2021-08-16

**Added**

* Windows: MSMF camera usage
* iOS, Android: Hand gestures tracking

**Changed**

* Android: Use tflite GPU info lib to range devices classes
* iOS: Use the same background segmentation neural networks for all devices
* iOS: Remove unneeded UI from demo app
* Renamed License utils symbols

**Fixed**

* tflite\_runner assorted fixes
* iOS: White eye lashed when making photo
* iOS: Time range issues in video player
* MacOS: Crash on M1
* CubemapEverest test effect autorotation
* WebAR: broken SIMD support
* WebAR: Fixed creation of MediaStreamCapture
* Android: Multitouch crash in demo app
* Unity: min version of Android SDK
* Unity: Android build on Windows
* Win32: Background NN work
* Incorrect lips shine work

### \[0.37.1] - 2021-07-27

**Added**

* Android x86\_64 preliminary support

**Changed**

* Android: Common gradle for SDK Demo projects
* Updated background segmentation neural network models for Web and Desktop platforms

**Fixed**

* iOS: Missing image from camera when using ARKit on iPhone 12
* Android: Crash on C API
* Android: Missing photos in gallery when using Demo app on some Android devices

### \[0.37.0] - 2021-07-09

**Added**

* New Eyes segmentation neural network with separate detection of eye parts: pupil, sclera, iris (all platforms)
* Token updates for Eye bags and Acne features (**new token required**)
* iOS: Lips corrector
* MacOS: reworked implementation of macOS framework
* WebAR: API to set the number of faces to track
* Unity: Action Units interface
* Abitilty to show camera frames during effect initialization
* M1 support (including simulators)
* Accepting YUV i420
* Lips morphing effect
* Ability to set Neck smoothing from JS (in the effect)
* Effect Player C API

**Changed**

* Update win tflite x64, x86 from 2.3 to 2.4.1
* Eyes corrector included in release archives by default
* Eyes corrector enabled for win and web
* Preload all Android NN classes instead of creating on request
* Improved performance of the Lips Shine effect
* Makeup API updates:
  * SetInitialRotation method is added to bg-image and bg-video classes
  * Transparent BG fix
  * Consistent methods naming
  * Fixed usage of the skin segmentation with background features
* Android: Remove unneeded rotateBg calls and all related code
* iOS: Include bitcode into minimal builds
* iOS: Updated background segmentation NNs for high-end and low-end devices
* Updated Face tracking neural network (all platforms)

**Fixed**

* Makeup Transfer exception
* WebAR: Fixed inactive tab video throttling
* Standalone: remove legacy resources copy
* Effects with video texture crash on some devices with MediaTek + PowerVR
* OEP long loading during app initialization

### \[1.0.0] - 2021-06-22

**Added**

* WebAR: Video textures support
* WebAR: API to set the number of faces to track
* WebAR: Lips effects support on iOS (Safari)
* Xcode 12.5 support

**Changed**

* Examples apps optimized for SDK v1.x

**Fixed**

* Android: Screen is flashing when switching effects
* Android: GPU-specific deadlock issues
* iOS: Demo app crash on iOS < 13.5
* WebAR: Fixed textures alpha-blending
* Windows: Effect with video has failed to load
* Windows: standalone build failure on x86 platform
* Do not crash app when assert has failed
* JS engine fixes
* Lips shine effect
* Various effects fixes

### \[0.36.1] - 2021-05-24

**Changed**

* WebAR: FrameData is available in WebAR SDK
* Distance to phone improvements

**Fixed**

* Unity: Triggers incorrect work
* Unity: iOS camera initialization

### \[0.36.0] - 2021-05-03

**Added**

* WebAR: Human-readable exception messages
* WebAR: Updated background segmentation
* WebAR: Optional SIMD
* WebAR: Made WebAR SDK SSR compatible
* WebAR: Crop, resize, horizontalFlip support
* Desktop: Updated background segmentation
* Android: Offscreen Effect Player (OEP) example
* iOS: Offscreen Effect Player (OEP) example
* Unity: Face morphing support
* GIF textures support
* Lips segmentation support for Web and Desktop
* Makeup API: Exposed extra APIs
* Hand AR API: Nails segmentation (see more)
* Windows: SDK dlls come signed

**Changed**

* Invalidate texture cache in case of file change
* WebAR: Speed up frames obtaining
* WebAR: Improved memory usage
* WebAR: Throw if effect has zero length
* Mac: build SDK as macOS framework
* iOS: Remove ARKit dependency if ARKit face search is disabled

**Fixed**

* Error logs when loading empty effect
* Android: Region cropping when apply zoom
* WebAR: Prevent playback stop during unsuccessful effect application
* WebAR: Inactive tab throttling
* Makeup API: "black square" on lips with alpha channel
* Unity: UI scaling for Beautification scene
* Crash on effect switching
* Standalone demo app signing

### \[1.0.0-beta] - 2021-04-23

**Added**

* New render engine aka _Scene_
* WebGL 1.0 support (for Safari)
* Metal support

### \[0.35.0] - 2021-02-26

**Added**

* Support non-ASCII symbols in paths
* New Background segmentation neural networks (Desktop)
* New Background segmentation neural networks (Web)
* Hair segmentation support on Windows platform
* WebAR: `Effect.preload` and `Player.applyEffect` will now throw an exception if effect's underlying source is not a .zip archive
* Initial support of Apple M1

**Changed**

* ARKit disabled by default (iOS)
* Strip unnecessary symbols on macOS
* Use only minimum required subset from OpenCV on macOS
* Use TFLite 2.4.1 without Metal delegate on macOS
* API to set animated background in effects dynamically

**Fixed**

* WebAR: Firefox video processing issue
* Android: Orientation fixes
* Android: Sound issues and minor improvements
* Unity: iOS plugin size

### \[0.34.1] - 2021-01-26

**Added**

* Face Ruler for Android platform
* Unity: New Action Units effect with background segmentation

**Changed**

* Distribute EffectPlayer for iOS as xcframework

**Fixed**

* Build with disabled face tracking

### \[0.34.0] - 2021-01-19

**Added**

* WebAR: Background support in landscape
* BG support field in effect\_info
* Android: Java 8+ API desugaring support
* Viewer extra options for processing

**Changed**

* tflite\_runner different delegates support for each feature
* Android: Add static tensorflow lite version
* Enable RGB camera on devices with Snapdragon 625
* Processed images location in Banuba Viewer
* Skin smoothing NN update (iOS)

**Fixed**

* WebAR: ES6 to ES5 transpilation issue
* WebAR: loading of non existing effect
* WebAR: several performance issues
* Hair segmentation: TFLite input copy error
* Prior fixes to work with frx\_meta logic
* Incorrect effects display on Android 10
* Android: Effect size after rotation

### \[0.33.1] - 2020-12-10

**Added**

* Add listener as soon as test\_Ruler or FaceRuler effect is activated

**Changed**

* Enable face recognition neural network for mid-end Android devices

**Fixed**

* `setEffectSize` fix for Android
* Lips shine mask incorrect work with back camera

### \[0.33.0] - 2020-11-30

**Added**

* Display FPS stats in desktop viewer app
* Beauty scene for Unity plugin
* Android: Ability to Override Detected Resolution
* Lips recoloring with glitter effect (also supported in Banuba Viewer)
* Distance to face (ruler feature)

**Changed**

* Updated tflite for windows to 2.3
* Both tflite runners creation on first request
* Text texture enabled by default

**Fixed**

* iOS: incorrect BG work on photo in landscape
* Unity: fix aspect on mobile devices
* Delayed camera start
* Repacking errors
* Front camera flip
* 'Face not found' message after load photo from Gallery
* Added handling of IllegalArgumentException to prevent crashes dependent on surface configuration

### \[0.32.1] - 2020-11-05

**Added**

* Effect activation listener
* Unity: Separate render target for beauty scene for the LUTs

**Changed**

* Decreases CPU load on MacOS

**Fixed**

* Crash during effect preload
* Mesh trembling with fast face tracking
* Unity: Aspect of Background segmentation
* Crash during fast effect switching

### \[0.32.0] - 2020-10-20

**Added**

* New background model
* New WebAR API
* WebAR quickstart Demo app
* WebAR beauty demo app
* Native OSX camera implementation
* Web and Desktop getting started added
* Possibility to customize capture session preset (iOS)
* Desktop apps examples for Win and Mac
* Demo effects without face recognition
* Xcode 12 support

**Changed**

* Eye corrector v2.0: improved stability and performance
* Makeup API improvements
* Use setBackgroundTexture with absolute path
* Face tracking stability and performance optimization
* Update offline face tracking (Android)

**Fixed**

* Crash with bitcode in javascript core
* Separate mask for neck smoothing feature
* Crash with effect reset (Android)
* Missing logs in Viewer Standalone
* Android video player loop
* Memory leak on desktop when using animated textures
* Quickstart example apps fixes
* Unity background fix
* ARKit face detection failure

### \[0.31.0] - 2020-08-27

**Added**

* SDK Features control and repacking with client token and client config
* Minimal SDK archive
* SDK build for MacOS
* Makeup transfer feature
* Photo online processing in Banuba Viewer
* Ability to enable effects and neural networks without face recognizer
* Eye brows segmentation NN
* Neck smoothing neural network
* Set camera FPS mode on Android (fixed/adaptive)
* Represent SDK frames as OpenGL textures (WebRTC for Android)
* New beautification API

**Changed**

* Updated Background Segmentation neural network for standalone builds
* Face recognizer work on full frame
* Landmarks smooth filter
* Updated eyes corrector
* Updated face recognition neural network
* Unity scene works in full screen mode
* OpenCV updated to 4.3.0
* Range android devices hardware class and max resolution for it

**Fixed**

* Unity plane does not update rect
* Video player fix
* Heart rate measurement with neural network face search
* Segmentation neural networks work with arkit
* Unity WebGL build
* Fix Unity failure on Win platform
* Crashes on effect unload
* Correctly handle MRT rendering into background camera texture
* Black screen on devices with ARKit
* Background segmentation on Win x86
* WebAR SDK blocks Backspace key
* Banuba SDK work on devices with iOS 14

### \[0.30.2] - 2020-07-15

**Fixed**

* Second mask freezes on the screen in scene effects

### \[0.30.1] - 2020-07-14

**Added**

* Eyes correction feature

**Changed**

* Hide Boost symbols

**Fixed**

* Asynchrony of sound and video after file import
* iOS: App freezes after background in Editing mode
* Android beauty: Screen is flashing after launch
* Crash on Editing Image
* App crashed in editing mod on iPhone XS Max
* EffectPlayer is not launched from 1st time
* Second face is missed if to use front Camera (with ARKit)

### \[0.30.0] - 2020-06-11

**Added**

* WebAR support for Unity platform
* Background segmentation for Unity platform
* Max Faces support in client token
* Videocall example for iOS
* _Minimal_ configuration of Banuba SDK
* EffectPlayer EffectManager

**Changed**

* EP version has changed to 5.6
* Enable bitcode by default (iOS)

**Fixed**

* Compilation error on Ubuntu
* Body segmentation neural network rotation
* Viewer Standalone build
* MSVC x64 Eigen crash
* App won't throw exception when neural network resources are missing
* Optimized face beautification
* Fix audio session (iOS)
* Bakground segmentation failures (iOS)
* Creepy smile fixes
* Portrait match fixes
* Skin smoothing fixes

### \[0.29.1] - 2020-05-19

**Fixed**

* Crash on Android with neural face recognition

### \[0.29.0] - 2020-04-30

**Added**

* Creepy smile neural network (iOS)
* Manual audio session in BNBEffectPlayer (https://docs.banuba.com/face-ar-sdk/overview/migration\_guides#to-version-029x)
* Skin smoothing neural network (iOS)
* New face recognition and trackig algorithm for offline (Android)

**Changed**

* Banuba Viewer color picker reacts to background and lips neural networks
* Make WebAR SDK ES6 module
* Updated llvm backend for WebAR
* WebAR improvements

**Fixed**

* Lips segmentation on Android HQ photo
* Memset buffer overflow when using Action Units
* Jaw mesh stretching fix in face trackig algorithm

### \[0.28.3] - 2020-04-29

**Added**

* Enabled bitcode in iOS release

**Fixed**

* Portrait match technology

### \[0.28.2] - 2020-04-22

**Added**

* Portrait match technology

### \[0.28.1] - 2020-04-09

**Added**

* Update Effect Player for video calls, support callkit audio session specifics

**Changed**

* Switch to fast face recognition algorithm for weak iOS devices

**Fixed**

* Celebrity match technology fixes
* Crash on Banuba Viewer close

### \[0.28.0] - 2020-03-23

**Added**

* New face recognition and trackig algorithm for realtime (iOS)

**Changed**

* Full Body segmentation can be applied again (iOS)
* Banuba Viewer UI changes
* Adapt Action Units to use new face recognition algorithm (iOS)
* Adapt triggers to use Action Units (iOS)

**Fixed**

* Physics behavior for effects on devices with ARKit (iOS)
* Effects render on low-level Android devices

### \[0.27.2] - 2020-03-12

**Fixed**

* Unity openCV error
* Small recognizer fixes for iOS platform

### \[0.27.1] - 2020-02-27

**Added**

* ARKit multiface support

**Changed**

* Android strong devices list updated

**Fixed**

* Multiface effects render
* Multiface issues
* Crash when processing photo with 2 faces
* Effects render with ARKit on iPhone X

### \[0.27.0] - 2020-02-19

**Added**

* Greatly improved face detection in offline mode (iOS, for photos)
* Objective-C full support
* More examples for iOS and Android
* Improved beauty effect
* Lips shine effect improved
* Ability to choose camera from command line on Desktops

**Changed**

* Persistent OpenGL context on Android (don't recreate it after app goes in background)
* Safely ignore GL errors on Android
* Beauty effect is enabled by default

**Fixed**

* Lips shine effect
* Neural networks behaviour after face was lost

### \[0.26.0] - 2020-01-17

**Added**

* Advanced lips recoloring
* Action Units from ARKit
* x86 support for Windows
* Lazy textures load

**Changed**

* Improve Unity sample effects
* Bokeh effect improved
* Enable beauty by default in sample effects
* Improve acne and bags removal performance
* Hair stands blending perfomance improvement

**Fixed**

* Threads leak on Android
* WebGL FPS stabilization
* Memory issue on Android
* Memory issue on iPhone6+
* Crash during rendering on Adreno 610

### \[0.25.2] - 2020-01-09

**Fixed**

* Camera open error on Android

### \[0.25.1] - 2019-12-31

**Fixed**

* Bundle version in xCode project

### \[0.25.0] - 2019-12-23

**Added**

* Eye bugs removal
* Neural network based acne removal
* Use `ARKit` for face tracking when available
* `dvcam` post-process effect
* Eyes state trigger and ruler features in recognizer API
* API to change sound volume from Java Script
* Option to add effect from external folder in sample application (Android)
* Improve API (SDK for browsers)

**Changed**

* Don't reload effect if there was an error in Java Script

**Fixed**

* Decrease memory pressure while creating multiple `BanubaSdkManager` instances (Android)
* Crash on effects with 3 and more faces
* Improved camera FPS on selected low-end Android devices

### \[0.24.1] - 2019-11-06

**Changed**

* Update documentation with examples of new UI

**Fixed**

* Video recording on Android
* Crash after exit from application
* Memory leak on Android
* Crashes when interacting with Android Demo app

### \[0.24.0] - 2019-11-01

**Added**

* Glasses detection
* Improved stability (aka jittersing) of face tracking
* Extended `Recognizer` API
* Recognition results in Python bindings

**Changed**

* Migration to AndroidX
* New redesigned UI for Banuba SDK Demo AP (Android and iOS)

**Fixed**

* Video textures decoding on Android 10
* Crash while going to background on iOS
* Audio recording speed on Android
* Lag during neural networks initialization
* Various camera fixes for Android

### \[0.23.0] - 2019-10-02

**Added**

* Neural network based approach to detect faces. Quality, detection angles and speed of face detection was improved
* Neural networks support for Windows and Web.
* Unity plugin

**Changed**

* Sync audio and video during recording on Android
* Fast background on iPhone 6 and lower.
* Correct neural networks behavior during device rotations

**Fixed**

* Video textures support (Android 10)
* Crashes on Adreno chipsets
* Stability fixes

### \[0.22.0] - 2019-08-28

**Added**

* Lips coloring API in `Beauty` effect
* Option to switch off face recognition in `config.json`
* Option to set preferred frame-rate on iOS

**Changed**

* Lips segmentation neural network updated (Android)

**Fixed**

* Rendering on Andreno GPUs
* Video texture decoding issue on Android
* Android crash on app coming from background
* Crash on iPhone 5 after video capture

### \[0.21.0] - 2019-08-05

**Added**

* Hair and lips recoloring in "Beauty" effect
* `EffectPlayer` threading model documentation
* SDK features documentation
* API to check if device is compatible with Neural Networks player

**Changed**

* `BanubaSdkManager` can be instantiated more then once (see "Migration Guides").
* Use background mask transform for background separation layer from `config.json`

**Fixed**

* Sample app signing (iOS)
* Rendering bugs after effect switch
* Correct screenshot size on Android
* "End touch" event (iOS)

### \[0.20.2] - 2019-07-24

**Fixed**

* background separation layer from config.json (Android)

### \[0.20.1] - 2019-07-17

**Fixed**

* Fix photo processing with MSAA enabled on Android

### \[0.20.0] - 2019-07-12

**Added**

* Sample ASMR effects
* Render passes
* Rendered frames forwarding as byte arrays (Android)
* Ability to debug JS
* Reset effect cache API call

**Changed**

* Watermark gravity (Android)
* Sample background separation effect blending improved
* Background separation feature respects gyroscope data
* Ignore gyroscope during photo and video processing
* Beauty effect improvements

### \[0.19.1] - 2019-06-24

**Added**

* Color post-processing effect
* Face rect API from face recognition result

**Changed**

* Beauty effect improvements

**Fixed**

* Post-processing effect (when apply to framebuffer)
* Image glitches and crash in photo editing mode (Android)

### \[0.19.0] - 2019-06-17

**Added**

* Bokeh effect example
* Icons cons for sample effects
* New documentation, programming guides added
* Rendering view transformation API
* Post-process library
* Beauty app example

**Changed**

* Removed `Beauty` effect API parameters:
  * eyes\_sharping\_str
  * blur\_bg\_enable
  * blur\_lod
  * remove\_bag\_intensity
  * eyes\_luts
* Renamed `Beauty` effect api parameters:
  * makeup\_tex -> eyebrows\_tex
  * makeup\_alpha -> eyebrows\_alpha
  * eyebrows\_tex -> lashes\_tex
  * eyebrows\_alpha -> lashes\_alpha
* Gravity in effect now respects device orientation
* Remove life-cycle methods from `BanubaSDKManader` on Android
* External texture disabled by default (Android)
* Action Units sample effect updated
* Use only one camera session for all tasks (Android)
* Improved photo processing speed
* Sound Changer is supplied as separate plugin
* Swift 5 support

**Fixed**

* Gracefully handle exceptions on OS X
* Missing and frozen video textures on iOS and Android
* Open GL crashes on Android
* Neural networks overload on Android
* Rendering bugs for Web version
* Stretched camera preview (iOS)

### \[0.18.1] - 2019-05-29

**Added**

* SVG watermark support (Android)
* Proguard rules for banuba\_sdk module (Android)

**Changed**

* `banuba_sdk` now supplied in compiled form
* `BNBFullImageData` can be created from RGB `CVPixelBuffer` with paddings
* Suspend frame processing while taking low res photo (Android)
* Beauty effect: return default parameters after animation
* Restart camera preview session on HR photo (Android)

**Fixed**

* Video texture freeze (Android)
* Crash during render size change

### \[0.18.0] - 2019-05-24

**Added**

* Processing Bitmap and apply current selected effect on it (Android)
* Image editing mode in platform modules (Android)
* Acne removing technology in photo processing
* Watermarks on video (Android)
* Considering device orientation in photo taking
* Ability to setup several listener in EffectPlayer
* Support of Bitmap in FullImageData constructor (Android)
* Universal framework for device and simulator (iOS)

**Changed**

* Added assertions in EffetPlayer life cycle (for video processing)
* Hair segmentation neural network is updated

**Fixed**

* Losing face orientation after android activity restart is fixed
* Physics on multiface effects is working correctly
* App has crashed on 32 bit Androids with enabled neural networks
* ActionUnits improvements

### \[0.17.1] - 2019-04-24

**Fixed**

* Exposure settings (iOS)
* Continuous photo rendering with updated parameters

### \[0.17.0] - 2019-04-18

**Added**

* Continuous photo rendering with updated parameters
* Conversions-free RGB input support
* Image file processing example (iOS)
* Support for landscape frame input
* API to check Android hardware performance

**Changed**

* Documentation improved
* Swift 4.2 support in example app
* Updated lips segmentation neural network
* Improved rendering quality on high-end Android devices

**Fixed**

* Removed duplicate functionality in Android samples
* Correct video orientation (iOS)

### \[0.16.0] - 2019-04-03

**Added**

* Neural networks for Android: lips, skin, hair, eyes iris segmentation; background separation.
* Neural networks rendering for Android.
* Full body segmentation neural network for iOS.
* Release binaries for Windows.
* New post process effects: acid whip, cathode, rave.
* x86\_64 build variant for iOS simulators.
* Face detection in any orientation (Android).

**Changed**

* Camera FPS increased on Huawei devices.
* Video now paused when app is in background.
* Process screenshot or HQ camera option for Android.
* Performance on low-end Android devices.

**Fixed**

* Video textures playback.
* Audio resume after background (Android).
* Launch time on first run (Android).

### \[0.15.0] - 2019-03-14

**Added**

* Action Units and Blend Shapes
* Take high resolution photo with effect, camera switch, video recording (Android)
* Post processing stage with simple effects
* New neural network for eyes segmentation (iOS)
* Multi-touch

**Changed**

* Method to process photo from file readded to API
* Hide eyes if there is no face in test\_Eyes effect
* Binary size reduced for iOS

**Fixed**

* Photo in Landscape mode on iOS
* Animation position on photos
* Acne removal performance on photos
* Sounds after background (Android)

### \[0.14.3] - 2019-02-21

**Fixed**

* Android crash with external texture
* Rendering area size for iOS
* Java documentation

### \[0.14.2] - 2019-02-09

**Fixed**

* Version number in iOS framework

### \[0.14.1] - 2019-02-01

**Added**

* iPad support for Demo app
* Analytics serialization
* New lifecycle: effect is paused before background
* Videoprocessing (desktop only)

**Changed**

* Photo processing optimization
* Android Demo Activity GC optimization

### \[0.14.0] - 2019-01-15

**Added**

* Haptic feedback.

**Changed**

* Client API automatically generated both for Java and Obj-C.
* Documantation reflecting Java and Obj-C classes.

**Fixed**

* Draw state after VAO modification made by external code (Android).
* Sound session restore on iOS.
* FPS degradation on video textures (Android).

### \[0.13.3] - 2019-01-15

**Fixed**

* Audio session configuration (iOS)

### \[0.13.2] - 2019-01-14

**Changed**

* Restore old RFX classifier

### \[0.13.1] - 2019-01-11

**Added**

* Watermarks on video (iOS only)

**Changed**

* Beauty soft light texture without eye shadows

**Fixed**

* Stretched picture during video preview on iOS
* Fix JS call with arguments
* Crashfixes

### \[0.13.0] - 2018-12-27

**Added**

* Ability to modify user's voice (voice changer); iOS only
* Smaller face recognition classifier
* Eyes segmentation textures
* Neural network for face detection (optional, disabled by default)
* Acne removal
* Lips segmentation

**Changed**

* Improved hair segmentation on Android
* BanubaSdkManager improvements on Android

**Fixed**

* FPS calculation,
* Overdraw on Android
* Black screen on Mali devices

### \[0.12.6] - 2018-12-20

**Fixed**

* Reverted unnecessary cropping of video pixel buffer

### \[0.12.5] - 2018-12-19

**Fixed**

* Fix video recording for custom size of input frame

### \[0.12.4] - 2018-12-18

**Added**

* Functions for retriving effect and screen sizes from js

**Fixed**

* Rendering artifacts near eyelid in beauty effect (z-fighting)
* Camera initial mode fix, custom aspect ratio support
* Adjust configuring exposure settings method

### \[0.12.3] - 2018-12-14

**Fixed**

* Fix beautification issues on high resolution
* Fix coordinates conversion in touch event

### \[0.12.2] - 2018-12-12

**Fixed**

* Video recording (copy + flip on BanubaSDK side), memory management improvements

### \[0.12.1] - 2018-12-11

**Changed**

* Turn off frame\_brightness feature by default.
* Enable gyroscope on demand.
* Process image improved **Fixed**
* Exposure point settings (iOS) **Added**
* Effect events for Android
* Touch events for android

### \[0.12.0] - 2018-12-04

**Changed**

* EffectPlayer life cycle methods updated
* Strict checks of surface lifecycle
* Face detection algorithm reverted to more stable implementation
* Resource finding path changed to subfolder (bnb)
* Naming banuba.core -> banuba.sdk (iOS)
* VideoRecording via TextureCache (iOS)

**Added**

* Search locations in ResourceManager error message
* Ability to setup log level and subscribe to SDK's log callback from client code
* Methods for getting CPU Info on Android
* Experimental neural network support on Android (background separation, hair segmentation) (special build is required)
* Bin record interface in BanubaCore
* Improved error reporting while effect loading
* Beautification effect added to resources (special build is required)
* Process single image method with custom input and output formats (ability to take high-quality photos)
* Experimental skin segmentation NN added on iOS
* Experimental eyes segmentation NN added on iOS
* Ability to flip rendered image along the Y axis
* Touch events on iOS

**Fixed**

* Fix pushFrameYVU420 method
* Fix crash in effect\_context::update (race condition)
* Return draw error when effect loading failed
* Bokeh effect works on Android,
* Fix slow wireframe in DebugRenderer
* Fix iOS crash in shader compilation
* Fix unpack alignment for textures with `width * components` not multiple of 4
* Fix process image when external camera texture
* Fix bg copy MRT on ANGLE WebGL (Web)
* Fix depth test\&write state after morph with hair compacting
* Fix min and max possible coordinates (in face recognition)
* Fix exposure point

### \[0.11.2] - 2018-11-20

**Fixed**

* Drawing artifacts on some effects

### \[0.11.1] - 2018-11-15

**Changed**

* Updated face recognition algorithm.

**Added**

* Ability to link with simulator on iOS.

**Fixed**

* Release number for frameworks fixed
* Fix runtime crash with aligned new on iOS 10
* Correctly stop Effect Player in onDestroy and initialization in onCreate

### \[0.11.0] - 2018-11-08

**Added**

* Sound volume control in effect.
* Callback to receive events from effects (mainly for analytics).
* Support for Bokeh effect.

**Changed**

* New face model classifier.
* Rendering performance optimization.

**Fixed**

* Various crashes

### \[0.10.2] - 2018-10-08

**Fixed**

* Issues with effects display (black background instead of camera texture).
* Dynamic shadow lag by one frame.

### \[0.10.1] - 2018-10-05

**Fixed**

* Face recognition black mask in effects has fixed on some Android devices.

### \[0.10.0] - 2018-10-05

**Added**

* Support of new pixel formats in effect\_player::process\_frame: RGBA, BGRA, ARGB, RGB, BGR. Not supported in BanubaCore yet.
* Binding EffectPlayer and Recognizer for Python.

**Fixed**

* Launch on iOS 10.
* Issue with audio engine lifecycle.
* Render: issue with effect's shadows has been fixed.
* Render: issue with depth buffer on Xiaomi Redmi 4a has been fixed.

**Changed**

* Render optimization:
  * Excess loading of 1x1 textures for background and hair masks was removed when these features are not used.
  * Color correction for easysnap (lut-textures background loading — speeds up beauty effect loading and small speed up of lut layer rendering).
  * Broken effects fixes.

### \[0.9.1] - 2018-10-02

**Fixed**

* Dynamic shadows drawing issue has been fixed (for Banuba 3.0).

**Changed**

* EffectPlayer for Backend major version was raised to 5.0.
* Render performance optimization.
* Beauty Effect for both platforms should be taken from 2b959fa12a966956c6f158ded762b634eac988de or later (update Android effect).

### \[0.9.0] - 2018-09-28

**Fixed**

* A few crashes in face recognition engine were fixed.
* Issue with mask does not respect head volume after switching the effects has been fixed.

**Changed**

* Render performance optimization.

### \[0.8.6] - 2018-09-24

**Added**

* Android version assembled with NDK 18.

**Changed**

* Face recognition improved performance, improved anti-tremble, smoothing and so on.

### \[0.8.5] - 2018-09-21

**Fixed**

* Fixed initialization crash.

### \[0.8.4] - 2018-09-21

**Added**

* Debug render antialiasing.

**Changed**

* Beautification effect performance has increased.
* Face recognition performance has increased.

### \[0.8.3] - 2018-09-21

**Changed**

* Binary file size was reduced for iOS (17.7 MB against 19.7 MB).

### \[0.8.2] - 2018-09-19

**Fixed**

* Issues with single frame processing were fixed.

**Changed**

* Performance has improved.

### \[0.8.1] - 2018-09-14

**Added**

* Minor render optimizations (excess glGetInteger were removed).

**Changed**

* Low-light feature has been reverted because it has issues.

### \[0.8.0] - 2018-09-12

**Added**

* New audio player.
* Callback on low light detection.

**Changed**

* Improvements in face recognition lib (performance in multiface mode has been increased, recognition angles has been increased, predictability of recognition work time has been improved — detection distribution by frames with self scheduler.
* Improvements in render performance (number of passed parameters into shader interpolation were decreased — pixel shaders patch in glfx).
* More accurate draw of the camera image (NEAREST filtration).

### \[0.7.2] - 2018-09-11

**Fixed**

* Issues with `effect_player_wrap-ios.framework` were fixed.

### \[0.7.1] - 2018-09-07

**Fixed**

* Fixed issue with crash in v0.7.0 release.

### \[0.7.0] - 2018-09-05

**Added**

* Photo mode frame processing (high resolution frame processing).
* Consistency mode for camera external texture (Android).
* Ability to get the version of EffectPlayer from backend.
* Ability to get the number of rendered frame and pass number in push\_frame.
* Face recognition finds face at a large angle (up to 30 degrees).
* Ability to set the texture parameters through suffixes in their names.
* Framework version is transferred to Manifest after building, AAR assembling completely automated (Andorid).

**Fixed**

* Fixed issue with context lose on Android.
* Effects with occlusion are fixed.
* Small bug fixes.

**Changed**

* Strong reference on Delegate has been removed in iOS.

### \[0.6.2] - 2018-08-31

**Fixed**

* Fixed deadlock when drawing regular camera texture.

### \[0.6.1] - 2018-08-29

**Added**

* Consistent external texture for Android.
* Zeroing face counter on onStop event.

### \[0.6.0] - 2018-08-21

**Fixed**

* Fixed and significantly improved inconsistency modes (was given earlier in unversioned release).
* Images strides from the camera were fixed for Android.
* Fixed issue with long camera initialization.

**Changed**

* Default iOS mode was changed to inconsistency-without-face (was given earlier in unversioned release).
* Updates in gender recognition (works fast and once in 3 seconds at the moment).

### \[0.5.2] - 2018-07-31

**Added**

* Possibility to enable inconsistency mode on iOS, it is possible to skip frame processing to render the image.
* Possibility to receive device orientation in script (it is possible to disable background separation according to orientation).
* Possibility to create a few recognizer instances (basically for DiffCat, not yet presented in EP API).
* Possibility to transmit both camera matrix into the script (needed for morphing creation in accordance to distance from camera).
* Recognizer coverage with performance tests has started.

**Fixed**

* Potential crash with keeping color\_plane was fixed.
* Fixed wrong\_fb\_after\_morph.

### \[0.5.1] - 2018-07-26

**Fixed**

* Beauty settings doesn’t apply issue has been fixed.

**Changed**

* Unnecessary Android resources were removed.

### \[0.5.0] - 2018-07-24

**Added**

* Consistency/inconsistency modes switching (Android).
* Blur background.
* Performance collection using systrace (Android).
* 32-bit support (but slow at the moment).
* Possibility to transfer frame number which has come from camera.
* Possibility to disabled background separation and other recognizer features from scripts.
* Switching between external texture and drawing from ImageReader (Android).

**Fixed**

* Huawei issues (Android).
* Colors conversion bug fix (color correction).

**Changed**

* Optimized morphing.
