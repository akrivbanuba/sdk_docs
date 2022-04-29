# Banuba SDK Web AR Integration tutorials

Banuba WebAR SDK depends on `BanubaSDK.data` and `BanubaSDK.wasm` (or `BanubaSDK.simd.wasm` if you are targeting SIMD) files. By default the SDK expects these files to be accessible from the application root i.e. by the `/BanubaSDK.data`, `/BanubaSDK.wasm` (`/BanubaSDK.simd.wasm`) links. It must be taken into consideration when working with application bundlers like [Vite](https://vitejs.dev), [Rollup](https://rollupjs.org/guide/en/) or [Webpack](https://webpack.js.org).

Generally speaking one should be able to put `BanubaSDK.data`, `BanubaSDK.wasm` and `BanubaSDK.simd.wasm` files into the application assets folder (usually `public/`) and get BanubaSDK properly loading these files.

But you may want to place the files somewhere else, that case the [locateFile](pathname:///generated/typedoc/modules.html#SDKOptions) property of the [Player.create()](pathname:///generated/typedoc/classes/Player.html#create) method should help you to set-up BanubaSDK properly.

### Bundlers

Ordinary bundlers have no issues with the Banuba WebAR SDK and it should be easy to set up the SDK with them.

#### Vite

```ts
// vite uses special ?url syntax to import files as URLs
import data from "/path/to/BanubaSDK.data?url"
import wasm from "/path/to/BanubaSDK.wasm?url"
import simd from "/path/to/BanubaSDK.simd.wasm?url"
import { Player /* ... */ } from "/path/to/BanubaSDK.js"

// ...

const player = await Player.create({
  clientToken: "xxx-xxx-xxx",
  // point BanubaSDK where to find these vital files
  locateFile: {
    "BanubaSDK.data": data,
    "BanubaSDK.wasm": wasm,
    "BanubaSDK.simd.wasm": simd,
  },
})

// ...
```

See Vite [Explicit URL imports](https://vitejs.dev/guide/assets.html#explicit-url-imports) docs for details.

#### Rollup

```ts
// you need to set-up @rollup/plugin-url for the import syntax to work
import data from "/path/to/BanubaSDK.data"
import wasm from "/path/to/BanubaSDK.wasm"
import simd from "/path/to/BanubaSDK.simd.wasm"
import { Player /* ... */ } from "/path/to/BanubaSDK.js"

// ...

const player = await Player.create({
  clientToken: "xxx-xxx-xxx",
  // point BanubaSDK where to find these vital files
  locateFile: {
    "BanubaSDK.data": data,
    "BanubaSDK.wasm": wasm,
    "BanubaSDK.simd.wasm": simd,
  },
})

// ...
```

See \[@rollup/plugin-url]\(see https://www.npmjs.com/package/@rollup/plugin-url#include) docs for details.

#### Webpack

Depending on the version of Webpack used, you may have to add following rule to the module.rules section of the webpack.config.js:

```ts
module.exports = {
  module: {
    rules: [
      // ...
      {
        test: /\.wasm$/,
        type: 'javascript/auto',
        loader: 'file-loader',
      },
      // ...
    ],
    },
  },
}
```

Now import of `.wasm` files as URLs should work properly:

```ts
import data from "/path/to/BanubaSDK.data"
import wasm from "/path/to/BanubaSDK.wasm"
import simd from "/path/to/BanubaSDK.simd.wasm"
import { Player /* ... */ } from "/path/to/BanubaSDK.js"

// ...

const player = await Player.create({
  clientToken: "xxx-xxx-xxx",
  // point BanubaSDK where to find these vital files
  locateFile: {
    "BanubaSDK.data": data,
    "BanubaSDK.wasm": wasm,
    "BanubaSDK.simd.wasm": simd,
  },
})

// ...
```

See the related [Webpacak issue](https://github.com/webpack/webpack/issues/7352) for details.

### React

Connect Banuba WebAR SDK as any other library:

```ts
import React, { useEffect } from "react"
import data from "/path/to/BanubaSDK.data"
import wasm from "/path/to/BanubaSDK.wasm"
import simd from "/path/to/BanubaSDK.simd.wasm"
import Glasses from "/path/to/Glasses.zip"
import { Webcam, Player, Effect, Dom } from "/path/to/BanubaSDK.js"

export default function WebARComponent() {
  // componentDidMount
  useEffect(() => {
    let webcam

    Player.create({
      clientToken: "xxx-xxx-xxx",
      locateFile: {
        "BanubaSDK.data": data,
        "BanubaSDK.wasm": wasm,
        "BanubaSDK.simd.wasm": simd,
      },
    }).then((player) => {
      player.use(webcam = new Webcam())
      player.applyEffect(new Effect(Glasses))
      Dom.render(player, "#webar")
    })

    // componentWillUnmount
    return () => {
      webcam?.stop()
      Dom.unmount("#webar")
    }
  })

  return <div id="webar"></div>
}
```

See [Bundlers](broken-reference) for notes about specific bundlers and `locateFile` usage.

See [Banuba React demo app](https://github.com/Banuba/quickstart-web-react) for more code examples.

### Real Time Video communication

#### WebRTC

Considering the [Fireship WebRTC demo](https://github.com/fireship-io/webrtc-firebase-demo/blob/main/main.js):

```ts
import {
  MediaStream as BanubaMediaStream,
  Player,
  Effect,
  MediaStreamCapture,
} from "/path/to/BanubaSDK.js"

// ...

webcamButton.onclick = async () => {
  localStream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  remoteStream = new MediaStream()

  const player = await Player.create({ clientToken: "xxx-xxx-xxx" })
  const webar = new MediaStreamCapture(player)

  player.use(new BanubaMediaStream(localStream))
  player.applyEffect(new Effect("BackgroundBlur.zip"))
  player.play()

  // original audio
  const audio = localStream.getAudioTracks()[0]
  // webar processed video
  const video = webar.getVideoTracks()[0]

  localStream = new MediaStream([audio, video])

  // Push tracks from local stream to peer connection
  localStream.getTracks().forEach((track) => {
    pc.addTrack(track, localStream)
  })

  // ...
}
```

See Capturing processed video > [MediaStream](broken-reference) for details.

#### Agora

```ts
import "/path/to/AgoraRTC_N-4.1.0.js"
import { MediaStream, Player, Effect, MediaStreamCapture } from "/path/to/BanubaSDK.js"

// ...

const camera = await navigator.mediaDevices.getUserMedia({ audio: true, video: true })
const player = await Player.create({ clientToken: "xxx-xxx-xxx" })
const webar = new MediaStreamCapture(player)

player.use(new MediaStream(camera))
player.applyEffect(new Effect("BackgroundBlur.zip"))
player.play()

// original audio
const audio = await AgoraRTC.createMicrophoneAudioTrack()
// webar processed video
const video = await AgoraRTC.createCustomVideoTrack({ mediaStreamTrack: webar.getVideoTrack() })

const client = AgoraRTC.createClient({ mode: "live", role: "host", codec: "h264" })
await client.join("AGORA APP ID", "CHANNEL NAME", null)
await client.publish([audio, video])

// ...
```

See [AgoraWebSDK NG API docs](https://agoraio-community.github.io/AgoraWebSDK-NG/api/en/interfaces/iagorartc.html#createcustomvideotrack) for details.

See [Banuba Video call demo app](https://github.com/Banuba/videocall-web) for more code examples.

#### OpenTok (TokBox)

```ts
import "/path/to/OpenTok_v2.js"
import { MediaStream, Player, Effect, MediaStreamCapture } from "/path/to/BanubaSDK.js"

// ...

const camera = await navigator.mediaDevices.getUserMedia({ audio: true, video: true })
const player = await Player.create({ clientToken: "xxx-xxx-xxx" })
const webar = new MediaStreamCapture(player)

player.use(new MediaStream(camera))
player.applyEffect(new Effect("BackgroundBlur.zip"))
player.play()

// original audio
const audio = camera.getAudioTracks()[0]
// webar processed video
const video = webar.getVideoTracks()[0]

const session = OT.initSession("OT API KEY", "OT SESSION ID")
session.connect("OT SESSION TOKEN", async () => {
  const publisher = await OT.initPublisher(
    "publisher",
    {
      insertMode: "append",
      audioSource: audio,
      videoSource: video,
      width: "100%",
      height: "100%",
    },
    () => {},
  )

  session.publish(publisher, () => {})
})

// ...
```

See [TokBox Video API docs](https://tokbox.com/developer/sdks/js/reference/OT.html#initPublisher) for details.

See [Banuba Video call (TokBox) demo app](https://github.com/Banuba/videocall-tokbox-web) for more code examples.
