# AppBridge downloads

Use selected Windows apps from your Android phone. Publish the apps you want to
share, pair your phone, and open multiple remote apps in one Android workspace.
This repository contains public downloads. The application source remains private.

## Download the pilot

| Device | Download |
| --- | --- |
| New Windows 11 24H2+ PC, Intel/AMD (x64) | [AppBridge Setup 1.1.4.0 (x64)](https://github.com/skyflyt/appbridge-releases/releases/download/v1.1.4.0/AppBridge-1.1.4.0-Setup.exe) |
| New Windows 11 24H2+ PC, Windows on ARM (ARM64 / Snapdragon) | [AppBridge Setup 1.1.5.0 (ARM64)](https://github.com/skyflyt/appbridge-releases/releases/download/v1.1.5.0-arm64/AppBridge-1.1.5.0-arm64-Setup.exe) |
| Android 10+ phone or tablet | [AppBridge Pilot 1.1.4 APK](https://github.com/skyflyt/appbridge-releases/releases/download/v1.1.4.0/appbridge-1.1.4-android-pilot.apk) |
| Release notes and checksums | [x64: Version 1.1.4.0 Setup](https://github.com/skyflyt/appbridge-releases/releases/tag/v1.1.4.0) → in-app updates [1.1.7.0-x64](https://github.com/skyflyt/appbridge-releases/releases/tag/v1.1.7.0-x64), [1.1.8.0-x64](https://github.com/skyflyt/appbridge-releases/releases/tag/v1.1.8.0-x64) · [ARM64: Version 1.1.5.0-arm64 Setup](https://github.com/skyflyt/appbridge-releases/releases/tag/v1.1.5.0-arm64) → in-app updates [1.1.6.0-arm64](https://github.com/skyflyt/appbridge-releases/releases/tag/v1.1.6.0-arm64), [1.1.8.0-arm64](https://github.com/skyflyt/appbridge-releases/releases/tag/v1.1.8.0-arm64) |

Pick the Setup that matches your PC. Open **Settings → System → About** and check
*System type*: "x64-based processor" → x64 Setup; "ARM-based processor" → ARM64
Setup. Each Setup refuses the other architecture. The Android APK is the same
for both.

Already have AppBridge installed on Windows? Open **Updates** in the app. The ZIP
asset is for that updater; use **Setup.exe** to install on a new PC.

## First connection

1. On Windows, run Setup from the administrator account that will share its apps.
   Review the pilot certificate trust page. Select the private-network option if
   your phone will connect on the local network.
2. Open AppBridge. In **Service**, enter this PC's reachable address and port 47641
   (for example, `https://192.168.1.10:47641`), enable **Allow LAN connections**, and
   click **Start listener**. Use your own PC's address.
3. In **Apps**, choose **Publish local app** and select an app to share.
4. Install the APK on Android and open **AppBridge Pilot**. In Windows **Pairing**,
   create an invitation, then scan its QR code on the phone.
5. Compare the displayed code on both devices, select the allowed apps, and approve
   the phone on Windows.

Setup includes Microsoft PowerShell and starts the service and desktop helper.
Its optional firewall rule allows only the AppBridge service on TCP 47641, on
Windows Private networks, from the local subnet. VPN routes outside that subnet
may need a separate owner-managed firewall rule. AppBridge does not include an
Internet relay. Windows must remain signed in and unlocked for app interaction.

## Pilot signing and updates

This is a coordinated pilot. Windows Setup uses a development signing certificate;
it requires explicit consent before adding the pinned public certificate to the
PC's trust store. The private key is not distributed. A production publisher
certificate and broader fresh-PC/device testing remain release requirements.
The x64 and ARM64 pilots use **separate** signing certificates and **separate**
update feeds; each installer pins only its own. Consent-page fingerprints:
x64 `5F00130FBD6FC246395C76B96437890BE271DE1F`, ARM64 `443A760C8F1E3A106151DE77D34CD79AF6394C27`.

Windows checks the signed GitHub feed and verifies package signatures and hashes.
Installation waits for active remote sessions to finish and requires Windows
administrator approval. Failed service startup triggers rollback. Pairings and app
settings remain in their protected data store.

The signed Android APK installs as **AppBridge Pilot** alongside the development
app. Existing development pairings remain in that app; pair the Pilot app once.
Future Pilot APKs update it in place. Android APK updates are manual for now;
Google Play distribution is planned separately.

Windows Installed apps provides uninstall, with settings preserved by default and
an explicit remove-data option for a clean reset. Preserved data needs recovery
before reinstalling. Shared PowerShell prerequisites remain installed.

Pilot Windows feeds:

- x64: `https://raw.githubusercontent.com/skyflyt/appbridge-releases/main/feed/pilot/windows-x64.json`
- ARM64: `https://raw.githubusercontent.com/skyflyt/appbridge-releases/main/feed/pilot/windows-arm64.json`
