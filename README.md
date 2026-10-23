# tvOS for Android TV

A clean, remote-first Android TV home screen by **ASHU**. Version **1.0**. Minimum supported version: **Android 11 (API 30)**.

> tvOS is an independent Android TV launcher inspired by the simplicity of Apple TV interfaces. It is not affiliated with or endorsed by Apple Inc. “Apple” and “Apple TV” are trademarks of Apple Inc. No Apple artwork or font files are included.

## Download

Download the universal APK: [tvOS-Android-TV-1.0.apk](release/tvOS-Android-TV-1.0.apk)

The same APK targets Android TV devices running Android 11 or newer. It contains no per-CPU split downloads. It is signed so Android can verify its integrity; sideloaded builds can show a Play Protect notice because they are not distributed through Google Play.

## Install and set tvOS as Home

See the illustrated-by-steps guide in [INSTALL.md](INSTALL.md). In short:

1. Download the APK to a USB drive or the TV.
2. Open it with the TV’s file manager and allow that app to install unknown apps when Android asks.
3. Install tvOS, open it, and complete or skip the welcome screen.
4. Press the remote’s **Home** button and choose **tvOS**. If offered, select **Always**. You can switch launchers later in Android TV’s Default apps / Home app settings.

## Features

- Choose a built-in theme wallpaper or a local TV image; Glance can show local photos after an adjustable idle period.
- A compact clock pill expands to show date, time, Inputs, Wi-Fi, and Settings.
- Hold **OK** on an app to move it, remove it from Home, or open App info. The App Library at the end of the grid lets you add apps back.
- Reorder apps with the remote, adjust the grid and dock, choose Dark or Light appearance, and optionally add tvOS Settings to the app grid.
- First-launch welcome setup with a skip option.

## Clean up a TV safely

The launcher itself changes the Home screen; it does **not** delete apps or disable Android components. Start with [CLEANING.md](CLEANING.md) for safe, reversible cleanup steps. Never disable a package because its name merely looks unfamiliar. Keep the TV’s original Home app and core TV, input, remote, Wi-Fi, Play Store, and system services enabled until you have verified the replacement works and know how to restore the original.

## Build from source

Requirements: Java 17 and Android SDK Platform 34. From the repository root:

```powershell
cd launcher
.\gradlew.bat assembleRelease lintRelease
```

The APK will be at `launcher/app/build/outputs/apk/release/app-release.apk`. The app uses the existing Android package ID `com.gathin.tvhome` to preserve upgrade compatibility. `minSdk` is 30.

## Credits and licensing

This release is based on [Gathin23/CleanYourTV](https://github.com/Gathin23/cleanyourtv), used under its MIT license. The source license and attribution are preserved in [LICENSE](LICENSE). The Outfit typeface is distributed under the SIL Open Font License; see [`launcher/FONT-LICENSE-OFL.txt`](launcher/FONT-LICENSE-OFL.txt).

The requested SF Compact font is not bundled: Apple’s font download terms restrict its use to Apple watchOS mockups. This Android app uses the included, openly licensed Outfit font instead.

**Made with love in India by ASHU.** [heyashubro.pages.dev](https://heyashubro.pages.dev/)
