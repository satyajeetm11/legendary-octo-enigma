# Meeting Assistant Productization Guide

This repository is now prepared as a starter base for your own product brand (`Meeting Assistant`).

## What was already customized

- Desktop app identity:
  - `frontend/src-tauri/tauri.conf.json`
    - `productName`: `meeting-assistant`
    - `identifier`: `com.meetingassistant.app`
    - window title: `Meeting Assistant`
- Frontend metadata:
  - `frontend/src/app/metadata.ts`
  - `frontend/src/app/metadata.tsx`
- Visible UI branding labels:
  - `frontend/src/components/Logo.tsx`
  - `frontend/src/components/Info.tsx`
  - `frontend/src/components/TranscriptView.tsx`
  - `frontend/src/components/VirtualizedTranscriptView.tsx`
- Package identity:
  - `frontend/package.json` (`name` set to `meeting-assistant`)

## Local setup status on this machine

- Node.js is installed (`v22.17.1`)
- Frontend npm dependencies are installed in `frontend/node_modules`
- Rust is installed (`rustc 1.93.0`, `cargo 1.93.0`)
- `cmake` is installed via `pip` at `~/Library/Python/3.9/bin/cmake`
- Current macOS blocker: Xcode plugin load failure during Rust build (`cidre`), requiring:
  - `xcodebuild -runFirstLaunch`

## Next commands to run

1. Ensure Xcode first-launch setup is complete:

```bash
xcodebuild -runFirstLaunch
```

2. Ensure `cmake` is on PATH for this shell:

```bash
export PATH="$HOME/Library/Python/3.9/bin:$PATH"
```

3. Start app in dev mode:

```bash
cd frontend
source "$HOME/.cargo/env"
npm run tauri:dev
```

## Critical branding and ownership tasks before launch

1. Replace remaining `Meetily` references in UI copy, notifications, and docs.
2. Replace app icons in `frontend/src-tauri/icons/` and `frontend/public/`.
3. Change updater endpoint in `frontend/src-tauri/tauri.conf.json` to your own releases feed.
4. Set your own legal docs (`PRIVACY_POLICY.md`, terms, consent copy).
5. Create your own GitHub org/repo and wire CI/CD for signed desktop releases.

## Recommended product roadmap

1. Ship MVP fork quickly
- Keep core recording, transcription, summaries as-is
- Rebrand, package, and test on your target OS

2. Add differentiation
- Better summary templates by persona/use-case
- Team workspace + export workflows
- Optional cloud sync with explicit privacy controls

3. Production hardening
- Telemetry/health checks (privacy-safe)
- Crash reporting
- In-app update quality gates
