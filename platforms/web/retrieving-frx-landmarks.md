# Retrieving FRX landmarks

It is possible to retrieve face landmarks from the face recognition performed by SDK:

```ts
player.addEventListener(Player.FRAME_DATA_EVENT, ({ detail: fd }) => {
  const frx = fd.getFrxRecognitionResult()
  const face0 = frx?.getFaces().get(0)

  const landmarksArray = []
  const landmarksVector = face0?.getLandmarks()

  if (landmarksVector)
    for (let i = 0, len = landmarksVector.size(); i < len; ++i)
      landmarksArray.push(landmarksVector.get(i))

  console.log(landmarksArray)
})
```

The landmarks array stores flattened pairs of 68 points in form of `[x1, y1, x2, y2, ... , x68, y68]`:

:::note Pay attention that an effect with Face Recognition must be applied to the player to get [FrxRecognitionResult](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1frx\_\_recognition\_\_result.html) from the `FrameData.getFrxRecognitionResult()` method. `FrameData.getFrxRecognitionResult()` returns `null` if Face Recognition is not enabled in the effect applied. :::

See the [frame\_data](pathname:///generated/doxygen/html/classbnb\_1\_1interfaces\_1\_1frame\_\_data.html) C++ docs for more details on the FrameData properties and methods.

See the [FRAME\_DATA\_EVENT](pathname:///generated/typedoc/classes/Player.html#FRAME\_DATA\_EVENT) docs for more examples.
