# Banuba SDK Size

Banuba Face AR SDK contains optional features which you can license separately. The SDK size may differ according to the features used. Below you can find reference information regarding the size of different SDK components.

:::note

* For iOS, the size refers to the raw files on disk. However, in the final .ipa, all components are compressed and consume less memory than on disk.
* For Android, the size refers to already built APK-bundle.
* The size of effects is not included in SDK because you can load effects into your app separately. :::

### SDK components size (iOS)

| Component                                          | Size, mb |
| -------------------------------------------------- | -------- |
| BanubaEffectPlayer binary\*                        | 80       |
| Face Tracking, NN (Neural Network for new devices) | 1.5      |
| Face Tracking (Algorithm for early devices)        | 13.7     |
| Face Detection (online NN, higher performance)     | 2.4      |
| Face Detection (offline NN, higher accuracy)       | 2.3      |

\*Binary contains libraries for different CPU architectures including: iOS x86\_64 (for simulators), ARM64 (for phones) and bitcode. To approximately estimate the final SDK size (in release app) _BanubaEffectPlayer_ binary size should ve divided by 4.

### SDK components size (Android)

See also: Binaries size, Minify app size

| Component                                          | Size, mb |
| -------------------------------------------------- | -------- |
| BanubaEffectPlayer binary (ARMv7)                  | 5.1      |
| BanubaEffectPlayer binary (ARMv8)                  | 6.5      |
| Face Tracking, NN (Neural Network for new devices) | 1.2      |
| Face Tracking (Algorithm for early devices)        | 6.7      |
| Face Detection (online NN, higher performance)\*\* | 2.5      |
| Face Detection (offline NN, higher accuracy)\*\*   | 2.5      |

\*\* Face Detection algorithms with higher performance and higher accuracy used together add 4.1 mb to your SDK package.

### Neural Network size

| Neural Network                                                            | iOS, mb | Android, mb   |
| ------------------------------------------------------------------------- | ------- | ------------- |
| Acne removal                                                              | 2.6     | not supported |
| Eyes bag removal                                                          | 4.2     | not supported |
| Background segmentation (for selfie and landscape)                        | 1.21    | 1.2           |
| Body segmentation                                                         | 0.5     | not supported |
| Eye (iris) segmentation                                                   | 0.7     | 0.22          |
| Hair segmentation                                                         | 0.35    | 0.64          |
| Lips segmentation (including Lips Shine recoloring)                       | 2.3     | 0.5           |
| Face skin segmentation (for skin smoothing effect)                        | 1.2     | not supported |
| Neck segmentation (for neck beautification)                               | 1.2     | not supported |
| Skin segmentation (for skin recoloring)                                   | 1.4     | 0.7           |
| Eyes Corrector (for better eyes tracking when using Neural Face Tracking) | 0.4     | 0.4           |

:::tip Please always keep in mind that the final bundle size with SDK may differ when combining different technologies together. The size also increases when you add face filters directly in your app. :::
