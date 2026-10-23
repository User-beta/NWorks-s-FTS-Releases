# NWorks's File Transfer System (NWFTS)

A file transfer system that works like a phone call. You call another
computer, it rings, and once the other person answers you can send files
and folders to each other directly. Nothing is uploaded to a cloud, and the
connection is end-to-end encrypted.

Available for **Windows**, **macOS** and **Linux**.

## Download

Get the latest version from
**[Releases](https://github.com/User-beta/NWorks-s-FTS-Releases/releases/latest)**:

| System  | File to download                       |
|---------|----------------------------------------|
| Windows | `NWFTS_x.y.z_x64-setup.exe`            |
| macOS   | `NWFTS_x.y.z_universal.dmg`            |
| Linux   | `NWFTS_x.y.z_amd64.AppImage` or `.deb` |

Once installed, NWFTS updates itself: when a new version is out, it asks
before installing and never restarts during a call.

## Installing

The app is not signed with a paid certificate yet, so your system warns you
the first time.

- **Windows:** run the setup file. If "Windows protected your PC" appears,
  click **More info**, then **Run anyway**. When the firewall asks, allow
  NWFTS on **both Private and Public networks**, otherwise calls cannot reach
  you.
- **macOS:** open the `.dmg` and drag NWFTS into Applications. If macOS says
  the app cannot be opened, go to **System Settings > Privacy & Security**
  and click **Open Anyway**.
- **Linux:** for the AppImage, make it executable
  (`chmod +x NWFTS_*.AppImage`) and run it. For the `.deb`:
  `sudo apt install ./NWFTS_*_amd64.deb`.

## How it works

1. **Call.** Computers on the same network appear under *On this network*.
   For someone elsewhere, they send you their code (*Your code* on their Home
   screen) and you paste it into *Call with a code*.
2. **Answer.** The other computer rings. When answering, they choose what
   happens to files you send:
   - **Receive automatically**
   - **Ask me each time**
   - **Don't accept files**
3. **Send.** Drag files or folders onto the window, or use *Choose files* /
   *Choose folder*. Both sides can send during the call.
4. **Hang up** when you are done.

Received files go to `Downloads/NWFTS` by default; you can choose another
folder in Settings. NWFTS has to be running to receive calls; it can stay in
the system tray and start when you log in.

## Calling over the internet

Only the computer **being called** has to be reachable from the internet.
The badge at the top of the Home screen tells you whether yours is:

- **Reachable from the internet:** people can call you with your code.
- **Reachable over IPv6 only:** only people who also have IPv6 internet can
  call you.
- **Local network only:** only computers on your network can call you.

Click the badge for step-by-step help. The usual fixes are: let the other
person be the one who gets called, turn on **UPnP** on your router, forward
**UDP port 48555** to your computer, or switch on the optional **relay** in
Settings (both people need it). The relay only passes on encrypted data and
cannot read your files.

## Virus checking

Received files can be checked before they appear in your folder. Dangerous
files are moved to a quarantine folder and the sender is told.

- **Windows:** uses Microsoft Defender automatically.
- **macOS:** macOS has no virus scanner that apps can use. Install ClamAV
  with [Homebrew](https://brew.sh) and download its virus database:
  ```
  brew install clamav
  cd "$(brew --prefix)/etc/clamav"
  cp freshclam.conf.sample freshclam.conf
  sed -i '' 's/^Example/#Example/' freshclam.conf
  freshclam
  ```
- **Linux:** install ClamAV (`sudo apt install clamav`, then
  `sudo freshclam`).
- Any other antivirus with a command-line scanner can be set in Settings.

No scanner catches everything, so be careful with programs from people you
don't know.

## Privacy and security

- Files go straight from one computer to the other. By default no server is
  involved at all.
- Every connection is end-to-end encrypted (QUIC with TLS 1.3).
- Each computer has its own key. Saved contacts are recognised by that key,
  and both sides see a **verification code** during a call: if it matches on
  both screens, you are connected to the right computer.
- You can hide your computer from the local network, or allow calls from
  saved contacts only.

## Problems?

Open an [issue](https://github.com/User-beta/NWorks-s-FTS-Releases/issues)
and include your system, the NWFTS version (Settings > About) and what
happened.
