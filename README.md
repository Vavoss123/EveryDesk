# EveryDesk

EveryDesk is a free remote desktop app for Windows that I built so I could help friends and family with their
computers without any of the hassle. You share your screen with someone, and if you want, you let them use your
mouse and keyboard too. Nothing happens unless you say yes, and you can take control back whenever you like.

It's still early. It works well between two copies of the app, but I'm only now testing it between different
houses, so expect a few rough edges.

## Getting it

Go to the [Releases page](../../releases) and download `EveryDesk-Setup-1.0.0-x64.exe`.

If you want to check you've got the real file (worth doing, see below), open PowerShell in your Downloads folder and run:

```powershell
Get-FileHash -Algorithm SHA256 .\EveryDesk-Setup-1.0.0-x64.exe
```

It should match the code on the release page. If it doesn't, delete the file.

## Installing it

Just run the installer. You don't need admin rights or anything else installed.

One heads up: I haven't paid for a code-signing certificate yet, so Windows will probably say "Windows protected
your PC" and call me an unknown publisher. If you trust the download (and the checksum matched), click
**More info** then **Run anyway**. If your PC has Smart App Control turned on, Windows won't let you run it at all,
and I can't do anything about that until the app is signed.

Once it's installed, open EveryDesk from the Start menu. After a few seconds it should say **Online** and show you
your device ID.

To get rid of it, uninstall it from Settings > Apps. Your device ID sticks around unless you also delete
`%APPDATA%\EveryDesk`.

## Using it

1. You both open EveryDesk and wait for **Online**.
2. Whoever wants to look at the other screen types in the other person's device ID, picks **View only** or
   **View and control**, and hits **Request access**.
3. The other person gets a pop-up. They check the ID is who they expect, press **Allow**, pick a screen or window
   and press **Share**. Nothing is captured before that.
4. You'll both see a nine-digit safety code. Read it out to each other over the phone. If it's not the same on
   both screens, stop sharing, because something's wrong.
5. If they asked for control, the person sharing gets a second prompt to allow it. They can take it back any time
   with **Revoke control** or by pressing **Ctrl+Alt+Shift+R**.
6. Hit **Stop sharing** (or **Disconnect**) when you're done. Next time, you ask again.

## Privacy

I wanted this to be something I'd actually trust, so:

- Every session needs the person at the computer to approve it, every single time. There's no way to leave it
  running for someone to dip into later.
- Your screen and any mouse or keyboard input go straight between the two computers, encrypted. They don't go
  through my server.
- The server is only there to introduce the two apps to each other. It can see device IDs, IP addresses and who's
  trying to connect to whom, and it keeps logs for three days. It can't see your screen or what you type, and it
  can't approve anything for you.
- The safety code is how you know you're talking to the right person and nobody's sitting in the middle.

## What it can't do (yet)

- It needs Windows 10 or 11, 64-bit. I've only tested it properly on Windows 11.
- Connections go directly between the two computers, and I haven't set up a relay server. Some stricter networks
  (some mobile and shared connections) might not be able to connect.
- Windows doesn't let any app control programs running as administrator, the lock screen, UAC prompts, or
  Ctrl+Alt+Delete, so EveryDesk can't either.
- No file transfer, clipboard sharing or audio.
- The connection service runs on a free plan with a daily limit. If it ever runs out, the app will tell you and
  carry on working again after midnight UTC.

## Licence

It's free to download and use. The source code isn't in this repo. The app does include some open source parts
(Electron and Chromium, React, ws and zod), and their licences are installed alongside it in the files
`THIRD-PARTY-NOTICES.txt`, `LICENSE.electron.txt` and `LICENSES.chromium.html`.
