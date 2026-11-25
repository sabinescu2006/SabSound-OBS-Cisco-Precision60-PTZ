# Sab Sound – Cisco Precision 60 PTZ Control

An independent native OBS Studio dock plugin for controlling a Cisco Precision 60 camera over Ethernet using DORIC.

## Features

- Pan, tilt and diagonal movement with adjustable speed (1–5)
- Zoom, manual focus and autofocus
- Center/reset command, power and LED controls
- Four locally stored camera position presets (experimental; recall accuracy may vary)
- Connection settings and diagnostic journal

## Requirements

- Windows 64-bit
- OBS Studio (tested with 32.2.2 during development; build SDK 31.1.1)
- Cisco Precision 60 camera reachable on a trusted local network, TCP port 13496
- A working TLS backend compatible with the Qt runtime bundled with OBS
- A separate video capture source for the camera's HDMI output; this plugin controls the camera, not video capture

## Installation

1. Close OBS Studio.
2. Download the Windows x64 package from [Releases](https://github.com/sabinescu2006/SabSound-OBS-Cisco-Precision60-PTZ/releases).
3. Extract the archive, preserving its directory structure, into your OBS installation directory. The plugin DLL belongs in `obs-plugins/64bit`.
4. Start OBS and open **Docks → Sab Sound Cisco Precision 60 PTZ**.
5. Enter your camera's local IP address in the settings tab (Setari), review the certificate trust option and connect.

If TLS is unavailable, inspect the journal for the Qt runtime version and available backends. Obtain a compatible TLS backend from a trusted official Qt distribution and follow its deployment requirements. For the tested OBS installation, Qt 6.11.1 x64 was used and TLS plugins were placed in `bin/64bit/tls`. Do not overwrite unrelated OBS runtime DLLs. Backend requirements may vary by installation.

## Security and limitations

The camera connection supports legacy TLS and disables peer certificate verification after explicit user confirmation. Use only on a trusted, isolated local network; do not expose the camera control port to the internet. This is an independent, experimental integration, not an official Cisco or OBS product. Compatibility with other cameras or firmware versions is not established. The interface currently uses Romanian labels.

## Build

The repository uses the OBS plugin template and GitHub Actions to build Windows x64 packages. Source formatting checks remain enabled. Version tags use the format `1.0.0` (without a v prefix) to trigger a draft release.

## License and credits

GNU General Public License version 2; see [LICENSE](LICENSE). Based on the [OBS plugin template](https://github.com/obsproject/obs-plugintemplate).

Developed by Sab Sound — https://sabsound.ro
