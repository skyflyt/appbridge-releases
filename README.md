# AppBridge releases

AppBridge lets a paired Android device use selected apps running on a Windows PC.
This repository holds public release metadata and downloadable Windows builds.
The application source repository remains private.

**Pilot software — not a general release.** Initial setup and recovery testing are
still being completed. There is no finished installer for new PCs yet; pilot
downloads are intended for coordinated testing.

## Current Windows prerequisites

- Windows x64 with an unlocked, signed-in desktop for remote app interaction.
- PowerShell 7.6 or later installed in its standard, protected Program Files location.
- An AppBridge installation configured for the signed UIAccess desktop helper.
- Explicit trust of the pilot's development signing certificate on each test PC.
  The private signing key is never distributed.

The pilot signing identity is not the final production distribution identity.
Initial installation and updates can require local administrator approval.
Downloaded updates preserve existing pairing and app settings; installation waits
until remote sessions have ended.

## Updates

The Windows app checks a signed release feed and verifies package hashes before
staging an update. An installed verification key determines which releases are
trusted; this repository cannot supply a replacement key through the feed.

- Pilot feed: `https://raw.githubusercontent.com/skyflyt/appbridge-releases/main/feed/pilot/windows-x64.json`
- Versioned builds: [Releases](https://github.com/skyflyt/appbridge-releases/releases)

The feed and first release will appear when pilot acceptance is complete.
Android distribution is planned through Google Play; this feed updates Windows only.
