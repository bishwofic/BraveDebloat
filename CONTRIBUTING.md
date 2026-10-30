# Contributing

Issues and pull requests are welcome at [bishwofic/BraveDebloat](https://github.com/bishwofic/BraveDebloat/issues).

This is a fork of [osfv/BraveDebloater](https://github.com/osfv/BraveDebloater). Fixes to the core script are usually best sent there first, so everyone benefits; changes specific to this fork (the `Extreme` preset and the ready-made profiles) belong here.

## Rules For Policy Changes

- Use official Brave or Chromium enterprise policies rather than profile JSON edits.
- Never add policies that disable Brave Shields, allowlist URLs from Shields, weaken Safe Browsing, or disable browser or component updates.
- Add every policy to `config/policies.json` with a clear category and reason.
- Keep previews readable for non-experts, and keep restore working for any new write path.

## Keep the Profiles in Sync

The `Extreme` preset, `profiles/macos/Brave-Debloat.mobileconfig` and `profiles/windows/Brave-Debloat.reg` must set the same policies with the same values. If you change one, update the others in the same pull request (including `Brave-Debloat-Remove.reg`), and bump `PayloadVersion` in the mobileconfig.

## Checks

Before opening a pull request, run:

```powershell
./scripts/Test-PolicyManifest.ps1
./scripts/Test-Behavior.ps1
./Invoke-BraveDebloat.ps1 -Preset Extreme
```

The last command is a preview and changes nothing.
