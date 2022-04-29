# How to get Landmarks in Android

The landmarks are anchor points that show the relative position and shape of the main elements of the face. Banuba SDK provides the coordinates of the landmarks. To get this information, you need to follow these steps.

### Getting information about the landmarks in your Android app

1.  Import the following files into your project

    ```java
    import com.banuba.sdk.effect_player.FrameDataListener;
    import com.banuba.sdk.manager.BanubaSdkManager;
    import com.banuba.sdk.types.FrxRecognitionResult;
    import com.banuba.sdk.types.TransformableEvent;
    import com.banuba.sdk.types.Transformation;
    import com.banuba.sdk.types.FrameData;
    import com.banuba.sdk.types.FaceData;
    import com.banuba.sdk.types.PixelRect;
    import com.banuba.sdk.types.Point2d;
    import com.banuba.sdk.types.Rotation;
    ```
2.  Add `FrameDataListener` to your `ViewController`

    ```java
    mySdkManager.getEffectPlayer().addFrameDataListener(this);
    ```

    :::note Remove the `FrameDataListener` when your `ViewController` will be destroyed

    ```java
    mySdkManager.getEffectPlayer().removeFrameDataListener(this);
    ```

    :::
3.  Inherit the `FrameDataListener` interface and override the `onFrameDataProcessed(...)` function

    ```java
    public class ViewController implements FrameDataListener {
        @Override
        public void onFrameDataProcessed(@Nullable FrameData frameData) {
            ...
        }
    }
    ```
4. From FrameData you can get the information about coordinates of the landmarks. The function `getLandmarks()` returns an array of `ArrayList<Float>` with a size of 2 \* (landmarks number). The first value corresponds to the X coord of the first landmark and the second value corresponds to the Y coord of the first landmark and so on.

At first, these coordinates are in the FRX camera space but you can transform them into the screen space. You can find more inforamtion about coordinates transformation [here](https://docs.banuba.com/face-ar-sdk/core/transformations) You must set the variables `mScreenWidth` and `mScreenHeight` to the width and height of your screen beforehand.

After transformation, you can get an array of points in the Screen coordinates in correspondence with the landmarks. In this example it is the `mLandmarksPoints` array.

````
```java
public class ViewController implements FrameDataListener {
    public int mScreenWidth = 720;   /* input screen width */
    public int mScreenHeight = 1280; /* input screen height */
    /* note: mLandmarksPoints - the variable is updated each frame in asynchronous mode.
    * To access it from another thread, required to add synchronization. */
    public ArrayList<Point2d> mLandmarksPoints = null;  /* output landmarks points */

    @Override
    public void onFrameDataProcessed(@Nullable FrameData frameData) {
        if (frameData == null) {
            return;
        }

        FrxRecognitionResult recognitionResult = frameData.getFrxRecognitionResult();
        if (recognitionResult == null) {
            return;
        }

        ArrayList<FaceData> faces = recognitionResult.getFaces();
        if (faces.isEmpty()) {
            return;
        }

        /* note: The example only uses first face data, but SDK allows to recognize
        * and receive data from several faces. For more details you can see:
        * https://docs.banuba.com/face-ar-sdk-v1/overview/glossary#2-faces-detection-multi-face */
        ArrayList<Float> landmarks = faces.get(0).getLandmarks();
        if (landmarks.isEmpty()) {
            return;
        }

        /* Create transformation for landmarks */
        PixelRect screenRect = new PixelRect(0, 0, mScreenWidth, mScreenHeight);
        TransformableEvent frxResultTransformation = recognitionResult.getTransform();
        Transformation commonToFrxResult = Transformation.makeData(frxResultTransformation.getBasisTransform());
        PixelRect commonRect = commonToFrxResult.inverseJ().transformRect(frxResultTransformation.getFullRoi());
        Transformation commonToScreen = Transformation.makeRects(commonRect, screenRect, Rotation.DEG_0, false, false);
        Transformation frxResultToCommon = commonToFrxResult.inverseJ();
        Transformation frxResultToScreen = frxResultToCommon.chainRight(commonToScreen);

        /* Create points from transformed coordinates */
        mLandmarksPoints = new ArrayList<Point2d>();
        int countPoints = landmarks.size() / 2;
        for (int i = 0; i < landmarks.size() / 2; i += 2) {
            Point2d pointBeforeTransformation = new Point2d(landmarks.get(i) /* x coord */, landmarks.get(i + 1) /* y coord */);
            Point2d pointAfterTransformation = frxResultToScreen.transformPoint(pointBeforeTransformation);
            mLandmarksPoints.add(pointBeforeTransformation);
        }
    }
}
```
````

6\. Now you can use the landmarks info in your Android app. For example, you can display them like in the picture below.
