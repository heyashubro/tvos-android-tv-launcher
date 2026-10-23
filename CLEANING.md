# Clean up an Android TV safely

**tvOS is a launcher, not a debloater.** Installing tvOS changes the Home screen only. It does not remove or disable apps. You can use the TV’s Settings to uninstall apps you installed yourself. For manufacturer apps, use the guidance below and keep changes reversible.

## 1. Start with Android TV Settings

1. Open **Settings → Apps → See all apps** (menu names vary by TV).
2. Uninstall only apps you personally installed and recognize.
3. For preinstalled apps, use **Disable** only when the TV explicitly offers it and you know exactly what that app does. When unsure, leave it enabled.
4. Do not disable the original Home/launcher, TV/input services, remote or Bluetooth components, Wi-Fi/network services, Android Settings, System UI, package installer, permission controller, Play Store, Play services, or anything you use for casting, voice control, updates, or streaming.

## 2. Optional advanced method: the CleanYourTV scripts

This repository retains the upstream CleanYourTV scripts and device-specific package lists. They disable selected packages for the current Android user; they do not uninstall those packages. The scripts create a recovery record before making changes and include checks for Android core packages and the active Home app. Disabling the wrong manufacturer service can still remove features or make a TV difficult to recover.

Use this only if you are comfortable with Windows PowerShell, the TV’s exact model is present under `examples/`, and you have read the list and upstream safety notes. Do not substitute a similar-looking model or apply a list from another brand.

1. Check the exact TV model and Android version in **Settings → About**. Leave the original Home app enabled.
2. Turn on ADB/Network debugging in Developer options. Keep the TV on the same trusted network as the computer and accept its debugging prompt.
3. Open PowerShell at the repository root and prepare the script environment:

   ```powershell
   py -m venv tools\venv
   tools\venv\Scripts\python.exe -m pip install -r tools\requirements.txt
   $env:TV_HOST = "TV_IP"
   tools\venv\Scripts\python.exe -I tools\tv.py --probe
   ```

   Replace `TV_IP` with your TV’s IP address. Confirm the probe reports the correct manufacturer/model and Android version before proceeding.
4. Locate the exact matching device folder under `examples/`. Read its README/header and every line in `debloat.txt`. Comment out any item you use or cannot confidently identify. If there is no exact matching model, stop here.
5. Apply only the reviewed list:

   ```powershell
   tools\disable.ps1 -List "examples\EXACT-MODEL-FOLDER\debloat.txt" -TvHost $env:TV_HOST
   ```

   Replace `EXACT-MODEL-FOLDER` with the exact folder name. Read each script message. Do not bypass a safety refusal or force the Home guard.
6. Check that the TV still opens Home, Wi-Fi, HDMI/Live TV, remote controls, Play Store, casting (if you use it), and your streaming apps. Reboot and check again.
7. To undo changes, use the **same list** you applied:

   ```powershell
   tools\restore.ps1 -List "examples\EXACT-MODEL-FOLDER\debloat.txt" -TvHost $env:TV_HOST
   ```

   Keep the recovery record and a copy of the list. `restore.ps1` restores the prior state recorded by the script. It cannot recover a TV that no longer accepts ADB or boots.

For the upstream project’s complete device notes and safety details, see [Gathin23/CleanYourTV](https://github.com/Gathin23/cleanyourtv). Never run cleanup commands you do not understand, and never uninstall Android system packages.
