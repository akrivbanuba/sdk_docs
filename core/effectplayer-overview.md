# EffectPlayer Overview

The`EffectPlayer` module is the main interface for all low-level functionality of Banuba SDK. As described in the Introduction page, `EffectPlayer` is responsible for consuming camera frames, running various recognition pipelines on it, sending the recognized data to the effect playback engine, and drawing the final image on the provided OpenGL surface.

:::note For most use cases of Banuba SDK, it's better to use platform-specific APIs and language bindings as described in the Platforms section. The `EffectPlayer` API should be used only for non-trivial cases not covered by Platform APIs. :::

### Overview

To work with the `EffectPlayer` application, you should create an appropriate execution environment. The two most essential components of this environment are the camera and render surface. The camera pushes the image frames to `EffectPlayer`. The render surface creates the OpenGL context with target framebuffer where the final image is rendered.

The camera or any other image source should periodically push the frames into EffectPlayer. Usually, it's done in the dedicated thread called _Camera thread_.

`EffectPlayer` periodically runs pipeline with recognition technologies to retrieve data from an input image. The component with the pipeline is called `Recognizer`, and it runs its work cycle in a dedicated thread incapsulated in `EffectPlayer`. Before recognition, the input images from the camera are placed into `InputBuffer` where they are waiting for the next recognition cycle. During processing a lot of information is attached to the image, e.g. face positions, segmentation masks from neural networks etc. In the end of the recognition process, these data compose the final result of the recognition which is stored in a separate data structure called `FrameData`. The final `FrameData` is placed in `OutputBuffer` from where it is sent to an Effect and drawn to the render surface.

During the drawing cycle `FrameData` is popped from `OutputBuffer` and consumed by the Effect engine. On this stage, the Effect engine executes all effect's logic, e.g. sends all recognized data to the script engine or to the renderer. Drawing cycles are usually initiated from an app or platform modules. The platform module creates a dedicated **Render thread** to manage this task. This module ensures that the OpenGL context and target framebuffer exist during the drawing calls.

### EffectManager

A new class that encapsulates all logic of working with effects. To get an instance of this class, call the method [`effect_manager`](pathname:///generated/doxygen/html/index.html#FIXME) from `EffectPlayer`. Some methods from `EffectPlayer` were moved here. For example instead of `load_effect` in `EffectPlayer` now you have an ability to choose between synchronous and asynchronous implementations ([`load`](pathname:///generated/doxygen/html/index.html#FIXME) and [`load_async`](pathname:///generated/doxygen/html/index.html#FIXME) respectively). You no longer need to worry about the effect status. Once the effect is loaded, it will be applied immediately.

### Effect

This class represents an effect in Banuba SDK. `load` and `load_async` methods from `EffectManager` return a reference to the `Effect` object. You can call `call_js_method` on specific effect.

### Threading model

As descibed in the [Overview](broken-reference) section, `EffectPlayer` expects its methods to be called from the three treads: the UI thread, render thread or camera thread. See the reference of [EffectPlayer](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html) for more details about each method.

:::note It's important to call each method of `EffectPlayer` only from its dediceted thread. Calling methods from the wrong threads can cause unexpected app crashes and halts.\
:::

### Use cases

`EffectPlayer` supports different operational modes:

* offline high-quality processing of an individual images or video frames
* online processing and visualization of real-time camera input

#### Realtime camera preview

The Camera and _Render thread_ work continuously, and the user sees the processed image on the screen in real time. It's the most commonly used operational mode.

To enable this mode, call the following methods:

* [`surface_created`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a4452f3817614bb9c3ac0248a094b5fc9), [`surface_changed`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a4891a5fb2317cc47fe1bfd906eaa614c),
* [`EffectManager::load`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_manager.html#af8a474829ceba669c5b3ce49bd931cc9), [`EffectManager::load_async`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_manager.html#a03747404aad1010af29038e60e118a3d)
* [`Effect::call_js_method`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect.html#a849affbe333d6146dece935b0dd3790f)
* [`playback_play`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a0d78fa8c39926cc5c15fa4132e9fe04e), [`playback_pause`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a0d78fa8c39926cc5c15fa4132e9fe04e)
* in a loop:
  * [`draw`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#ada36c8f13f1d039d6f2f7c362124867a), [`capture_blit`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a8224337c12bb471af9e99a66c8e9b70e), [`read_pixels`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a1e257d4045b841ae7fcc6019a733994f)
  * [`push_frame`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a281d3b5a3f850d53817943b55c8b51be), [`push_frame_with_number`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#aad58b2188250fbe9ac7538f4a2fae341)
* [`playback_stop`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a0d78fa8c39926cc5c15fa4132e9fe04e)
* [`surface_destroyed`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a3b7f8d3f7f4d737eb5acd09c7a2dfe74)

#### Live editing

The user can apply effects to the static photo uploaded from the gallery and see dynamic changes in real time.

* [`surface_created`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a4452f3817614bb9c3ac0248a094b5fc9), [`surface_changed`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a4891a5fb2317cc47fe1bfd906eaa614c),
* [`EffectManager::load`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_manager.html#af8a474829ceba669c5b3ce49bd931cc9), [`EffectManager::load_async`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_manager.html#a03747404aad1010af29038e60e118a3d)
* [`Effect::call_js_method`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect.html#a849affbe333d6146dece935b0dd3790f)
* [`playback_play`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a0d78fa8c39926cc5c15fa4132e9fe04e), [`playback_pause`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a0d78fa8c39926cc5c15fa4132e9fe04e)
* [`start_video_processing`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#aa191bde58ac55beeef0488930152da0a)
* [`process_video_frame`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a2d3bc4de0b5c07eca611fdded1b93a2b)
* [`stop_video_processing`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#ae31aa51b5be4ddebb49933fb73f7232e)
* in a loop:
  * [`draw_with_external_frame_data`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#acd34b041233ff8f3e30db5b5d5f499a2)
* [`playback_stop`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a0d78fa8c39926cc5c15fa4132e9fe04e)
* [`surface_destroyed`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a3b7f8d3f7f4d737eb5acd09c7a2dfe74)

#### Video Processing

The video is processed synchronously frame by frame with results returned as a series of images in system memory.

* [`surface_created`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a4452f3817614bb9c3ac0248a094b5fc9), [`surface_changed`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a4891a5fb2317cc47fe1bfd906eaa614c),
* [`EffectManager::load`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_manager.html#af8a474829ceba669c5b3ce49bd931cc9), [`EffectManager::load_async`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_manager.html#a03747404aad1010af29038e60e118a3d)
* [`Effect::call_js_method`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect.html#a849affbe333d6146dece935b0dd3790f)
* [`start_video_processing`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#aa191bde58ac55beeef0488930152da0a)
* In a loop:
  * [`process_video_frame`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a2d3bc4de0b5c07eca611fdded1b93a2b)
  * [`draw_video_frame`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#ad966e830385004fffa79ec0852c8caa3), [`draw_video_frame_allocated`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a85dc38cc2b1d0f34917c1778b4da98eb)
* [`stop_video_processing`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#ae31aa51b5be4ddebb49933fb73f7232e)
* [`surface_destroyed`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a3b7f8d3f7f4d737eb5acd09c7a2dfe74)

:::note Realtime processing methods can't be used during video processing (`draw`, `push_frame`, etc.). Please, use the methods descibed above. :::

#### Single-image processing

One photo is processed synchronously with results returned as an image in system memory.

* [`surface_created`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a4452f3817614bb9c3ac0248a094b5fc9), [`surface_changed`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a4891a5fb2317cc47fe1bfd906eaa614c),
* [`EffectManager::load`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_manager.html#af8a474829ceba669c5b3ce49bd931cc9), [`EffectManager::load_async`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_manager.html#a03747404aad1010af29038e60e118a3d)
* [`Effect::call_js_method`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect.html#a849affbe333d6146dece935b0dd3790f)
* In a loop (if processing of multiple images is needed):
  * [`process_image`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a759fd0d49789fb558c3519afd7f00e94),
  * [`process_image_data`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a28da1a2f0851da017f0b6ffed7a99766)
* [`surface_destroyed`](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1effect\_\_player.html#a3b7f8d3f7f4d737eb5acd09c7a2dfe74)

:::note The state of face tracking isn't saved between `process_image` calls. The `process_image` method is slow but accurate and not intended for realtime usage.\
:::

:::info Still have any questions about FaceAR SDK? Visit our [FAQ](https://www.banuba.com/faq/) or contact our support. :::
