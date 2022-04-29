# Android Demo app UI

#### Android Demo app UI description



1.  **FPS Counter and active effect** — shows 3 types of FPS in real-time and displays active effect. FPS counters:

    * Camera
    * Face Recognition (FRX)
    * Draw

    **Effect Info** block contains the information about _audio, video, touches_ usage and _render type_ of the effect. Can be enabled by longtap on the FPS counters area.
2. **Frame Logger** — 1st tap starts FPS log recording, 2nd tap ends FPS log recording. FPS log can be found in logcat output.
3. **Gallery** — selection and processing photos from the gallery (continuous photo editing).
4. **Take HQ Photo** — takes a high-quality photo (process image).
5. **Switch camera** — switches the camera between the front and rear views.
6. **Save Dump** — 1st tap starts face recognition data recording, 2nd tap ends face recognition data recording. Recorded dump can be found on device: `/sdcard/Android/data/com.banuba.sdk.demo/cache`.
7. **Photo/Video** — tap to take a low-quality photo in the Photo mode (5), tap and hold to record a video in the Video mode (5).
8. **Switch mode** - switches between the Photo and Video modes. When the Video mode is enabled, you can record videos with control 7.
9. **Effects selection** — the slider control that shows all effects in the app.
10. **Add Effects** — feature that allows to add new effects into Demo App more quickly using _File Manager_.
11. **Enable fixed FPS** — allows to fix FPS by disabling autoexposition setting.

#### How to use Add Effects feature in Banuba SDK Demo app

1. Download a folder with effect via _Android Studio_ to device.
2. Launch Demo App and tap '+' icon.
3. Find the effect(s) downloaded in File Manager.
4. Mark the folder(s) with checkbox and tap 'Select' button.
5. Effect(s) appeared in Demo app right after being added and can be applied.
