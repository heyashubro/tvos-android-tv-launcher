# Install tvOS on Android TV

This guide is for Android TV and Google TV devices running Android 11 or later.

## Method A: Install from USB

1. On a computer, download [tvOS-Android-TV-1.0.apk](release/tvOS-Android-TV-1.0.apk).
2. Copy the APK to a USB drive and connect the drive to the TV.
3. Open the TV’s file manager and select the APK.
4. If Android blocks the install, open the prompt for **Install unknown apps** and allow it for that file manager. Return and install the APK.
5. Open **tvOS**. Follow the welcome steps, choose Dark or Light, or select **Skip setup**.
6. Press the remote’s **Home** button. Select **tvOS** as the Home app. Choose **Always** if Android offers that option.

If the TV does not include a file manager, use Method B or install a reputable file manager from the TV’s official app store.

## Method B: Install from a Windows computer with ADB

1. Connect the computer and TV to the same trusted home network.
2. On the TV, open **Settings → About** and press **OK** on **Build** seven times to reveal Developer options. Turn on **USB debugging** or **Wireless/Network debugging**. Menu names differ by manufacturer.
3. On Windows, download Google’s official [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools) and extract the folder. Open PowerShell in that folder.
4. Find the TV’s IP address in **Settings → Network**. Connect (many Android TV 11 devices use port 5555):

   ```powershell
   .\adb.exe connect TV_IP:5555
   .\adb.exe devices
   ```

   Replace `TV_IP` with the address shown on your TV. Accept the debugging prompt on the TV and check that `adb devices` says `device`.
5. Install the APK you downloaded on the computer:

   ```powershell
   .\adb.exe install -r .\tvOS-Android-TV-1.0.apk
   ```

   If you saved the APK elsewhere, use its full path.
6. Press **Home** on the TV remote and select tvOS as the Home app. Choose **Always** if prompted.

Some devices use a pairing code and a changing port instead. Follow the TV’s **Wireless debugging → Pair device** prompt and use the displayed pairing address/code with `adb pair`, then connect to the separate connection address shown by the TV.

## Use the launcher

- Use the remote arrows to select apps; press **OK** to open one.
- Hold **OK** on an app to move it, remove it from Home, or view App info.
- Open **App Library** at the end of the app grid to add a hidden app back.
- Open the Control Center gear to find tvOS Settings. Weather appears beside the clock and date in Control Center; enable it and choose a city or TV location in Settings → Status & Weather.
- To pick a local wallpaper or enable Glance, allow image access when asked. The app copies the selected wallpaper into its private storage, so it stays selected after you remove a USB drive.
- To change the default launcher later, use **Android TV Settings → Apps → Default apps → Home app** (wording varies by TV) and choose the launcher you want.

## Remove tvOS

Select your original launcher as the Home app first. Then open **Settings → Apps → tvOS → Uninstall**. This only removes tvOS; it does not remove other apps or restore any separately disabled packages.
