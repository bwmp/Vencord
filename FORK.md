# BWMP Vencord for Windows

This is an unofficial Vencord fork for bwmp and friends. Upstream code and licenses are preserved. Custom-build problems should be handled here, not by upstream Vencord support.

## Install

Download [VencordInstaller.exe from the latest release](https://github.com/bwmp/Vencord/releases/latest/download/VencordInstaller.exe), fully quit Discord, and select your Discord installation. Use Install, or Repair if Vencord is already installed. Then start Discord and enable automatic updates under Vencord settings. Restart Discord when an update is ready.

Use this fork's installer for future repairs. The official installer installs the official build instead. The Windows executable is unsigned.

## Add plugins

Add each plugin to `src/userplugins/PluginName/index.ts` (or `index.tsx`), commit it, and push to `main`. This fork tracks that directory. Do not add a second nesting level. No sample plugins are bundled.

The release workflow runs on pushes, hourly at minute 17, and manually through Actions. It merges `Vendicated/Vencord:main`, checks types and lint, builds Vencord and the Windows installers, then pushes the verified merge and publishes a complete release. Merge conflicts and failed checks stop publication. GitHub schedules can be delayed and can be disabled after 60 days without repository activity; check Actions if updates stop. Configure GitHub Actions failure notifications in your GitHub notification settings.

The installer is built from the pinned upstream commit in `.github/workflows/bwmp-release.yml`, with `scripts/fork/installer.patch` applied. Both installation and installer self-updates use this repository. Installer upstream changes require updating that pin and checking the patch; Vencord upstream changes are merged automatically.

## Recovery

Previous releases and their source remain available. To recover locally, disable automatic updates, quit Discord, back up `%APPDATA%\Vencord\dist`, and replace its `patcher.js`, `preload.js`, `renderer.js`, `renderer.css` and matching map files with those from a known-good release. Restart Discord. An old installer still downloads the latest release, so it does not perform a rollback.

For a fix for everyone, revert the faulty source change with a new commit and push to `main`; the workflow publishes a new build. Keep automatic updates off on affected machines until that release is available. Successful compilation does not guarantee Discord or custom-plugin runtime compatibility.
