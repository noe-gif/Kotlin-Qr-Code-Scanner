<h1 align="center">Kotlin QR code analyzer</h1></br>

<p align="center">
📱 This project is a native android app that analyzes a qr code and displays it's content
</p>
<br>

![Banner](https://cdn.discordapp.com/attachments/774360587391860769/1105186000944246915/kotlin.png)

## Stats

![](https://img.shields.io/tokei/lines/noe-gif/Dating-app-React-Native?color=orange&label=Total%20Lines&logo=kotlin&logoColor=white)
[![](https://img.shields.io/github/downloads/noe-gif/Dating-app-React-Native/total?color=orange&label=Total%20Downloads%20(GitHub)&logo=github&logoColor=white)](https://tooomm.github.io/github-release-stats/?username=noe-gif&repository=Dating-app-React-Native)
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fnoe-gif%2FDating-app-React-Native&count_bg=%239A3DC8&title_bg=%23555555&icon=tencentweibo.svg&icon_color=%23E7E7E7&title=Total+Visits&edge_flat=false)](https://hits.seeyoufarm.com)
[![Release](https://img.shields.io/github/v/release/noe-gif/Dating-app-React-Native?color=52be80&label=Release)](https://github.com/noe-gif/Dating-app-React-Native/releases)
![](https://img.shields.io/github/languages/count/noe-gif/Dating-app-React-Native?color=white&label=Languages)
![](https://img.shields.io/github/license/noe-gif/Dating-app-React-Native?color=red&label=License)
![](https://img.shields.io/badge/Minimum%20SDK-23%20(Marshmallow)-839192?logo=android&logoColor=white)
![](https://img.shields.io/badge/Target%20SDK-30%20(Android%2011)-566573?logo=android&logoColor=white)
[![Crowdin](https://badges.crowdin.net/inure/localized.svg)](https://crowdin.com/project/inure)

# QR code scanner

User interface and experience

<p align="center">
<img src="assets/presentation.gif" alt="androiddevnotes logo"></img>
</p>

## Installation

Add below dependancy in application build.gradle
```gradle
dependencies {
        // Activity Compose
    implementation "androidx.activity:activity-compose:1.4.0"

    // CameraX
    implementation "androidx.camera:camera-camera2:1.0.2"
    implementation "androidx.camera:camera-lifecycle:1.0.2"
    implementation "androidx.camera:camera-view:1.0.0-alpha31"

    // Zxing
    implementation 'com.google.zxing:core:3.3.3' 
}
```
Also include the following required permission in your manifest.
```xml
<!--permission to get camera access-->
<uses-permission android:name="android.permission.CAMERA" />
```
Implements  analyze in activity

Add following method to create Qr code analyzing method
```kotlin
/**
* Analyzes Qr code and decrypt it
*/
    override fun analyze(image: ImageProxy) {
        if(image.format in supporterImageFormats) {
            val bytes = image.planes.first().buffer.toByteArray()
            val source = PlanarYUVLuminanceSource(
                bytes,
                image.width,
                image.height,
                0,
                0,
                image.width,
                image.height,
                false
            )
            val binaryBmp = BinaryBitmap(HybridBinarizer(source))
            try {
                val result = MultiFormatReader().apply {
                    setHints(
                        mapOf(
                            DecodeHintType.POSSIBLE_FORMATS to arrayListOf(
                                BarcodeFormat.QR_CODE
                            )
                        )
                    )
                }.decode(binaryBmp)
                onQrCodeScanned(result.text)
            } catch(e: Exception) {
                e.printStackTrace()
            } finally {
                image.close()
            }
        }
    }

```

## Project Structure

```bash
qrCodeAnalyzer-kotlin/
├── app/                        # This folder contains the main application logic and components.
| ├── src/                      # This folder contains the source code for the app.
| | ├── main/                   # This folder contains the main logic of the app.
| | | ├── java/                 # This folder contains the Java source code.
| | | | └── com/                # This folder contains the package for the app.
| | | | └── qrcodeanalyzer/     # This folder contains the main activity and components for the app.
| | | ├── res/                  # This folder contains the resource files for the app such as images, layouts and strings.
| | | └── AndroidManifest.xml   # This file contains metadata about the app, including the app name, version, and permissions.
├── build.gradle                # This file contains the configuration for the Gradle build system.
├── gradle/                     # This folder contains the Gradle wrapper files.
| └── wrapper/                  # This folder contains the Gradle wrapper files.
| ├── gradle-wrapper.jar        # This file contains the Gradle wrapper executable.
| └── gradle-wrapper.properties # This file contains the Gradle wrapper configuration.
├── gradlew                     # This file contains the Gradle wrapper executable for Unix-based systems.
├── gradlew.bat                 # This file contains the Gradle wrapper executable for Windows-based systems.
├── local.properties            # This file contains the local configuration for the project, such as the path to the Android SDK.
├── settings.gradle             # This file contains the settings for the Gradle build system.
├── proguard-rules.pro          # This file contains the configuration for the ProGuard obfuscator.
├── app.iml                     # This file contains metadata about the project, including the project name, version, and dependencies.
├── .idea/                      # This folder contains the IntelliJ IDEA project files.
```

## License

**MBTFY** Copyright © 2023 - Noé Campo

**MBTFY** could be released as open source software under
the [GPL v3](https://opensource.org/licenses/gpl-3.0.html)
license, see the [LICENSE](./LICENSE) file in the project root for the full license text.

[react-navigation]: https://reactnavigation.org/docs/getting-started/
[moti]: https://moti.fyi/
[react-content-loader]: https://www.npmjs.com/package/react-content-loader
[gesture-handler]: https://www.npmjs.com/package/react-native-gesture-handler
[linear-gradient]: https://github.com/react-native-linear-gradient/react-native-linear-gradient
[reanimated]: https://docs.swmansion.com/react-native-reanimated/
[redash]: https://www.npmjs.com/package/redash
[safe-area-context]: https://www.npmjs.com/package/react-native-safe-area-context
[native-screens]: https://www.npmjs.com/package/react-native-screens
[native-splash-screen]: https://www.npmjs.com/package/react-native-splash-screen
[native-svg]: https://www.npmjs.com/package/react-native-svg


[tutorial]: assets/presentation.gif
