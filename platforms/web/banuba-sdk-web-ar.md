# Banuba SDK Web AR

### What is included

Banuba SDK Web AR is delivered as:

* `BanubaSDK.wasm` - low-level high-performance Banuba SDK module compiled to WebAssembly
* `BanubaSDK.data` - face detection neural networks and auxiliary AR data
* `BanubaSDK.js` - a JavaScript wrapper for consuming the WebAssembly module with browser-specific things like WebCamera usage and DOM rendering

### What it can do

`BanubaSDK.js` exports different APIs for Web AR development like _Player_, _Effect_, several types of _Input_ and _Output_.

A generic workflow looks like:

> _Input_ -> _Player_ + _Effect_ -> _Output_

#### Player

The _Player_ allows to consume different data inputs like webcam or image file, to apply an effect on top of it and to produce an output like rendering to DOM node or an image file.

#### Effect

The _Effect_ allows to consume an effect or a face filter as remote or local archive.

#### Input

The _Input_ can be one of:

* Webcam
* Image as Blob or URL
* Video as Blob or URl
* 3rd-party MediaStream (like HTMLVideoElement stream or WebRTC stream)

#### Output

The _Output_ can be one of:

* HTML Element
* Image as Blob
* Video as Blob
* MediaStream that can be used by 3rd-parties (like WebRTC streaming app)

The plenty of input options multiplied by the plenty of output options covers lots of use cases like:

* Photo booth app with realtime webcam video processing and photo capturing
* Photo and video files post-processing app
* P2P video call app with face filter applied

And many more.

### How it looks in JavaScript

Realtime webcam video processing and DOM rendering:

```js
import { Webcam, Player, Effect, Dom } from "./BanubaSDK.js"

const player = await Player({ clientToken: "xxx-xxx-xxx" })

player.use(new Webcam())
player.applyEffect(new Effect("Glasses.zip"))

Dom.render(player, "#webar-app")
```

And with screenshot capturing:

```js
import { Webcam, Player, Effect, Dom, ImageCapture } from "./BanubaSDK.js"

const player = await Player({ clientToken: "xxx-xxx-xxx" })

player.use(new Webcam())
player.applyEffect(new Effect("Glasses.zip"))

Dom.render(player, "#webar-app")

const capture = new ImageCapture(player)
const photo = await capture.takePhoto()
```

:::info Still have any questions about Banuba SDK Web AR? Visit the [Web AR FAQ](https://www.banuba.com/faq/face-ar-sdk#web) or contact support to get helped. :::
