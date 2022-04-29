# FaceAR Glossary

### AR Technologies

#### FRX (Face tracking)

The technology to detect and track the presence of a human face in a digital video frame to enable FaceAR camera experiences.

Background separation

Neural network that separates a user on the foreground from the background in a sequence of video frames to remove the background or replace it with another image. As a standalone feature, the background segmentation is used in video conferencing, live streaming and video communication apps. It also can be used as part of face filter together with facial animation in entertainment apps.

Bokeh effect

The algorithm that separates a person on the foreground and blurs the background as in photography.

#### Skin segmentation

Neural network trained to recognize and segment the skin area for recoloring tasks, e.g. make the skin tone lighter or darker.

Skin smoothing

Neural network trained to segment and blur the skin on the face to create a retouch effect similar to professional photography.

#### Neck smoothing

Neural network trained to segment and blur the neck area for beautification purposes.

#### Hair Segmentation

Neural network to detect and segment the image into hair, face and background to allow for real-time hair modification such as change the hair color.

Eye segmentation

Neural network to detect and segment the eye into iris, pupil and eyeball for eye recoloring and virtual contact lens try on.

Lips segmentation

Neural network to detect and segment the lips on the users face for virtual lipstic try on effect.

Full body segmentation

Neural network trained to recognize the human body in full length and separate it from the background in images and videos.

#### Acne removal (tap)

Acne removal is an algorithm to remove acne in photos by single taps on the selected area.

#### Acne removal (auto)

The algorithm to automatically remove acne in photos.

#### Eye bag removal

The algorithm segments and lightens the area under the eyes in photos for beautification purposes.

#### Hair strands painting

The algorithms to change the hair color with several colors applied simultaneously, e.g. for strands highlight or coloring.

### Features

#### 2+ faces detection (Multi-face)

Algorithm allowing for masks application to several people simultaneously for more engaging group AR experiences. For the quality user experience, we generally don’t recommend supporting more than 3 faces on mobile devices due to limited computing capabilities.

#### Pulse (Heart rate)

Algorithm analyses fine patterns of the facial areas and their color variations within time to detect pulse frequency in real-time.

#### Ruler (Distance to phone)

Algorithm analyses face area size to estimate distance from user's face to camera in real-time.

#### Text Texture (on mask)

Allows to write text as texture on any 2D or 3D model in the effect..

#### Mask on a picture from Camera Roll

Mask application on pre-recorded images the user uploads from the Camera Roll.

#### Mask on video from Camera Roll

Mask application on pre-recorded videos the user uploads from the Camera Roll.

#### Post-processing effects

Graphical camera effects and animations applied on pre-recorded videos.

#### Continuous photo editing

AR effect is processed in real-time on the image. E.g. beautification slider to control the face modification or "Before/After" slider.

#### Touches

Small AR scenarios enabled thought the user touches on the screen. AR objects or camera effects can change color and behaviour. Applied in FaceAR games or interactive face filters to increase engagement.

#### Trigger

Small AR scenarios enabled through user facial expressions. The user can interact with effects or call them opening mouth, smiling, raising eyebrows or frowning. Applied in FaceAR games or interactive face filters to increase engagement.

SFX

Sound effects support in FaceAR experiences, e.g. add music to filters.

#### Voice changer

The 3rd party software allowing to change the tone of the user's voice, e.g. make the user talk like a robot, kid, male/female, etc.

#### Glasses detection

The algorithm detects if the user wears glasses and removes them in a virtual mask. Applied in glasses try-on for convenient frame choice and face filters for AR glasses would not overlay the real glasses.

### Graphical technologies

#### Face beautification

The AR filter based on face tracking which automatically retouches the appearance applying skin smooth, morphing, eye makeup, teeth whitening, eye flare and LUT effect.

Morphing

Changing the size and proportions of the face, e.g. slim down the cheeks, nose or modify them for fun masks.

Skinned mesh animation

AR models look not static but moving, animated and transforming.

Physically-based rendering

AR models behave like the real objects in the flow of real-world light and physics, e.g. support gravity or mirror the light with the camera rotates and user tilts.

LUT post-processing

Real-time or offline color correction of pre-recorded images, e.g. Instagram-like filters.

#### Texture sequences

The digital representation of the surface of an AR object providing the sophisticated and life-like object representation.

#### Video textures

Infuse a static image with dynamic qualities and explicit action to achieve an enhanced look and feel of the FaceAR video experience.

Action units

The fundamental actions of individual muscles or groups of muscles of the face that enable the AR mask to support user facial expressions, e.g. in emojis, avatars or full-face AR masks.
