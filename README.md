<p align="center">
  <img src="assets/icons/debloater.png" alt="BraveDebloater" width="180" />
</p>

`Not affiliated with or endorsed by Brave Software`

# BraveDebloat

![Brave](https://img.shields.io/badge/Brave-FB542B?style=flat-square&logo=brave&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D4?style=flat-square&logo=windows&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-000000?style=flat-square&logo=apple&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)

Removes Brave Browser extras (Rewards, Wallet, VPN, Leo, News, telemetry and promo surfaces) using Brave's official enterprise policies, while keeping the everyday conveniences like autofill, translate and search suggestions.

Nothing changes until you add `-Apply`, every apply run makes a backup you can restore, and every policy it sets is visible in `brave://policy`.

## Credit

This is a fork of **[osfv/BraveDebloater](https://github.com/osfv/BraveDebloater)** by osfv, released under the MIT License. The script, policy manifest, safety checks and backup/restore system are all their work.

What this fork changes:

- The `Extreme` preset keeps convenience features instead of removing them (details below).
- A ready-made macOS configuration profile, so Mac users can install the policies without running a script.

## What Extreme Does

**Turns off:** Rewards, Wallet, VPN, Leo AI, News, Talk, Playlist, Email Aliases, Brave and Chromium telemetry, Web Discovery, remote spellcheck, promotions, Browser Labs, media recommendations, new tab cards, shopping list and the Google search side panel.

**Turns on:** De-AMP, bounce tracking protection, Global Privacy Control, tracking parameter stripping and language fingerprint reduction.

**Leaves alone:** Speedreader, Wayback prompts, search suggestions, network prediction, background mode, QR codes, payment buttons, autofill and translate.

That's 25 policies in total. Anything left alone can still be turned off with `-IncludeFeature` (see [Customise](#customise)).

It never disables Brave updates, turns off Shields or weakens Safe Browsing. The script refuses to write those policies.

## macOS: Install the Profile (no script)

1. Download [Brave-Debloat.mobileconfig](https://github.com/bishwofic/BraveDebloat/raw/main/profiles/macos/Brave-Debloat.mobileconfig).
2. Double-click it. macOS shows "Profile Downloaded".
3. Open **System Settings → General → Device Management**, double-click **Brave Debloat (25 policies)**, click **Install** and enter your password.
4. Quit and reopen Brave, then check `brave://policy`.

To remove it, go to the same screen, select the profile and click **−**.

The profile is unsigned, so macOS labels it "Unverified". That's expected for a personal profile; you can read the whole file before installing.

## Windows, macOS and Linux: Use the Script

1. Download this repo (**Code → Download ZIP**) and extract it, or clone it:

   ```bash
   git clone https://github.com/bishwofic/BraveDebloat.git
   cd BraveDebloat
   ```

2. Open PowerShell in that folder. Windows has it built in; on macOS or Linux install [PowerShell 7](https://learn.microsoft.com/powershell/scripting/install/installing-powershell) and run `pwsh`.

3. Preview what would change:

   ```powershell
   ./Invoke-BraveDebloat.ps1 -Preset Extreme
   ```

4. If it looks right, apply it and restart Brave:

   ```powershell
   ./Invoke-BraveDebloat.ps1 -Preset Extreme -Apply
   ```

On Windows, if scripts are blocked, run `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` once.

## Customise

```powershell
# List every feature name
./Invoke-BraveDebloat.ps1 -ListFeatures

# Keep something Extreme would turn off
./Invoke-BraveDebloat.ps1 -Preset Extreme -ExcludeFeature News,LeoAI

# Also turn off something Extreme leaves alone
./Invoke-BraveDebloat.ps1 -Preset Extreme -IncludeFeature Translate,Autofill

# Only apply specific features
./Invoke-BraveDebloat.ps1 -OnlyFeature Rewards,Wallet,VPN

# Choose each feature interactively
./Invoke-BraveDebloat.ps1 -Preset Extreme -Customize
```

Other presets: `Standard` removes Brave bloat and telemetry; `High` adds the privacy settings. `-LockShields` additionally enforces stricter Shields defaults.

## Check and Undo

```powershell
# Read-only report of what's currently applied
./Invoke-BraveDebloat.ps1 -Doctor

# List backups, then restore one (preview first, then add -Apply)
./Invoke-BraveDebloat.ps1 -ListBackups
./Invoke-BraveDebloat.ps1 -UndoFromBackup Latest
./Invoke-BraveDebloat.ps1 -UndoFromBackup Latest -Apply
```

## Where Policies Are Written

| Platform | Location |
| --- | --- |
| Windows | Registry: `HKCU\Software\Policies\BraveSoftware\Brave` (add `-Scope LocalMachine` for all users, as admin) |
| macOS | `defaults write com.brave.Browser` (or the profile above, which applies machine-wide) |
| Linux | `/etc/brave/policies/managed/BraveDebloater.json` (run with `sudo pwsh`) |

To create a policy file without applying it, for example a Windows `.reg`:

```powershell
./Invoke-BraveDebloat.ps1 -Platform Windows -Preset Extreme -ExportPolicyPath ./brave-policy.reg
```

## Sources

Policy names and values come from Brave's official [Group Policy documentation](https://support.brave.app/hc/en-us/articles/360039248271-Group-Policy) and [policy templates](https://brave-browser-downloads.s3.brave.com/latest/policy_templates.zip).

## License

MIT. See [LICENSE](LICENSE). Original work © osfv.
