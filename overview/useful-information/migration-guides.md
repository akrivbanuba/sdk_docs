# Migration Guides

### To version 1.4.1

### iOS

* `EffectPlayerConfiguration` doesn't have constructor with `renderMode` anymore. Use constructor without parameters instead.
* `EffectPlayerConfiguration` doesn't contain auxiliary class `Default` with default values anymore.
* `CameraSessionType` contains only `FrontCameraSession` and `BackCameraSession` values now.

### To version 1.0.x

Starting from version 1.0.x and higher, we provide a new rendering engine. Effects from the previous version _will not work_. Please, contact Banuba to convert your effect for the new engine.

### iOS

* `BanubaSdkMnager.setRenderTarget` now accepts `EffectPlayerView`(for on-screen rendering) or `CAMetalLayer` (for off-screen rendering) instead of `CAEAGLLayer`.
* `EffectPlayerView.effectPlayer` property was made private, don't use it anymore.

### To version 0.30.x

One of the goals of this release was to separate the logic of working with effects. Methods of `EffectPlayer` that were moved to the new `EffectManager` and `Effect` classes:

* `add_error_listener` was moved to the `EffectManager`
* `remove_error_listener` was moved to the `EffectManager`
* `add_hint_listener` was moved to the `EffectManager`
* `remove_hint_listener` was moved to the `EffectManager`
* `add_effect_event_listener` was moved to the `EffectManager`
* `remove_effect_event_listener` was moved to the `EffectManager`
* `set_effect_size` was moved to the `EffectManager`
* `load_effect` was moved to the `EffectManager`
* `unload_effect` was moved to the `EffectManager`
* `force_effect_reload` was removed
* `get_effect_status` was removed
* `call_js_method` was moved to the `Effect`

#### Android

* `BanubaSdkManager.setDrawSize` was removed

### To version 0.29.x

#### iOs

A new `manualAudio` parameter was added to `BNBEffectPlayerConfiguration`. Set it to `true` if you wish to create the audio session manually. Otherwise use `false`.

#### Android

A new `manualAudio` parameter was added to `EffectPlayerConfiguration`. Set it to `true` if you wish to create the audio session manually. Otherwise use `false`.

### To version 0.27.x

#### iOS

We've made BanubaSdk.framework (written in Swift) callable from Objective-C just adding `@objc` attribute to each public function and making classes extend from `NSObject`. In most cases you need nothing to do with your code, but good to mention this change.

### To version 0.21.x

One of the goals of this release was to get rid of singletons both for `BanubaSdkManager` and `EffectPlayer`. Now you can create multiple instances of the classes (however, resources aren't shared yet).

#### Android

* `BanubaSdkManager.createInstance`, `BanubaSdkManager.getInstance` and `BanubaSdkManager.destroyInstance` were removed. Instead intialize SDK with call to `BanubaSdkManager.initialize` and create an instanse of `BanubaSdkManager`.
* `effectsResourcesPaths` argument was removed from BanubaSdkManager construction. Use second argument of `BanubaSdkManager.initialize` instead.
* Whenever you need `BanubaSdkManager`, just create a class field to access it.
* `BanubaSdkTouchListener` requires `EffectPlayer` as an argument in constructor.
* Refer `MainActivity` as an example.

#### iOS

* The `instance` property was removed in `BanubaSdkManager`. Instead intialize SDK with call to `BanubaSdkManager.initialize`, next create and hold a reference to `BanubaSdkManager` in a view controller or an application.
* `voiceChanger`, `outputService` are optional now (to reflect the state of `BanubaSdkManager` while `BNBEffectPlayer` isn't created). Correct nullabity access to these properties.
* Pass a reference to `BNBEffectPlayer` in `EffectPlayerView`.
* Refer `ViewController` as an example.
