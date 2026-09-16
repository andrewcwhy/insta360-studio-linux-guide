# Install Insta360 Studio on Linux with Wine

<p align="center">
  <img src="insta360-studio-icon.jpg" width="96" alt="Insta360 Studio icon">
</p>

This guide explains how to install the Windows version of Insta360 Studio on Ubuntu-based Linux distributions using Wine. It was tested with Insta360 Studio v6.0.5.

> [!IMPORTANT]  
> Insta360 Studio does not officially support Linux, so some features may not work correctly through Wine.

This guide uses Wine’s default prefix:

```
~/.wine
```

Winetricks changes will also affect other Windows applications installed in this prefix.

## 1. Install Wine and Winetricks

```bash
sudo apt install wine winetricks
```

## 2. Check for `vcrun2026`

```
winetricks list-all | grep vcrun2026
```

If `vcrun2026` appears, continue to the next section. Otherwise, update Winetricks:

```
sudo winetricks --self-update
```

Check again:

```
winetricks list-all | grep vcrun2026
```

> [!WARNING]  
> This replaces Ubuntu’s packaged Winetricks script with the upstream version. A future package update may replace it again.

## 3. Install the Compatibility Components

```bash
winetricks allfonts dxvk vcrun2026
```

These components provide:

- `vcrun2026`: Microsoft Visual C++ runtime libraries.
- `allfonts`: Windows fonts required by the Qt interface.
- `dxvk`: Vulkan-based Direct3D support for AMD, Intel, and NVIDIA GPUs.

## 4. Download Insta360 Studio

Download Insta360 Studio for Windows from the official website:

[Download Insta360 Studio](https://www.insta360.com/download/hot-download)

This guide assumes the installer is named:

```text
Insta360_Studio_6.0.5.exe
```

and saved in:

```text
~/Downloads
```

## 5. Install Insta360 Studio

```bash
wine "$HOME/Downloads/Insta360_Studio_6.0.5.exe"
```

Keep the default installation location. On the **Additional Tasks** screen, I personally left **Create a desktop shortcut** selected and cleared the remaining optional items:

- **Windows Firewall whitelist:** Unnecessary because Wine uses the Linux host’s networking and firewall.
- **File associations:** Optional because files can be opened from inside Insta360 Studio.
- **QuickLook and thumbnail plugins:** Add file previews and thumbnails to Windows file managers but does not integrate with Linux file managers through Wine.

## 6. Launch Insta360 Studio

Open Insta360 Studio normally or launch it through Wine:

```bash
wine "$HOME/.wine/drive_c/Program Files/Insta360 Studio/Insta360 Studio.exe"
```

If Insta360 Studio opens normally, the installation is complete.

## 7. Remove the Downloaded Installer

After confirming that Insta360 Studio launches correctly, delete the installer:

```bash
rm "$HOME/Downloads/Insta360_Studio_6.0.5.exe"
```
