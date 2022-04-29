# Unity Demo Scene

Since 1.4.0 Banuba SDK provides a new **Demo Scene** for our Unity plugin.

New Demo scene allows using multiple face filters with carousel like in our native Demo application. To launch this Demo scene on your device follow the steps bellow:

1. In the project files tree find BanubaSDKDemo which is located under Assets -> BanubaFaceAR -> Demo
2. Specify the quantity of effects you want to add. Go to BanubaSDKDemo -> EffectsConteiner -> Script and write needed number
3. To add effect pick prefab under Assets -> BanubaFaceAR -> Effects and drop it to empty cell in Effect Manager (Script)
4. Select **LoaderScene** and BanubaSDKDemo in **File** -> **Build Settings** and launch it on the needed platform as usual. If you would like to launch **BanubaSDKDemo** on a mobile platform, add LoaderScene under Assets -> BanubaFaceAR -> Scenes and add **BanubaSDKDemo** to `LoaderScene` Script

That’s how a properly configured scene should look like.
