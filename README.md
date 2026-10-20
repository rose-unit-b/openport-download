# Install openport - rose

openport - rose opens the rose portal (GitLab, Argo CD, Keycloak, ...) from your computer.
You install it once, sign in with your AWS user, press **Connect** and then **Open portal**.
You don't need a terminal, the AWS CLI or any scripts.

> No GitHub account is needed to download. To connect you need an **AWS user in the rose
> account** with the tunnel permission; if you don't have one, ask your team lead.

## 1. Download

Pick your system. These links always give you the newest version:

| System | Download |
|---|---|
| **Windows 10 / 11** (64-bit) | [openport-rose-windows-setup.exe](https://github.com/rose-unit-b/openport-download/releases/latest/download/openport-rose-windows-setup.exe) |
| **macOS 11+** (Intel and Apple Silicon) | [openport-rose-macos.pkg](https://github.com/rose-unit-b/openport-download/releases/latest/download/openport-rose-macos.pkg) |
| **Ubuntu 22.04+ / Debian 12+** | [openport-rose-linux-amd64.deb](https://github.com/rose-unit-b/openport-download/releases/latest/download/openport-rose-linux-amd64.deb) |
| **Fedora / RHEL-like** | [openport-rose-linux-amd64.rpm](https://github.com/rose-unit-b/openport-download/releases/latest/download/openport-rose-linux-amd64.rpm) |

All files and their SHA-256 checksums are on the [Releases page](https://github.com/rose-unit-b/openport-download/releases/latest).

## 2. Install

You need admin rights on your computer **once**, during the install. The installer adds:
the app, AWS's Session Manager component, the rose certificate (`RED-ROOT-CA`),
the `*.rose.localhost` names, and (macOS and Linux only) permission to use port 443.

### Windows
The app has no paid code-signing certificate, so the browser and Windows warn that it is
"not commonly downloaded" or from an "unknown publisher". This is expected; the steps below get past it.

1. **Keep the download.** If the browser holds the file back:
   - **Edge:** in the downloads list, hover over the file → **⋯** → **Keep** → **Show more** → **Keep anyway**.
   - **Chrome:** in the downloads list, click **Keep** (or **⋯** → **Download suspicious file**).
2. *(Optional, to be sure the file is genuine)* In PowerShell:
   `Get-FileHash $HOME\Downloads\openport-rose-windows-setup.exe` and compare the hash with the
   `.exe` line in `SHA256SUMS.txt` on the [Releases page](https://github.com/rose-unit-b/openport-download/releases/latest)
   (upper/lower case does not matter).
3. Double-click `openport-rose-windows-setup.exe`. Windows shows **"Windows protected your PC"**:
   click **More info**, then **Run anyway**. (If you see no **Run anyway** button: right-click the file →
   **Properties** → tick **Unblock** at the bottom → **OK**, then double-click it again.)
4. Click **Yes** when Windows asks to allow changes, then **Next**, then **Finish**.
   The app starts, and it also has a desktop shortcut.

If your computer is managed by an organization that blocks unknown programs entirely, ask its IT
administrator to allow the file, or use another computer.

### macOS
1. Double-click `openport-rose-macos.pkg` (Safari saves it in **Downloads**).
2. macOS will say it **"cannot verify"** the package. Click **Done** (not "Move to Trash").
3. Open **System Settings → Privacy & Security**. Scroll down to the message about
   *openport-rose-macos.pkg* and click **Open Anyway**, then enter your password.
4. Follow the installer (Continue → Install) and enter your Mac password when it asks.
5. Start **openport-rose** from Applications (or Launchpad).

### Ubuntu / Debian
1. Double-click `openport-rose-linux-amd64.deb`. It opens in your software installer
   (App Center or Software). Click **Install** and enter your password.
   If double-clicking opens an archive viewer instead, right-click the file → **Open With** → **App Center**
   (or **Software Install**).
2. Start **openport - rose** from your app menu.

### Fedora / RHEL-like
1. Double-click `openport-rose-linux-amd64.rpm` (it opens in **Software**). Click **Install**.
2. Start **openport - rose** from your app menu.

## 3. First use

1. **AWS account.** Click **Sign in with AWS**. Your browser opens the AWS sign-in page. Check that the code
   matches the one shown in the app, then approve. The app shows *Signed in as …*.
   - If you have more than one role, the app asks which one to use. It remembers your choice.
   - This is the same AWS access portal (`https://d-ce672930af.awsapps.com/start`) you may already use.
   - **Other ways to sign in** also work: an existing AWS profile on your computer, or the temporary keys
     from the access portal (*Access keys → copy*). The app keeps pasted keys in memory only and forgets
     them when it closes.
2. **Connection.** Click **Connect**. After a few seconds the status changes to **Connected via relay 1**
   (or 2).
3. Click **OPEN PORTAL**. The portal opens in your normal browser. The **GitLab**, **Argo CD** and **Keycloak** buttons
   open those services directly.

Keep the app open while you work. Closing it closes the tunnel, and the app asks before it does. If the
connection drops (for example after 20 minutes without traffic), the app reconnects by itself.

## 4. If something is wrong

The **This computer** section checks your setup. Each line shows ✓ (fine), **!** (works partly) or ✕ (must
be fixed), and most problems have a **Fix** button.

| You see | What to do |
|---|---|
| *rose certificate … not trusted* | Click **Trust**. Windows or macOS asks you to confirm. Then restart your browser. |
| *another program already uses port 443* | Something else on your computer uses that port, for example a local web server or Docker. Stop it, then click **Check again**. |
| *Linux only lets the tunnel use port 443 after a one-time permission* | Click **Fix** and enter your password. |
| *the redirect from port 443 is not installed* (macOS) | Click **Fix** and enter your Mac password. |
| *not allowed to open the tunnel* | Your AWS user lacks the tunnel permission. Ask your team lead. |
| *your AWS sign-in expired* | Click **Sign out**, then **Sign in with AWS** again. |
| Browser shows *Your connection is not private* | Fix the certificate line above, then restart the browser completely. |
| Anything else | Click **Copy diagnostics** at the bottom and paste it in a message to the network team. It contains no passwords or keys. |

## 5. Update

When a newer version exists, the app shows **"A new version is available - Download"**. Download it and
install it over the old one, using the same steps as above. Your settings are kept.

## 6. Uninstall

- **Windows:** Settings → Apps → *openport - rose* → Uninstall.
- **macOS:** open the app and click **Uninstall** at the bottom (asks for your Mac password).
- **Linux:** remove *openport - rose* in your software manager (App Center / Software).

Uninstalling also removes the rose certificate, the port setting and the `*.rose.localhost` names.
