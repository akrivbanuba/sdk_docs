# Banuba Face AR SDK Overview

### Introduction to Face AR SDK

Welcome to Banuba Face AR SDK. This document will help you to get started with our SDK and guide you on how to create your project with Face AR features.

How to read this Documentation:

1. **View the samples.** The SDK is delivered with examples of feature applications for each platform. They cover a variety of real-life use cases and give a comprehensive overview of how to run and use the SDK.
2. **Setup your project** using our examples.

### Architecture of Face AR SDK

The image below shows the components of the Banuba Face AR SDK.

![](.gitbook/assets/introduction\_0.svg)

#### EffectPlayer

EffectPlayer is a low-level library for effects' playing. The code of the library is cross-platform and doesn't depend on the platform-specific APIs and compilers.

EffectPlayer is written in C++, but has bindings to all supported platform-specific languages and run-times.\
You need to use Java or Kotlin on Android, and Objective-C or Swift on iOS for dealing with this API.

EffectPlayer features:

* Consumes the camera frames and requests for the frame drawing. Serves it in an asynchronous manner using multithreading if available on a platform.
* Runs all recognition operations on the input frames.
* Runs and manages all platform-specific modules encapsulated in C++. For example audio playback, video playback, accelerometer, haptic and vibration engines, scripting engine, etc.
* Implements all logic of loading and playing interactive effects (loading from disk, rendering, scripting of effect logic, etc).

#### Platform modules

The functionality of the platform modules depends on a specific platform. Generally, it includes:

* camera features (permission management, configuration, life cycle implementation)
* effect's rendering context setup
* video recording
* high-resolution photo taking
* preparing of EffectPlayer's resources on the app's launch

The source code of the platform modules is included in SDK's distribution archive. You can modify the code and adapt the SDK up to your use case if its default functionality is not enough.

#### Mobile C++ interfaces

Besides bindings to Objective-C and Java we provide native C++ interfaces for iOS and Android. These interfaces are exposed by the same binary libraries and provided on a general basis with every release. We don't recommend using C++ API for mobile platforms unless you have a strong reason for this.

API documentation is available [here](pathname:///generated/doxygen/html/index.html) with samples for [iOS](https://github.com/Banuba/quickstart-ios-cpp) and [Android](https://github.com/Banuba/quickstart-android-cpp).

### More info

* Visit our getting started page for more information about SDK integration and examples of Demo apps.
* Have questions about Face AR SDK? Visit [FAQ page](https://www.banuba.com/faq/).
* Can't find an answer? Contact our support.
