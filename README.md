# mespeak

`mespeak` is a 64-bit Android Text-to-Speech engine based on eSpeak
1.44.05-r26. It uses the Android service, settings and JNI integration model
from eSpeak NG, while the native synthesizer and voice data come from the
reborn eSpeak 1.44.05 codebase, including its current Polish dictionary.

The speech-rate dialog includes an optional Sonic time-compression boost. The
normal eSpeak rate remains unchanged; above 450 WPM the legacy core uses the
clarity-oriented timing model from eSpeak NG before Sonic performs the
remaining pitch-preserving compression.

The settings interface follows the system language in Polish and uses English
for every other locale. A checked-by-default setting controls whether the
`mespeak` icon is shown in the launcher; hiding it does not disable the TTS
engine or remove its entry from Android TTS settings.

This repository builds the architectures used by modern Android devices and
the 64-bit Pixel emulator:

- `arm64-v8a`
- `x86_64`

The application identifier is `com.pates2004.mespeak`. The separate
[`mespeak-x32`](https://github.com/Pates2004/mespeak-x32) project contains the
32-bit build for older devices. Both editions expose the same Android TTS
features and use the same engine data.

## Build

Use JDK 17 and the Android SDK, NDK and CMake versions declared in
`build.gradle`:

```text
gradlew.bat assembleDebug
```

The resulting APK is `build/outputs/apk/debug/mespeak-debug.apk`.

## Licensing

The eSpeak synthesizer sources and data are distributed under GPLv3; see
`LICENSE-eSpeak.txt`. Android integration files retain their original Apache
2.0 copyright and license notices.
