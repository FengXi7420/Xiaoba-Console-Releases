<div align="center">
  <img height="128" src="docs/branding/m-control-repository-icon.png" alt="Xiaoba Console Logo">

  # Xiaoba Console

  [![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D4?logo=windows&logoColor=white)](#download-and-installation)
  [![.NET Framework](https://img.shields.io/badge/.NET%20Framework-4.6.2-512BD4?logo=dotnet&logoColor=white)](#download-and-installation)
  [![Downloads](https://img.shields.io/github/downloads/FengXi7420/Xiaoba-Console-Releases/total?color=brightgreen)](https://github.com/FengXi7420/Xiaoba-Console-Releases/releases)
  [![MSI laptops](https://img.shields.io/badge/MSI-laptops-D23D1D)](#compatibility)
  [![Telemetry](https://img.shields.io/badge/telemetry-none-success)](#privacy-and-network-access)
</div>

## 🚨 Project Status Notice

> [!IMPORTANT]
> - Xiaoba Console is under active development and is primarily improved through real MSI laptop feedback.
> - The current release, issue-reporting and documentation entry is [FengXi7420/Xiaoba-Console-Releases](https://github.com/FengXi7420/Xiaoba-Console-Releases).
> - This project is not affiliated with MSI / Micro-Star International and is not official MSI software.
> - Xiaoba Console accesses low-level hardware interfaces including EC, MSI WMI, UEFI variables, NVAPI / NVML and SteelSeries HID. Read the disclaimer and risk notes before using it.

#### Other language versions of this README file:

- 简体中文: [README.md](README.md)
- English: current file

---

Xiaoba Console is a lightweight Windows hardware control utility for MSI laptops. It aims to replace the most commonly used parts of MSI Center / Dragon Center with a smaller, local-first application: dashboard monitoring, fan curves, performance modes, GPU mode switching, battery health, SteelSeries keyboard lighting, shortcut OSD, MSI support-page shortcuts and version checks.

The project follows the same general direction as [G-Helper](https://github.com/seerge/g-helper) and [Lenovo Legion Toolkit](https://github.com/LenovoLegionToolkit-Team/LenovoLegionToolkit): keep the laptop control features that matter, reduce background services, avoid account systems and unrelated online modules, and keep the application quiet when it is not needed. Xiaoba Console does not include telemetry or user-data collection.

# Localization

The main UI and Chinese README cover the current feature set. This English README includes the project overview, requirements, features, risks and build instructions. More model-specific compatibility notes and troubleshooting documentation will be added as more MSI laptop data becomes available.

Translations and model reports are welcome. Because MSI EC, WMI, lighting, GPU mode and driver behavior varies significantly between laptop generations, documentation should match verified behavior whenever possible.

## Project Icon

Project branding assets are stored in `docs/branding/`:

- `m-control-repository-icon.png`: a 512×512 square icon for a GitHub user / organization avatar or for code-hosting platforms that support repository avatars.
- `m-control-social-preview.png`: a 1280×640 social preview image for GitHub repository Social preview.

Note: the small icon shown next to a GitHub repository title comes from the repository owner avatar, not from a file inside the repository. To make the title area look like the LenovoLegionToolkit example, upload `m-control-repository-icon.png` as the GitHub user / organization avatar. Use `m-control-social-preview.png` for repository share cards.

---

# Table of Contents

- [Localization](#localization)
- [Project Icon](#project-icon)
- [Disclaimer](#disclaimer)
- [Closed-Source Freeware Notice](#closed-source-freeware-notice)
- [Download and Installation](#download-and-installation)
- [Compatibility](#compatibility)
- [Features](#features)
- [Design Goals](#design-goals)
- [Fan Calibration](#fan-calibration)
- [Command Line Arguments](#command-line-arguments)
- [Diagnostic Logs](#diagnostic-logs)
- [Build](#build)
- [Tests](#tests)
- [Packaging](#packaging)
- [Project Structure](#project-structure)
- [Privacy and Network Access](#privacy-and-network-access)
- [Feedback and Compatibility Reports](#feedback-and-compatibility-reports)
- [Risk Notes](#risk-notes)
- [License](#license)

---

## Disclaimer

**Xiaoba Console is not official MSI software and does not provide official warranty or support.**

This project can read from and write to low-level hardware interfaces such as EC, MSI WMI, UEFI variables, WinRing0 and SteelSeries HID, and uses NVAPI / NVML for read-only GPU telemetry. Behavior can differ between MSI laptop models, BIOS versions, EC firmware versions and driver stacks. Fan curves, GPU mode switching, power limits, keyboard lighting and hotkey handling must be verified on the target device.

You are responsible for any hardware issue, system instability, data loss, warranty dispute or other consequence caused by using this project.

---

## Closed-Source Freeware Notice

Xiaoba Console is currently released as closed-source freeware. The software communicates with low-level MSI laptop hardware interfaces including EC, fan controllers, keyboard lighting and GPU mode paths. Some compatibility work depends on unpublished interfaces, private protocol adaptation and reverse-engineering notes. To avoid unnecessary intellectual-property or compliance risks and to keep the project maintainable, the implementation details and project code are not publicly released at this stage.

Xiaoba Console does not include telemetry, does not collect user data and does not read personal files. Core hardware-control features run locally. Release packages should include SHA256 checksums so users can verify file integrity, and users may scan the package with antivirus tools or test it in a virtual machine before using it. If you are uncomfortable with closed-source hardware-control tools, do not use it.

---

## Download and Installation

Releases provide a regular installer and a regular portable archive. The large `MControl_v<version>_Setup_WebView2_Fixed.exe` may be provided for both baseline releases and hotfixes. It contains the pinned x64 Fixed Version Runtime.

Xiaoba Console v1.0.0 establishes this release line's in-place upgrade baseline. M-Control v1.1.0 or later can be replaced directly by installing Xiaoba Console; earlier M-Control releases should be uninstalled first. Future Xiaoba Console releases can be installed directly over v1.0.0 or later.

Requirements:

- Windows 10 / 11 x64.
- .NET Framework 4.6.2.
- Microsoft Edge WebView2 Runtime.
- MSI ACPI WMI Provider / MSIWMIACPI2 platform driver.
- WinRing0 runtime files for EC / MSR fallback access.
- NVIDIA driver and NVAPI / NVML / nvidia-smi for read-only NVIDIA GPU monitoring.
- SteelSeries keyboard lighting first uses compatible HID devices already enumerated by Windows. If an existing SteelSeries GG installation exposes an advanced KLC channel, Xiaoba Console can reuse it; otherwise it prioritizes the driver-free HID path. Release packages do not bundle `ssdevfactory` / `ssps2` / `msihid`.
- Administrator privileges may be required for low-level hardware access.

---

## Compatibility

Xiaoba Console targets MSI laptops, especially models with EC fan control, MSI WMI support, GPU mode switching and SteelSeries keyboard lighting.

Compatibility depends on:

- Laptop model and motherboard platform.
- BIOS and EC firmware version.
- MSI ACPI WMI Provider / MSIWMIACPI2 driver state.
- NVIDIA driver and NVAPI / NVML availability.
- SteelSeries keyboard PID, HID channel and driver stack.
- ThermalInfo, IPF / DTT, LibreHardwareMonitor and MSR sensor availability.

Known limitations:

- Features without matching EC registers or WMI commands will not be shown or enabled.
- Laptops without a dGPU or MUX support will not provide full GPU mode switching.
- SteelSeries lighting depends on keyboard device, firmware, driver stack and protocol.
- Third / fourth fans, PCH temperature, and system power are shown only when valid data is available.

---

## Features

### Dashboard

- CPU / GPU temperature, frequency, power, battery state and fan state.
- AMD CPU temperature prefers the Feature Manager-style ThermalInfo `Get_Temperature(0)` CPU value before falling back to ThermalInfo AMD SENSOR `Get_BIOS(3)`, generic ThermalInfo and EC. AMD CPU power prefers PawnIO/MSR RAPL AMD package before falling back to LHM / WMI / ThermalInfo.
- Fan display can switch between RPM and percentage. Percentage mode requires fan calibration.
- Fan RPM prefers ThermalInfo `Get_Fan(0)`, with EC direct reads as fallback.
- Extended sensors can show PCH, third / fourth fan and system power when supported.
- Monitoring uses fast and slow paths so core health values can appear quickly while slower extended sensors are filled in later.

### Fan Control

- Independent CPU and GPU fan curves.
- Automatic / manual modes, draggable curve points and table editing.
- The curve Y-axis is RPM. EC duty is treated as 0-150, with a maximum display value of 9000 RPM (`150 × 60`).
- Restore Default returns to the current BIOS / EC default curve for the machine.
- Fan curve reads and writes prefer ThermalInfo official `Get_* / Set_*` paths, with EC fallback.
- Percentage display calibration uses IQR outlier rejection and a median full-speed reference to reduce RPM spikes.
- Full-speed fan mode is available from the UI and through `Fn + ↑`.

### Performance, Power and GPU Mode

- Balanced, Silent, Super Battery and High Performance modes.
- Startup sync reads the real active performance mode.
- Windows power plan control can be used alongside MSI performance modes.
- GPU mode supports integrated, hybrid and discrete options where available.
- After GPU mode changes, the user can restart immediately or restart later.

### GPU Monitoring

- Read-only NVIDIA GPU temperature, frequency, power, utilization and fan state.
- The main branch does not ship GPU overclocking, clock locking, VF-curve controls, or game FPS detection. Those experiments remain isolated on a development branch.

### Battery

- Battery charge limit.
- Health, cycle count, design capacity, full charge capacity, current capacity and voltage.
- Battery current includes direction and unit correction to avoid inverted charge/discharge status.

### SteelSeries Keyboard Lighting

- Zone groups, effects, color palette, brightness and speed.
- SteelSeries native KLC HID and driver-free FW Basic / direct-HID paths, with reuse of an already installed GG / KLC channel when available.
- SteelSeries GG is not required; dynamic effects use built-in real-device HID captures and native write logic.
- Release packages do not include `ssdevfactory` / `ssps2` / `msihid`, and Xiaoba Console does not install SteelSeries drivers. Existing GG / SteelSeries KLC channels are detected and reused automatically.
- Per-key editing, official key mapping, partial-zone writes, dynamic effects, response layers and lighting-host takeover.
- Dedicated handling for Raider 18 / KLC071 / PID_1122 / PID_1161 and related device families.

### Hotkeys and OSD

- Fixed hotkeys: `Fn + ↑` toggles full-speed fan mode; `Fn + F4` toggles the touchpad.
- Real shortcuts listed in the Information page are connected to the top-left OSD where possible.
- OSD displays status only and does not take over system functions.
- Features with readable state show on / off. Features without reliable state show triggered / switched.
- Coverage includes CapsLock, touchpad, full-speed fan mode, Win/Fn swap, volume, brightness, screenshot, display output, keyboard backlight, media, sleep, microphone, Bluetooth, Fn Lock, crosshair and Scroll Lock.
- Hotkey events can come from low-level keyboard hooks, MSI WMI hotkey events and EC debug registers, with duplicate-event throttling.

### Drivers, Information and App Behavior

- Driver Update opens the MSI China support page for the detected model.
- Installed driver list and backup entry points.
- Hardware Information shows machine, CPU, GPU, memory, disks and shortcut documentation.
- About page includes version checking, ignored version and automatic-check settings.
- Startup behavior, close-to-tray, auto-start, minimized startup and keep-lighting-on-exit are available in Settings.
- The main application is single-instance: launching it again restores the existing window.

---

## Design Goals

Xiaoba Console does not aim to clone every MSI Center module. It focuses on daily laptop control tasks:

- Keep common hardware controls in one lightweight utility.
- Reduce resident services, popups, account systems and unrelated online modules.
- Prefer local hardware interfaces and local drivers.
- Hide or clearly degrade unsupported functionality instead of displaying misleading states.
- Avoid telemetry and user-data collection.

---

## Fan Calibration

Fan calibration is used by dashboard fan percentage mode. PWM / duty readings are inconsistent across MSI models, so Xiaoba Console estimates the full-speed reference from actual RPM samples.

Calibration flow:

1. Enable full-speed fan mode and wait for spin-up.
2. Collect RPM samples at 1Hz.
3. Filter zero and physically unreasonable values.
4. Use IQR to remove outliers.
5. Use the median value as the full-speed reference.
6. Calculate runtime percentage as `current_rpm / RpmRef × 100` with a small clamp for jitter.

Calibration data is saved to `%LocalAppData%\M-Control\fan-calibration.json` and keyed by model.

---

## Command Line Arguments

Common startup arguments:

- `--background`: start in the background without showing the main window.
- `--minimized`: start minimized.

If an instance is already running, a normal launch restores the existing window. Background startup arguments do not force the existing window to appear.

---

## Diagnostic Logs

Xiaoba Console provides two-level logging:

### 1. Error Logs (enabled by default)

All hardware operation failures, configuration load errors and other exceptions are automatically logged to:
- `%LocalAppData%\M-Control\error.log`

Log format:
```
[2026-06-20 02:15:30] WARN Failed to read GPU temperature via NVAPI
System.Exception: NVAPI error code 5
   at MControl.Core.GpuTelemetryController.CollectTelemetryUncached()
   ...
```

### 2. Diagnostic Logs (manual enable)

For detailed troubleshooting, create an empty file at `%LocalAppData%\M-Control\debug.flag` and restart the application.

Common diagnostic logs:
- `telemetry_debug.txt`: CPU / GPU frequencies, power and sensor values.
- `fan_debug.txt`: fan RPM, percentage and parsing path.
- `monitor_push_debug.txt`: frontend monitoring payload.
- `gpu_mode_read_debug.txt`: GPU mode detection path.
- `errors.txt`: backend errors (debug mode only).
- `errors_js.txt`: frontend JavaScript errors.
- `hotkey_debug.txt`: hotkey and EC debug-register events.

Remove `debug.flag` and restart to disable diagnostic logs.

---

## Build

```powershell
dotnet build MControl.sln -c Release
```

Output:

```text
01_source\MControl\bin\Release\net462\MControl.exe
```

Build requirements:

- Windows 10 / 11 x64.
- .NET SDK capable of building .NET Framework 4.6.2 projects.
- Microsoft Edge WebView2 Runtime.
- Administrator privileges for runtime hardware access.

Windows Release builds are validated with compatible .NET 8 and .NET 10 SDKs and complete with zero warnings.

---

## Tests

JavaScript syntax checks:

```powershell
Get-ChildItem 01_source\MControl\Web -Filter app*.js | ForEach-Object { node --check $_.FullName }
```

Run all static smoke tests:

```powershell
Get-ChildItem 01_source\tests -Filter *.test.js | ForEach-Object { node $_.FullName }
```

These tests lock down important UI, hardware-path and documentation hooks so confirmed behavior is not accidentally removed.

---

## Packaging

```powershell
powershell -File 02_build\scripts\Publish-MControl.ps1
```

The script:

1. Publishes the app to `02_build\publish_final_yyyyMMdd_HHmmss\`.
2. Removes runtime debug text files and temporary diagnostics.
3. Cleans old frontend leftovers.
4. Creates `02_build\MControl_v<version>_Portable.zip`.
5. With `-IncludeWebView2OfflinePortable`, also creates `02_build\MControl_v<version>_Portable_WebView2_Offline.zip`.
6. Builds `03_exe\MControl_v<version>_Setup.exe` when Inno Setup 6 is detected.
7. Creates `02_build\SHA256SUMS.txt` for release-page verification.

Options:

- `-SkipInstaller`: skip Inno Setup package creation.
- `-NoVersionBump`: keep the current source version.
- `-IncludeWebView2OfflinePortable`: add a portable ZIP containing Microsoft's official x64 WebView2 offline installer.
- `-WebView2OfflineInstallerPath <path>`: use an existing verified x64 offline installer instead of downloading it to the ignored build cache.
- `-InnoSetupExe <path>`: specify the `ISCC.exe` path.

---

## Project Structure

```text
01_source/MControl/        Main application source
├── MControl.csproj        net462 / x64 / WinExe
├── Program.cs                Entry point, DPI and single-instance startup flow
├── MainForm.cs               Main window and core hardware-control logic
├── MainForm.HostBridge.cs    WebView2 ↔ C# JSON RPC routing
├── MainForm.Tray.cs          Tray, auto-start and window restore
├── MainForm.Monitor.cs       Dashboard sampling and extended sensors
├── MainForm.DriverUpdate.cs  MSI support page and driver backup
├── MainForm.Shortcut.cs      Hotkeys, MSI WMI events and keyboard hook
├── MainForm.Osd.cs           OSD triggers and shortcut mapping
├── MainForm.Touchpad.cs      Touchpad state read/write paths
├── Core/                     EC, WMI, GPU, lighting and sensor hardware layer
├── Services/                 Logging and atomic-file infrastructure
│   ├── Logger.cs             File-based logging system (supports formatting)
│   └── AtomicFile.cs         Same-directory temporary files and atomic replacement
└── Web/                      WebView2 frontend pages, styles and scripts

02_build/                     Build scripts and release output
03_exe/                       Inno Setup output
01_source/tests/              Node static smoke tests
```

---

## Privacy and Network Access

Xiaoba Console does not include telemetry, does not collect user data and does not upload hardware information.

Possible network access:

- Opening Driver Update redirects to the MSI support website.
- Version checking requests GitHub update-repository Release information.

Core hardware-control features run locally.

---

## Feedback and Compatibility Reports

Useful reports include:

- Compatibility reports for new MSI laptop models.
- BIOS / EC version and feature availability records.
- Real-device test results for fans, GPU mode, touchpad, lighting and hotkeys.
- Documentation, translation, installation-flow and website-content suggestions.

When reporting an issue, include:

- Exact laptop model.
- Windows version.
- BIOS / EC version.
- MSI platform-driver versions.
- NVIDIA driver version.
- Reproduction steps.
- Relevant logs generated with `debug.flag` enabled.

---

## Risk Notes

- EC writes can affect fans, battery behavior, keyboard state, GPU mode and system stability.
- Fan curves, full-speed mode, power limits and GPU mode switching should be verified on test hardware.
- Touchpad and hotkey behavior varies between MSI laptop generations.
- SteelSeries lighting depends on PID, firmware, driver stack and HID channel.
- Some WMI features still require MSI ACPI WMI Provider.

---

## License

The current release is closed-source freeware. You may install and use official release packages for free on personal devices, but you may not sell, repackage, impersonate the original authors, remove or alter attribution, or claim any official MSI authorization or partnership.
