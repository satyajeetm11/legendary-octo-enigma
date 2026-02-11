# Desktop Staging Setup

This repo now supports a complete desktop staging channel using Tauri releases and updater manifests.

## Files added/updated

- `.github/workflows/release-staging.yml`
- `.github/workflows/build.yml` (release upload behavior improved for pre-created releases)
- `frontend/src-tauri/tauri.staging.conf.json`

## How staging works

1. Build artifacts are produced for macOS + Windows using `tauri.staging.conf.json`.
2. A draft prerelease is created with tag format: `staging-v<base>.<n>`.
3. `latest.json` from that release is published to branch `staging-updates`.
4. Staging desktop app checks updates at:
   - `https://raw.githubusercontent.com/satyajeetm11/legendary-octo-enigma/staging-updates/latest.json`

## Trigger staging release

- Push to `staging` branch, or
- Manually run workflow: `Release Staging`

## Required GitHub secrets

The staging workflow reuses signing and updater secrets from existing build workflows:

- `TAURI_SIGNING_PRIVATE_KEY`
- `TAURI_SIGNING_PRIVATE_KEY_PASSWORD`
- macOS signing/notarization secrets (`APPLE_*`) if signing mac builds
- Windows signing secrets (`SM_*`) if signing windows builds

## Important notes

- Staging app uses a separate bundle identifier: `com.meetingassistant.app.staging`
- Staging and production can be installed side-by-side.
- For stricter isolation, use a separate staging updater key and replace `plugins.updater.pubkey` in `tauri.staging.conf.json`.
