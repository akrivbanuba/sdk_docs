# Upgrade SDK version in your app

In general, the SDK upgrade process is smooth and simple. All you have to do is replace the current EffectPlayer XCFramework with its latest version and consider the information from migration guides.

### Step by step guide for upgrading an SDK in your application

#### Step 1. Get new release archive from your sales manager

A new release may include new features or changes of the already existing versions. In this case, a sales manager will provide you with updated **client token** and **config.json** accordingly.

#### Step 2. Repack your SDK copy

Each new SDK release should be repacked to minify its size and remove unnecessary resources. At the moment, it should be made only for iOS and Android platforms.

#### Step 3. Replace the EffectPlayer XCFramework

Copy the existing EffectPlayer XCFramework and paste it inside your project, replacing the old version of SDK.
