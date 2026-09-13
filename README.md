# Arkitexe ServerFeel — prebuilt Windows package

This repo is the **ready-to-run build** of ServerFeel, a Halo Infinite
capture-and-log agent (it identifies the Azure server hosting each match,
measures your real ping to it, and logs every match). No Python needed.

## Get it

**Easiest:** download `ServerFeel-<version>-win64.zip` from the
[Releases](../../releases) page, unzip anywhere, double-click `ServerFeel.exe`.

**Or** clone this repo — the checkout *is* the unzipped folder:

```
git clone https://github.com/Arkitexe/ServerFeel-release.git
ServerFeel-release\ServerFeel.exe
```

Keep `ServerFeel.exe` and `_internal\` together.

## First launch

1. Accept the Windows admin (UAC) prompt — packet capture uses the WinDivert
   kernel driver, which needs it.
2. If SmartScreen says "Windows protected your PC": **More info → Run anyway**
   (the exe is not code-signed).
3. If it reports the Edge WebView2 runtime is missing (Windows 11 ships it),
   run `MicrosoftEdgeWebview2Setup.exe` from this folder once.
4. Start Halo. Matches log automatically. Your data lands in
   `%USERPROFILE%\Arkitexe\serverfeel\` — nothing is written to this folder.

`README.txt` has the full rundown, including the one hard rule: **don't run
clumsy at the same time** (it hijacks the WinDivert driver registration).

## What this is not

The source lives in the separate `ServerFeel` repo; this one only carries the
PyInstaller output produced by its `build_exe.bat`. Each release here matches
a tagged version there.
