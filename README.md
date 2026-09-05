# mespeak

`mespeak` is a 64-bit Android Text-to-Speech engine based on eSpeak
1.44.05-r29. It uses the Android service, settings and JNI integration model
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

On first launch, bundled voice data is installed before the settings lists are
built, all languages start selected, and a shortcut opens Android's system TTS
settings. The application includes the complete 104-variant collection from
eSpeak NG 1.52.0, with the `fast` file adapted to classic-eSpeak syntax.

Starting with r28, published APKs are optimized release builds. Their signing
lineage preserves updates from the r27 Android Debug certificate while moving
modern Android devices to the permanent Pates2004 release certificate. Its
SHA-256 fingerprint is
`2928C21E152E9FD245A5F423F0A11BD8FD658C09282684481C82EDF599E9E055`.
Verbose Java and JNI diagnostic logging is disabled in release builds.

Release r29 synchronizes the Polish dictionary with the Windows editions and
keeps hard `z` in the complete *bezinteres-* word family.

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

For an installable development APK, use `gradlew.bat assembleDebug`. For a
locally signed release that preserves the signing lineage from r27, run:

```text
powershell -ExecutionPolicy Bypass -File build-release.ps1
```

The release script reads the private signing material from the sibling
`signing` directory, which must never be committed to this public repository.

## Licensing

The eSpeak synthesizer sources and data are distributed under GPLv3; see
`LICENSE-eSpeak.txt`. Android integration files retain their original Apache
2.0 copyright and license notices.
