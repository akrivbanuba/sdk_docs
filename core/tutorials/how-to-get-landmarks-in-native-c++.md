# How to get Landmarks in Native C++

The landmarks are anchor points that show the relative position and shape of the main elements of the face. Banuba SDK provides the coordinates of the landmarks. To get this information, you need to follow these steps.

### Getting information about the landmarks in your C++ app

1.  Import the following files into your project

    ```cpp
    #include <bnb/effect_player/interfaces/all.hpp>
    #include <bnb/recognizer/interfaces/all.hpp>
    #include <bnb/types/interfaces/all.hpp>
    ```
2.  Add `landmarks_holder` to your `effect_player`

    ```cpp
    /* note: m_landmarksHolder - is of type std::shared_ptr<interfaces::frame_data_listener>
    * Must be created before calling this method. */
    my_effectPlayer->add_frame_data_listener(m_landmarksHolder);
    ```

    :::note Remove the `landmarks_holder` when your `effect_player` will be destroyed

    ```cpp
    my_effectPlayer->remove_frame_data_listener(m_landmarksHolder);
    ```

    :::
3.  Inherit the `frame_data_listener` interface and override the `on_frame_data_processed(...)` method

    ```cpp
    class landmarks_holder : public frame_data_listener
    {
        void on_frame_data_processed(const std::shared_ptr<::bnb::interfaces::frame_data> & frameData)
        {
            ...
        }
    };
    ```
4.  From `frame_data` you can get the information about coordinates of the landmarks. The function `get_landmarks()` returns an array of `std::vector<float>` with a size of 2 \* (landmarks number). The first value corresponds to the X coord of the first landmark and the second value corresponds to the Y coord of the first landmark and so on.

    At first, these coordinates are in the FRX camera space but you can transform them into the screen space. You can find more inforamtion about coordinates transformation [here](https://docs.banuba.com/face-ar-sdk/core/transformations). You must set the variables `m_screenWidth` and `m_screenHeight` to the width and height of your screen beforehand.

    After transformation, you can get an array of points in the Screen coordinates in correspondence with the landmarks. In this example it is the `m_landmarksPoints` array.

    ```cpp
    class landmarks_holder : public frame_data_listener
    {
        void on_frame_data_processed(const std::shared_ptr<::bnb::interfaces::frame_data> & frameData)
        {
            if (frameData == nullptr) {
                return;
            }

            auto recognitionResult = frameData->get_frx_recognition_result();
            if (recognitionResult == nullptr) {
                return;
            }

            auto faces = recognitionResult->get_faces();
            if (faces.empty()) {
                return;
            }

            /* note: The example only uses first face data, but SDK allows to recognize
            * and receive data from several faces. For more details you can see:
            * https://docs.banuba.com/face-ar-sdk-v1/overview/glossary#2-faces-detection-multi-face */
            auto landmarks = faces[0]->get_landmarks();
            if (landmarks.empty()) {
                return;
            }

            /* Create transformation for landmarks */
            using ns = bnb::interfaces;
            ns::pixel_rect screenRect(0, 0, m_screenWidth, m_screenHeight);
            auto frxResultTransformation = recognitionResult->get_transform();
            auto commonToFrxResult = ns::transformation::make_data(frxResultTransformation.basis_transform);
            auto commonRect = commonToFrxResult->inverse_j()->transform_rect(frxResultTransformation.full_roi);
            auto commonToScreen = ns::transformation::make_rects(commonRect, screenRect, ns::rotation::deg_0, false, false);
            auto frxResultToCommon = commonToFrxResult->inverse_j();
            auto frxResultToScreen = frxResultToCommon->chain_right(commonToScreen);

            /* Create points from transformed coordinates */
            m_landmarksPoints.clear();
            for (int i = 0; i < landmarks.size(); i += 2) {
                auto pointBeforeTransformation = ns::point2d(landmarks[i] /* x coord */, landmarks[i + 1] /* y coord */);
                auto pointAfterTransformation = frxResultToScreen->transform_point(pointBeforeTransformation);
                m_landmarksPoints.push_back(pointAfterTransformation);
            }
        }

    public:
        int32_t m_screenWidth {1280}; /* input screen width */
        int32_t m_screenHeight {720}; /* input screen height */
        /* note: m_landmarksPoints - the variable is updated each frame in asynchronous mode.
        * To access it from another thread, required to add synchronization. */
        std::vector<bnb::interfaces::point2d> m_landmarksPoints; /* output landmarks points */
    };
    ```
5. Now you can use the landmarks info in your C++ app. For example, you can display them like in the picture below.
