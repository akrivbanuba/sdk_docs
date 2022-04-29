# Banuba SDK Web AR Common use-cases

### Customizing video source

You can easily modify the built-in [Webcam](pathname:///generated/typedoc/classes/webcam.html#constructor) module video by passing [parameters](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#properties\_of\_video\_tracks) to it.

#### Switching from front to back camera

For example, you can use back camera of the device by passing [facingMode](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints/facingMode) parameter to it:

```ts
// ...

// The default facingMode value is "user" which means front camera
// The "environment" value here means back camera
player.use(new Webcam({ facingMode: "environment" }))

// ...
```

#### External MediaStream

If the built-in [Webcam](pathname:///generated/typedoc/classes/Webcam.html#constructor) can not fit your needs you can use a custom [MediaStream](pathname:///generated/typedoc/classes/MediaStream.html) with [Player](pathname:///generated/typedoc/classes/Player.html#constructor):

```ts
import { MediaStream /* ... */ } from "/path/to/BanubaSDK.js"

// ...

/* process video from the camera */
const camera = await navigator.mediaDevices.getUserMedia({ audio: true, video: true })
player.use(new MediaStream(camera))

/* or even from another canvas */
const canvas = $("canvas").captureStream()
player.use(new MediaStream(canvas))

// ...
```

See Banuba WebAR SDK [MediaStream](pathname:///generated/typedoc/classes/MediaStream.html) docs for more details.

### Capturing processed video

You can easily capture the processed video, take screenshots, video recordings or pass the captured video to a WebRTC connection.

#### Screenshot

```ts
import { ImageCapture /* ... */ } from "/path/to/BanubaSDK.js"

// ...

const capture = new ImageCapture(player)
const photo = await capture.takePhoto()

// ...
```

See Banuba WebAR SDK [ImageCapture.takePhoto()](pathname:///generated/typedoc/classes/ImageCapture.html#takephoto) docs for more details.

#### Video

```ts
import { VideoRecorder /* ... */ } from "/path/to/BanubaSDK.js"

// ...

const recorder = new VideoRecorder(player)
recorder.start()
await new Promise((r) => setTimeout(r, 5000)) // wait for 5 sec
const video = await recorder.stop()

// ...
```

See Banuba WebAR SDK [VideoRecorder](pathname:///generated/typedoc/classes/VideoRecorder.html) docs for more details.

#### MediaStream

```ts
import { MediaStreamCapture /* ... */ } from "/path/to/BanubaSDK.js"

// ...

// the capture is an instance of window.MediaStream
const capture = new MediaStreamCapture(player)

// so it can be used as a video source
$("video").srcObject = capture

// or can be added to a WebRTC peer connection
const connection = new RTCPeerConnection()
connection.addTrack(capture.getVideoTrack())

// ...
```

See Banuba WebAR SDK [MediaStreamCapture](pathname:///generated/typedoc/classes/MediaStreamCapture.html) docs for more details.

### Video cropping

You can adjust video frame dimensions via [Webcam](pathname:///generated/typedoc/classes/Webcam.html#constructor) constructor parameters:

```ts
const wcam = new Webcam({ width: 320, height: 240 })
```

But this approach is platform dependent and varies between browsers, e.g. some browsers may be unable to produces frames of the requested dimensions and can yield frames of close but different dimensions instead (e.g. 352x288 instead of requested 320x240).

To workaround this platform-specific limitations, you can levered the built-in SDK crop and resize modificators:

```ts
const desiredWidth = 320
const desiredHeight = 240

function resize(frameWidth, frameHeight) {
  const wRatio = desiredWidth / frameWidth
  const hRatio = desiredHeight / frameHeight
  const ratio = Math.max(wRatio, hRatio)

  const resizedWidth = ratio * frameWidth
  const resizedHeight = ratio * frameHeight

  return [resizedWidth, resizedHeight]
}

function crop(renderWidth, renderHeight) {
  const dx = (renderWidth - desiredWidth) / 2
  const dy = (renderHeight - desiredHeight) / 2

  return [dx, dy, desiredWidth, desiredHeight]
}

player.use(webcam, { resize, crop })
```

This way you can get the desired frame size despite the platform used.

See [Player.use()](pathname:///generated/typedoc/classes/player.html#use) and [InputOptions](pathname:///generated/typedoc/modules.html#inputoptions) docs for more datails.

### Postprocessing

It's possible to postprocess the processed by WebAR SDK video.

You can grab the idea from the code-snippet:

```ts
import { MediaStreamCapture /* ... */ } from "/path/to/BanubaSDK.js"

// ...

const capture = document.createElement("video")
capture.autoplay = true
capture.srcObject = new MediaStreamCapture(player)

const canvas = document.getElementById("postprocessed")
const ctx = canvas.getContext("2d")
const fontSize = 48 * window.devicePixelRatio

function postprocess() {
  canvas.width = capture.videoWidth
  canvas.height = capture.videoHeight

  ctx.drawImage(capture, 0, 0)

  ctx.font = `${fontSize}px serif`
  ctx.fillStyle = "red"
  ctx.fillText("A Watermark", 0.5 * fontSize, 1.25 * fontSize)
}

;(function loop() {
  postprocess()
  requestAnimationFrame(loop)
})()
```

See [Capturing processed video](broken-reference) > [MediaStream](broken-reference) for details.
