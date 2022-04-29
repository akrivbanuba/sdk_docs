# Banuba SDK Web AR Optimization tutorials

### Optimizing WebAR SDK bundle size

Banuba WebAR SDK is [tree-shakable](https://developer.mozilla.org/en-US/docs/Glossary/Tree\_shaking), so simply import only those modules your application relies on:

```ts
// the named import saves extra KBs
import { Webcam, Player, Effect, Dom } from "/path/to/BanubaSDK.js"

// ...
```

### Optimizing WebAR SDK assets size

`BanubaSDK.data` and `BanubaSDK.wasm` are heavy ones. But they have a good compressability due to the internal format of the files.

| Asset               | Original | Gzip  | Brotli |
| ------------------- | -------- | ----- | ------ |
| BanubaSDK.data      | 13Mb     | 11Mb  | 11Mb   |
| BanubaSDK.wasm      | 12Mb     | 3.5Mb | 2.5Mb  |
| BanubaSDK.simd.wasm | 13Mb     | 3.8Mb | 2.7Mb  |

Most hosting environments like [Netlify](https://www.netlify.com) automatically pre compress the files, but sometimes you may have to compress them yourself for better downloading times. You can run the command in the assets folder to get them compressed:

```
npx gzipper compress --brotli .
```

See [gzipper docs](https://www.npmjs.com/package/gzipper#compressc-1) for details.

### Speed up WebAR SDK for modern browsers

Banuba WebAR SDK ships with the `BanubaSDK.simd.wasm` file - the SIMD version of the `BanubaSDK.wasm`. Without digging into the details of what SIMD is, the SIMD enabled file can boost the processing performance up to several times. Taking into consideration that SIMD has [a good support across modern browsers](https://webassembly.org/roadmap/) you should definitely give it a try.

SIMD support detection is built into the WebAR SDK. It means the SDK will try to load `BanubaSDK.simd.wasm` if the current browser supports SIMD and will load `BanubaSDK.wasm` otherwise.

Don't forget to point BanubaSDK to the SIMD file location if you are using `locateFile`:

```ts
const player = await Player.create({
  clientToken: "xxx-xxx-xxx",
  // point BanubaSDK where to find these vital files
  locateFile: {
    "BanubaSDK.data": "/path/to/BanubaSDK.data",
    "BanubaSDK.wasm": "/path/to/BanubaSDK.wasm",
    "BanubaSDK.simd.wasm": "/path/to/BanubaSDK.simd.wasm",
  },
})
```

See [Player.create()](pathname:///generated/typedoc/classes/Player.html#create) and [locateFile](pathname:///generated/typedoc/modules.html#SDKOptions) for details.

### Reducing CPU/GPU usage on HiDPI devices

On HiDPI devices Banuba WebAR SDK scales the output frames by the [device pixel ratio](https://developer.mozilla.org/en-US/docs/Web/API/Window/devicePixelRatio). This approach allows SDK to render face masks in a high quality and keep all the mask details.

Despite the better rendering quality this approach utilizes more CPU and GPU resources since the frame size to be processed scales geometrically.

One can simply opt out from the default behavior and reduce CPU/GPU utilization by overriding the `devicePixelRatio` used by the SDK:

```ts
const player = await Player.create({
  clientToken: "xxx-xxx-xxx",
  devicePixelRatio: 1,
})
```

See the [PlayerOptions](pathname:///generated/typedoc/modules.html#PlayerOptions) of the [Player.create()](pathname:///generated/typedoc/classes/Player.html#create) method for more details.

The CPU and GPU usage can be reduced even more by processing frames of smaller size, e.g the 640x480 webcam frame size can be used instead of the default 1280x720 frame size:

```ts
player.use(new Webcam({ width: 640, height: 480 }))
```

Check out the Video cropping tutorial for more details.

### Preloading Effects

Sometimes you may experience a time lag between [player.applyEffect()](pathname:///generated/typedoc/classes/Player.html#applyEffect) call and a visual change due to the long time of the effect archive download.

To speed up things, you can preload the Effect and apply it later on demand:

```ts
const preloaded = await Effect.preload("SomeBigEffect.zip"))

// ...

player.applyEffect(preloaded)
```

You can also scale the approach and add a local cache of the preloaded effects, or preload an effect on some user interaction like mouse hover a button.
