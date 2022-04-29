# Banuba SDK Web AR Getting Started

### Requirements

* The [latest](broken-reference) Banuba SDK Web AR release
* Banuba [client token](broken-reference)
* An AR [effect](https://github.com/Banuba/quickstart-web/blob/master/effects/Hipster3.zip)
* [Nodejs](https://nodejs.org/en/) installed
* Browser with support of [WebGL 2.0](https://caniuse.com/#feat=webgl2)

#### Obtaining Banuba SDK Web AR

To get the latest Banuba SDK Web AR release please fill in the [form on banuba.com](https://www.banuba.com/facear-sdk/face-filters#form) website, or contact us via [info@banuba.com](mailto:info@banuba.com).

#### Obtaining Banuba Client token

Banuba Client token is required to get Banuba SDK Web AR working.

Generally it's delivered with Banuba SDK Web AR archive.

To receive a new **trial** client token please fill in the [form on banuba.com](https://www.banuba.com/facear-sdk/face-filters#form) website, or contact us via [info@banuba.com](mailto:info@banuba.com).

### Usage

The obtained Banuba SDK Web AR archive contains a simple demo app with several effects.

Unzip the archive. Check the unarchived folder and find there the `index.html` file. Put the Banuba Client token into the `index.html` file:

```js
    // ...
 
    const player = await Player.create({ clientToken: "PUT YOUR CLIENT TOKEN HERE" }) // <- put your Banuba Client token here as the hint suggests

    // ...
```

Run the command in the unarchived folder:

```bash
npx live-server
```

Open [localshot:8080](http://localhost:8080).

:::info You can obtain more effects on the Demo Face Filters page :::

When finished, you can proceed to a more complicated example or to the [Web AR API docs](pathname:///generated/typedoc).
