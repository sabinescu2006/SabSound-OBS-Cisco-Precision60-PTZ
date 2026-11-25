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

The camera connection supports legacy TLS and disables peer certificate verification after explicit user confirmation. Use only on a trusted, isolated local network; do not expose the camera control port to the internet. This is an independent, experimental integration, not an official Cisco or OBS product. Compatibility with other cameras or firmware versions is not established. The interface supports English (default) and Romanian; choose your language in Settings.

## Build

The repository uses the OBS plugin template and GitHub Actions to build Windows x64 packages. Source formatting checks remain enabled. Version tags use the format `1.0.0` (without a v prefix) to trigger a draft release.

## License and credits

GNU General Public License version 2; see [LICENSE](LICENSE). Based on the [OBS plugin template](https://github.com/obsproject/obs-plugintemplate).

Developed by Sab Sound — https://sabsound.ro


## Detailed Windows installation and TLS troubleshooting

1. Download the Windows x64 release ZIP and extract it.
2. Close OBS completely. Copy the plugin DLL into `C:\Program Files\obs-studio\obs-plugins\64bit\` (adjust for custom installations). Preserve any accompanying data directories in the package.
3. Restart OBS. Select **Docks → Sab Sound Cisco Precision 60 PTZ**.
4. Open Settings, enter the camera IP, explicitly accept the unverified LAN certificate if appropriate, and click Connect.

If the dock is missing, check **Help → Log Files → View Current Log** for plugin loading errors. Confirm that OBS and the plugin are both 64-bit.

If connection fails with a TLS backend error:
- Open the plugin Journal and check the reported Qt runtime version, TLS backends and plugin paths.
- In our development test with OBS 32.2.2, the runtime was Qt 6.11.1 x64. Compatible Qt TLS plugins were needed in `C:\Program Files\obs-studio\bin\64bit\tls\`.
- Obtain the matching Windows x64 Qt base distribution from the [official Qt archive](https://download.qt.io/). Locate its `plugins/tls` directory. With OBS closed, copy the compatible TLS backend DLLs into the OBS TLS directory above, creating it if necessary. Back up existing files first.
- Depending on the backend, additional matching runtime dependencies may be required. Do not mix Qt versions or replace OBS core Qt DLLs. The exact backend/dependency combination was not recorded conclusively during testing.
- Restart OBS and inspect the Journal again. If TLS is available but the camera is unreachable, check the IP, LAN connectivity and TCP port 13496 using PowerShell: `Test-NetConnection CAMERA_IP -Port 13496`.

## Instalare și depanare (Română)

1. Descarcă arhiva Windows x64 din Releases și dezarhiveaz-o.
2. Închide OBS complet. Copiază DLL-ul pluginului în `C:\Program Files\obs-studio\obs-plugins\64bit\`. Păstrează structura celorlalte directoare din pachet, dacă există.
3. Pornește OBS și deschide **Docks → Sab Sound Cisco Precision 60 PTZ**.
4. În Settings selectează Română, introdu IP-ul camerei, acceptă certificatul neverificat numai în rețeaua locală de încredere și apasă Conectare.

Dacă pluginul nu apare, verifică **Help → Log Files → View Current Log** și compatibilitatea x64.

Dacă apare eroarea TLS:
- Verifică în Jurnal versiunea Qt, backend-urile TLS și căile de căutare.
- În testele noastre cu OBS 32.2.2 am folosit Qt 6.11.1 x64. Bibliotecile TLS compatibile au fost plasate în `C:\Program Files\obs-studio\bin\64bit\tls\`.
- Descarcă distribuția Qt base Windows x64 corespunzătoare versiunii raportate, din [arhiva oficială Qt](https://download.qt.io/). Caută directorul `plugins/tls` și copiază bibliotecile backend TLS compatibile în directorul OBS indicat, cu OBS închis. Fă o copie de siguranță a fișierelor existente.
- Unele backend-uri necesită dependențe suplimentare. Nu înlocui bibliotecile Qt principale ale OBS și nu amesteca versiuni. Combinația exactă de backend și dependențe din testul nostru nu a fost consemnată complet.
- Repornește OBS și verifică Jurnalul. Dacă TLS funcționează, verifică IP-ul și portul 13496 cu PowerShell: `Test-NetConnection IP_CAMERA -Port 13496`.

Utilizează pluginul numai într-o rețea locală de încredere. Nu expune portul camerei la internet.
