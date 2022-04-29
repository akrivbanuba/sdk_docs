# How to get Landmarks in iOS

The landmarks are anchor points that show the relative position and shape of the main elements of the face. Banuba SDK provides coordinates of the landmarks. To get this information, you need to follow these steps.

### Getting information about the landmarks in your iOS app

1.  Import `BanubaEffectPlayer` framework into your project.

    ```swift
    import BanubaEffectPlayer
    ```
2.  Add `BNBFrameDataListener` to your ViewController

    ```swift
    sdkManager.effectPlayer?.add(self as BNBFrameDataListener)
    ```

    :::note Remove `BNBFrameDataListener` when your ViewController is deinited

    ```swift
    sdkManager.effectPlayer?.remove(self as BNBFrameDataListener)
    ```

    :::
3.  Inherit interface BNBFrameDataListener and add protocol stubs

    ```swift
    extension ViewController: BNBFrameDataListener {
        func onFrameDataProcessed(_ frameData: BNBFrameData?) {

        }
    }
    ```
4. From BNBFrameData you can get information about coordinates of the landmarks. The function `getLandmarks()` returns an array of NSNumber with size of 2 \* (landmarks number). The first value responds to the X coord of the first landmark and the second value responds to the Y coord of the first landmark and so on.

At first, this coordinates will be in the FRX (Camera) system, but you can transform them to the Screen system. You can find more inforamtion about coordinates transforamtion [here](https://docs.banuba.com/face-ar-sdk/core/transformations) You must set the variables `screenWidth` and `screenHeight` to the width and height of your screen beforehead.

After transformation you can get an array of points in the Screen coordinates in correspondence with the landmarks. In this example it is the `landmarksPoints` array.

```swift
extension ViewController: BNBFrameDataListener {
    func onFrameDataProcessed(_ frameData: BNBFrameData?) {

        guard let fD = frameData else { return }

        let recognitionResult = fD.getFrxRecognitionResult()
        let faces = recognitionResult?.getFaces()
        let landmarksCoordinates = faces?[0].getLandmarks()

        guard let landmarks = landmarksCoordinates else { return }

        if landmarks.count != 0 {
             // get transformation from FRX (Camera) coordinates to Screen coordinates
             let screenRect = BNBPixelRect(x:0, y:0, w:screenWidth, h:screenHeight)
             guard let frxResultTransformation = recognitionResult?.getTransform(),
             let commonToFrxResult = BNBTransformation.makeData(frxResultTransformation.basisTransform),
             let commonRect = commonToFrxResult.inverseJ()?.transform(frxResultTransformation.fullRoi),
             let commonToScreen = BNBTransformation.makeRects(commonRect,
                                                              targetRect: screenRect,
                                                              rot: BNBRotation.deg0, flipX: false, flipY: false),
             let FrxResultToCommon = commonToFrxResult.inverseJ(),
             let frxResultToScreen = FrxResultToCommon.chainRight(commonToScreen)  else { return }

             //create points from transformed coordinates
             var landmarksPoints: [CGPoint] = []
             for i in 0 ..< (landmarks.count / 2) {
                 let xCoord = Float(truncating: landmarks[i * 2])
                 let yCoord = Float(truncating: landmarks[i * 2 + 1])
                 let pointBeforeTransformation = BNBPoint2d(x: xCoord, y: yCoord)

                 let pointAfterTransformation = frxResultToScreen.transformPoint(pointBeforeTransformation)
                 landmarksPoints.append(CGPoint(x: CGFloat(pointAfterTransformation.x),
                                                y: CGFloat(pointAfterTransformation.y)))
             }
        }
    }
}
```

1. Now you can use the landmarks info in your iOS app. For example, you can display them like in the picture below.
