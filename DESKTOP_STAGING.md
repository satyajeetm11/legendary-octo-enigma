# Desktop Staging Setup

This repo now supports a complete desktop staging channel using Tauri releases and updater manifests.

## Files added/updated

- `.github/workflows/release-staging.yml`
- `.github/workflows/build.yml` (release upload behavior improved for pre-created releases)
- `frontend/src-tauri/tauri.staging.conf.json`

## How staging works

1. Build artifacts are produced for macOS + Windows using `tauri.staging.conf.json`.
2. A prerelease is created with tag format: `staging-v<base>.<n>`.
3. Installers are published as release assets for tester installs.

## Trigger staging release

- Push to `staging` branch, or
- Manually run workflow: `Release Staging`

## Required GitHub secrets

The current staging workflow is configured for simple setup (unsigned builds), so no signing secrets are required.

If you later want signed binaries and OTA updater for staging, add and configure:

- macOS signing/notarization secrets (`APPLE_*`) if signing mac builds
- Windows signing secrets (`SM_*`) if signing windows builds
- `TAURI_SIGNING_PRIVATE_KEY`
- `TAURI_SIGNING_PRIVATE_KEY_PASSWORD`

## Important notes

- Staging app uses a separate bundle identifier: `com.meetingassistant.app.staging`
- Staging and production can be installed side-by-side.
- OTA updater manifest publishing is currently disabled for staging.
- For stricter isolation when enabling updater later, use a separate staging updater key and replace `plugins.updater.pubkey` in `tauri.staging.conf.json`.
