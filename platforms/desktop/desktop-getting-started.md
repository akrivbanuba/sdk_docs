# Desktop Getting Started

### Requirements

* Latest stable xCode on MacOS
* Latest stable Microsoft Visual Studio on Windows

### Get the client token and configuration file

To start working with the Banuba SDK in your project, you need to have the client token. To receive the client token please fill in our [form on banuba.com](https://www.banuba.com/face-filters-sdk) website, or contact us via [info@banuba.com](mailto:info@banuba.com).

### Get the Banuba SDK archive

With the client token, you will also receive the Banuba SDK archive for desktop which contains:

* `bnb_sdk` folder with dynamic libs and include files,
* `third` folder with third-party libraries,
* `resources` folder

### Build your project with Banuba SDK on Windows

1. Copy `bnb_sdk` folder from your SDK archive to your project.
2.  Configure your project to use Banuba SDK:

    1. Open Project `Properties` -> `Linker` -> `Input` and add `additional dependencies`: `bnb_effect_player.lib`.
    2. Open Project `Properties` -> `Linker` -> `General` and add `additional library directories` for each build configuration: `bnb_sdk/bin/{platform}/{configuration}`.&#x20;
    3. Open Project `Properties` -> `VC++ Directories` and add `include directories`: `bnb_sdk/include`.&#x20;

    :::note You need to copy `bnb_effect_player.dll` to the `build` directory. You may do this by using a post-build action in your project or just copying manually. \<img className="shadow--md" style=\{{ width: "446px" \}} src={require("@site/static/img/desktop/win/build\_sdk\_dlls.png").default} />\
    :::
3. You will also need third-party libraries to run your project with Banuba SDK. You will find them in the `third` folder in your SDK archive. Copy the `third` folder to your project.
4.  When you need one of these libraries just configure your project to use this library like at the 2nd point.

    1. For example, you will need to use the `glad` library. Add `glad` include directories to your project.
    2. You also need to copy `third/openal` and `third/ffmpeg` dlls to the `build` directory.

    \<img className="shadow--md" style=\{{ width: "440px" \}} src={require("@site/static/img/desktop/win/build\_additional\_dlls.png").default} />
5. Now you can run your project with Banuba SDK.

### Build your project with Banuba SDK on MacOS

1. Copy the `bnb_sdk` folder from your SDK archive to your project.
2. Configure your project to use Banuba SDK (if you need debug version, replace `release` with `debug` in the paths):
   1. Open Project `General` -> `Framework, Libraries, and Embedded Content` and add BanubaEffectPlayer.framework (path to framework: `bnb_sdk` -> `mac` -> `release`)
   2. Open Project `Build Settings` -> `Search Paths` -> `Header Search Paths` and add path to headers: `${SRCROOT}/bnb_sdk/mac/release/BanubaEffectPlayer.framework/Versions/A/Headers`&#x20;
3. You will also need third-party libraries to run your project with Banuba SDK. You will find them in the `third` folder in your SDK archive. Copy the `third` folder to your project.
4. When you need one of these libraries just configure your project to use this library like at the 2nd point.
   1. For example, you will need to use the `glad` library. Add `glad` include directories to your project.
5. Now, you can run your project with release version of Banuba SDK.
