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
    // it is suppporting ABIs likes armeabi-v7a, arm64-v8a, x86 and x86_64.
    compile 'de.mrmaffen:libvlc-android:2.1.12@aar'    
}
```
Also include the following required permission in your manifest.
```xml
<!--if you want to play server URL-->
<uses-permission android:name="android.permission.INTERNET" />
```
Implements IVLCVout.Callback and MediaPlayer.EventListener in activity or fragment

Include following veriables at class level
```kotlin
// declare media player object
private var mediaPlayer: MediaPlayer?=null
// declare surface view object
var mSurface: SurfaceView?=null
// declare surface holder object
var holder: SurfaceHolder?= null
// declare libvlc object
private var libvlc: LibVLC?=null
```
Add following method to create player to play provided URL
```kotlin
/**
* Creates MediaPlayer and plays video
* @param media
*/
fun createPlayer(media: String) {
  if(mediaPlayer!=null && libvlc!=null){
      releasePlayer()
  }
  Log.i(TAG, "Creating vlc player")
  try {
      // create arraylist to assign option to create libvlc object
      val options = ArrayList<String>()
      options.add("--aout=opensles")
      options.add("--http-reconnect")
      options.add("--audio-time-stretch") // time stretching
      options.add("--network-caching=1500")
      options.add("-vvv") // verbosity

       // create libvlc object
       libvlc = LibVLC(activity, options)

       // get surface view holder to display video
       this.holder=mSurface!!.holder
       holder!!.setKeepScreenOn(true)

       // Creating media player
       mediaPlayer = MediaPlayer(libvlc)

       // Setting up video output
       val vout = mediaPlayer!!.vlcVout
       vout.setVideoView(mSurface)
       vout.addCallback(this)
       vout.attachViews()
       val m = Media(libvlc, Uri.parse(media))
       mediaPlayer!!.setMedia(m)
       mediaPlayer!!.play()

  } catch (e: Exception) {
    Toast.makeText(activity, "Error in creating player!", Toast.LENGTH_LONG).show()
  }

}
```

## Project Structure

```bash
Dating-app-React-Native/
├── config/                         # configuration files like environment_config
├── node_modules/                   # This folder contains all the dependencies that the project requires, including React Native itself.
|   └── ...                         # all the dependencies listed
├── android/                        # This folder contains the Android project files, including Gradle build files, Java source code, and XML layout files.
├── ios/                            # This folder contains the iOS project files, including Xcode project files, Objective-C and Swift source code files.
├── App.js                          # This is the main component of the React Native app and is responsible for rendering the UI.
├── src/                            # Main source files folder
|   ├── assets/                     # The assets used in the project such as pngs / svgs..
|   └── components/                 # Context components relative to the app itself
|   └── uiComponents/               # General usable UI components everywhere through the app such as headers, drawers,..
├── package.json                    # This file contains metadata about the project, including the project name, version, and dependencies.
├── package-lock.json               # This file is generated by npm and ensures that the project's dependencies are installed in a consistent manner.
├── babel.config.js                 # This file contains configuration for the Babel transpiler
├── metro.config.js                 # This file contains configuration for the Metro bundler
```

## Dependencies

| Name                   | Description                                  | Version                    |
| ---------------------- | -------------------------------------------- | -------------------------- |
| [react-navigation]     | Navigation library                           | ^6.9.12                    |
| [moti]                 | Animation library                            | ^0.24.2                    |
| [react-content-loader] | Placeholder component library                | ^6.2.1                     |
| [gesture-handler]      | Gesture recognition library                  | ^2.9.0                     |
| [linear-gradient]      | Linear gradient component                    | ^3.0.2                     |
| [reanimated]           | Animation library                            | ^18.1.0                    |
| [redash]               | Utility library for animations               | ^4.5.1                     |
| [safe-area-context]    | Safe area component                          | ^3.20.0                    |
| [native-screens]       | Native screen components                     | ^3.3.0                     |
| [native-splash-screen] | Splash screen library                        | ^13.9.0                    |
| [native-svg]           | SVG rendering library                        | ^9.6.5                     |

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
