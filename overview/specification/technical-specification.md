# Technical Specification

{\` table { font-size: 14px; } \`}

This page provides technical metrics of Face AR SDK feature performance. The values below are for your reference only. We received them on fixed conditions. However, many factors may influence the actual technology performance, e.g. the state of device, other apps running, wi-fi enabled, room temperature, etc. We encourage you to test each feature within your environment.

Please visit SDK Features and SDK Features for Unity for the information regarding features support on different platforms.

:::note

* **FPS** — Frames per second of the face detection algorithm on a given device.
* **Angles** — Maximum angle on which the technology was able to work during the measurement.
* **Distance** — Maximum distance on which the technology was able to work during the measurement.
* **Real-time (online)** — Technology performance in real-time.
* **Photo (offline)** — The processing time needed to take a photo or process it from the gallery. :::

### SDK Features

#### Face Detection

**Android**

|                | <p>Android Mid<br>Samsung Galaxy S7</p> | <p>Android Top<br>Pixel 3 XL</p> |
| -------------- | --------------------------------------- | -------------------------------- |
| FPS            | 30                                      | 30                               |
| Angles, degree | 70                                      | 70                               |
| Distance, cm   | 120                                     | 120                              |

**iOS**

|                | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| -------------- | -------------------------- | --------------------------- |
| FPS            | 30                         | 60                          |
| Angles, degree | 70                         | 70                          |
| Distance, cm   | 120                        | 120                         |

#### Single-face Tracking

**Android**

|                | <p>Android Mid<br>Samsung Galaxy S7</p> | <p>Android Top<br>Pixel 3 XL</p> |
| -------------- | --------------------------------------- | -------------------------------- |
| FPS            | 30                                      | 30                               |
| Angles, degree | 70                                      | 70                               |
| Distance, cm   | 180                                     | 200                              |

**iOS**

|                | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| -------------- | -------------------------- | --------------------------- |
| FPS            | 30                         | 60                          |
| Angles, degree | 70                         | 70                          |
| Distance, cm   | 180                        | 200                         |

#### Multi-face Tracking

**Android**

|              | <p>Android Mid<br>Samsung Galaxy S7</p> | <p>Android Top<br>Pixel 3 XL</p> |
| ------------ | --------------------------------------- | -------------------------------- |
| Faces Number | 3                                       | 3                                |
| 2 Faces, FPS | 20                                      | 30                               |
| 3 Faces, FPS | 20                                      | 30                               |

**iOS**

|              | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ------------ | -------------------------- | --------------------------- |
| Faces Number | 3                          | 3                           |
| 2 Faces, FPS | 30                         | 60                          |
| 3 Faces, FPS | 30                         | 60                          |

Faces Number\* — Maximum number of faces which SDK can track with acceptable quality and performance on most mobile devices. The actual number allowed for multi-face tracking is not limited by the technology but only by the physical ability of the device and proportions of the screen.

### Effect performance

Banuba SDK allows for a variety of Face AR effects. Some of them require only face tracking and can be represented as a single 3D mask with textures and materials. Other effects are implemented with separately trained neural networks.

Below, you may find information on the real-time performance of Face AR effects which require only face tracking, i.e. face filters, avatars with action units, beautification, and makeup filter (without lipstick).

**Android**

|     | <p>Android Mid<br>Samsung Galaxy S7</p> | <p>Android Top<br>Pixel 3 XL</p> |
| --- | --------------------------------------- | -------------------------------- |
| FPS | 30                                      | 30                               |

**iOS**

|     | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| --- | -------------------------- | --------------------------- |
| FPS | 30                         | 60                          |

### Beautification

#### Beautification filter

Basic face beautification filter includes skin smoothing, morphing, teeth whitening, eyes flare and LUT. It requires only face tracking, so please, refer to the [Effects performance](broken-reference) section. Other features given below are based on neural networks, and their performance differs.

#### Acne removal (manual)

**iOS only**, neural network, photo processing (offline only)

|            | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ---------- | -------------------------- | --------------------------- |
| Photo, sec | 1                          | < 1                         |

#### Acne removal (auto)

**iOS only**, neural network, photo processing (offline only)

|            | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ---------- | -------------------------- | --------------------------- |
| Photo, sec | < 2                        | < 1                         |

#### Eye bag removal

**iOS only**, neural network, photo processing (offline only)

|            | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ---------- | -------------------------- | --------------------------- |
| Photo, sec | < 2                        | < 1                         |

#### Skin smoothing

**iOS only**, neural network, photo processing (offline only)

|            | <p>iOS Top<br>iPhone 11</p> |
| ---------- | --------------------------- |
| Photo, sec | < 1                         |

#### Neck beautification

**iOS only**, neural network, photo processing (offline only)

|            | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ---------- | -------------------------- | --------------------------- |
| Photo, sec | 1                          | < 1                         |

### Makeup

The Makeup filter allows for a realistic try on of foundation, eyeshadow, eyeliner, highlighter, contour, and blusher. It requires only face tracking, so please, refer to the [Effects performance](broken-reference) section. The lipstick try on requires lips segmentation neural network with a separate algorithm for Lips Shine effect.

#### Lips coloring

**Android**

|                | <p>Android Mid<br>Huawei P30 Lite</p> | <p>Android Top<br>Samsung Galaxy S10+</p> |
| -------------- | ------------------------------------- | ----------------------------------------- |
| Real-time, FPS | 23                                    | 30                                        |
| Photo, sec     | < 3                                   | < 2                                       |

**iOS**

|                | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| -------------- | -------------------------- | --------------------------- |
| Real-time, FPS | 30                         | 80                          |
| Photo, sec     | < 1                        | < 1                         |

**Web**

|        | Real-time, FPS |
| ------ | -------------- |
| Chrome | 30             |
| Safari | 12             |

#### Lips Shine (Glossy lipstick)

**Android**

|                | <p>Android Mid<br>Huawei P30 Lite</p> | <p>Android Top<br>Samsung Galaxy S10+</p> |
| -------------- | ------------------------------------- | ----------------------------------------- |
| Real-time, FPS | 18                                    | 30                                        |
| Photo, sec     | 3                                     | 2                                         |

**iOS**

|                | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| -------------- | -------------------------- | --------------------------- |
| Real-time, FPS | 30                         | 60                          |
| Photo, sec     | < 1                        | < 1                         |

**Web**

|        | Real-time, FPS |
| ------ | -------------- |
| Chrome | 18             |
| Safari | 12             |

### Background separation

**Android**

|               | <p>Android Mid<br>Samsung Galaxy S7</p> | <p>Android Top<br>Pixel 3 XL</p> |
| ------------- | --------------------------------------- | -------------------------------- |
| Real-time,FPS | 20                                      | 30                               |
| Photo, sec    | < 3                                     | < 3                              |

**iOS**

|                | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| -------------- | -------------------------- | --------------------------- |
| Real-time, FPS | 30                         | 60                          |
| Photo, sec     | < 1                        | < 1                         |

#### Distance

| Device                  | Distance, cm                                |
| ----------------------- | ------------------------------------------- |
| iPhone XR               | <p>Portrait 160 cm,<br>Landscape 195 cm</p> |
| iPhone 8 Plus           | <p>Portrait 175 cm,<br>Landscape 180 cm</p> |
| Huawei Mate 20 Pro      | <p>Portrait 175 cm,<br>Landscape 225 cm</p> |
| MacBook Pro (13", 2017) | 180 cm                                      |

#### Image formats support

Currently, the following images formats are supported as background texture:

* `.jpeg`
* `.jpg`
* `.png`
* `.ktx`
* `.gif`

#### Video formats support

Used as part of animated background.

| Video format | MacOS | iOS | Android | Windows |
| ------------ | ----- | --- | ------- | ------- |
| .mp4         | ✅     | ✅   | ✅       | ✅       |
| .avi         | ✅     | ❌   | ✅       | ✅       |
| .flv         | ✅     | ❌   | ❌       | ✅       |
| .mkv         | ✅     | ❌   | ✅       | ✅       |
| .mov         | ✅     | ✅   | ✅       | ✅       |
| .mts         | ✅     | ❌   | ❌       | ✅       |
| .webm        | ✅     | ❌   | ✅       | ✅       |
| .wmv         | ✅     | ❌   | ✅       | ✅       |

### Hair segmentation

#### Hair Recoloring

**Android**

|               | <p>Android Mid<br>Samsung Galaxy S7</p> | <p>Android Top<br>Pixel 3 XL</p> |
| ------------- | --------------------------------------- | -------------------------------- |
| Real-time,FPS | 20                                      | 30                               |
| Photo, sec    | < 3                                     | < 2                              |

**iOS**

|               | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ------------- | -------------------------- | --------------------------- |
| Real-time,FPS | 30                         | 60                          |
| Photo, sec    | < 1                        | < 1                         |

#### Hair Strands Recoloring

**iOS only**, works for photo processing (offline only)

|            | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ---------- | -------------------------- | --------------------------- |
| Photo, sec | < 2                        | < 1                         |

### Skin segmentation

**Android**

|               | <p>Android Mid<br>Samsung Galaxy S7</p> | <p>Android Top<br>Pixel 3 XL</p> |
| ------------- | --------------------------------------- | -------------------------------- |
| Real-time,FPS | 20                                      | 30                               |
| Photo, sec    | < 3                                     | < 2                              |

**iOS**

|               | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ------------- | -------------------------- | --------------------------- |
| Real-time,FPS | 30                         | 60                          |
| Photo, sec    | < 1                        | < 1                         |

### Eyes recoloring

**Android**

|               | <p>Android Mid<br>Samsung Galaxy S7</p> | <p>Android Top<br>Pixel 3 XL</p> |
| ------------- | --------------------------------------- | -------------------------------- |
| Real-time,FPS | 20                                      | 30                               |
| Photo, sec    | < 3                                     | < 3                              |

**iOS**

|               | <p>iOS Mid<br>iPhone 7</p> | <p>iOS Top<br>iPhone 11</p> |
| ------------- | -------------------------- | --------------------------- |
| Real-time,FPS | 30                         | 60                          |
| Photo, sec    | < 1                        | < 1                         |

### Hand gestures

**Basic information**

* Supported gestures:
  * Palm ✋
  * Victory✌️
  * Rock 🤘
  * Like 👍
  * Ok 👌
* Maximum distance — 1.1m

**iOS**

| Device    | Realtime FPS\* |
| --------- | -------------- |
| iPhone 11 | 54             |
| iPhone 7  | 41             |
| iphone 6s | 25             |

\* Means technology FPS. In real usage, FPS is usually limited with the render value and locked by 30 or 60 FPS.

**Android**

| Device            | Realtime FPS\* |
| ----------------- | -------------- |
| top-end Huawei    | 30             |
| middle-end Xiaomi | 25             |

\* Means technology FPS. In real usage, FPS is usually limited with the render value and locked by 30 or 60 FPS.

### Full Body segmentation

**iOS**

|                      | iPhone 7 | iPhone 11 |
| -------------------- | -------- | --------- |
| Real-time, FPS\*     | 30       | 60        |
| Photo, sec           | < 1      | < 1       |
| Activation time, sec | \~2      | \~1       |
| Memory usage, mb     | 135      | 170       |

\* Means technology FPS. In real usage, FPS is usually limited with the render value and locked by 30 or 60 FPS.
