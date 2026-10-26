# EveryDesk

Free, consent-based remote desktop for Windows. One person shares their screen, and if they choose, lets the
other person use their mouse and keyboard. Nothing is shared without the host's approval, and the host can take
control back at any moment.

> **1.0.0 is a pre-release.** It works between two EveryDesk apps through the live connection service, but testing
> between computers in different homes is still under way. The installer is not code-signed yet, so Windows will
> warn about it (see below).

## Download

Get **`EveryDesk-Setup-1.0.0-x64.exe`** from the [Releases page](../../releases). Before running it, check that the
file is exactly the one published, in PowerShell from your Downloads folder:

```powershell
Get-FileHash -Algorithm SHA256 .\EveryDesk-Setup-1.0.0-x64.exe
```

The result must match the SHA-256 shown on the release page and in the `.sha256` file. If it differs, delete the file.

## Install

1. Run the installer as your normal Windows user. No administrator rights or other software are needed.
2. Because the installer is not signed, Windows may show **Windows protected your PC** (Unknown publisher).
   **More info → Run anyway** runs it; that is your choice to make. On PCs with **Smart App Control** turned on,
   Windows blocks unsigned apps completely; EveryDesk cannot be installed there until it is signed.
3. Open **EveryDesk** from the Start menu. It connects by itself and shows your **device ID**.

To remove it: **Settings → Apps → Installed apps → EveryDesk → Uninstall**. Your device ID is kept unless you also
delete `%APPDATA%\EveryDesk`.

## Connect

1. Both people open EveryDesk and wait for **Online**.
2. Send your device ID to the other person (use **Copy**). Only share it with people you trust.
3. The person who wants to see the other screen enters the other ID, chooses **View only** or **View and control**,
   and presses **Request access**.
4. The other person checks the ID in the prompt, presses **Allow**, then picks a screen or window and presses
   **Share**. Nothing is shared before that.
5. Read the nine-digit **safety code** to each other, for example on a phone call. If the codes differ, stop sharing.
6. For control, the viewer presses **Request control** and the host allows it. The host can press
   **Revoke control** or **Ctrl+Alt+Shift+R** at any time.
7. **Stop sharing** or **Disconnect** ends the session. Every new session needs a new request and approval.

## Safety and privacy

- There is no unattended access: every session must be approved by the person at the computer, every time.
- Screens, mouse and keyboard travel directly between the two computers, end-to-end encrypted. They never pass
  through the EveryDesk connection service.
- The connection service (on Cloudflare) introduces the two computers. It sees device IDs, IP addresses and who
  asks to connect to whom, and keeps logs for three days. It cannot see screens or input, and cannot approve access.
- The safety code proves you are connected directly to each other, with nobody in between.

## Requirements and limits

- Windows 10 or 11, 64-bit. Tested on Windows 11.
- Connections are direct between the two networks. Some strict networks (some mobile and shared networks) may not
  be able to connect; there is no relay server.
- Windows does not allow remote control of programs running as administrator, the lock screen, UAC prompts or
  Ctrl+Alt+Delete.
- Not included: file transfer, clipboard sharing, audio, unattended access, automatic updates.
- The free connection service has a daily limit. If it is reached, the app says so and connects again after
  midnight UTC.

## Licence

EveryDesk is free to download and use. Its source code is not published in this repository. The app includes
third-party software (Electron and Chromium, React, ws, zod) under their own licences; their notices are installed
with the app (`THIRD-PARTY-NOTICES.txt`, `LICENSE.electron.txt`, `LICENSES.chromium.html`).
