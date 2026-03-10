# copyq-qrcode

CopyQ commands for generating QR codes from clipboard text entries.

Right-click any text item in CopyQ and instantly generate a QR code — copied to your clipboard or saved as a PNG file.

## Features

- **Generate (to clipboard)** — creates a QR code PNG and copies it to your clipboard, ready to paste
- **Generate (show)** — opens the QR code in your default image viewer for easy scanning
- **Generate (save to file)** — saves the QR code as a PNG file with a hash + timestamp filename
- **Configure** — set pixel size, error correction level, and default save folder

## Requirements

- CopyQ **9.0+**
- **qrencode** — a lightweight QR code encoder available on all major platforms:

| OS | Install |
|---|---|
| Debian/Ubuntu | `sudo apt install qrencode` |
| Fedora | `sudo dnf install qrencode` |
| Arch | `sudo pacman -S qrencode` |
| macOS | `brew install qrencode` |
| Windows | `choco install qrencode-windows` or [download binary](https://fukuchi.org/works/qrencode/) |

## Install

### Option 1: GUI

1. Copy the contents of `qrcode-commands.ini` to your clipboard
2. Open CopyQ → press **F6** (Command dialog)
3. Click **Paste Commands**
4. Click **OK**

### Option 2: CLI

```bash
curl -s https://raw.githubusercontent.com/thereisnotime/copyq-qrcode/master/qrcode-commands.ini | \
  copyq eval 'var nc = importCommands(input()); var e = commands(); for (var i = 0; i < nc.length; i++) e.push(nc[i]); setCommands(e);'
```

### Option 3: Load from file

```bash
git clone https://github.com/thereisnotime/copyq-qrcode.git
cat copyq-qrcode/qrcode-commands.ini | \
  copyq eval 'var nc = importCommands(input()); var e = commands(); for (var i = 0; i < nc.length; i++) e.push(nc[i]); setCommands(e);'
```

## Configuration

Default settings work out of the box. You can tweak them via **QR Code → Configure...**:

- **Pixel size** — size of each QR module in pixels (default: 10)
- **Error correction** — L (7%), M (15%), Q (25%), H (30%) — higher means more readable when damaged but larger codes (default: M)
- **Default save folder** — where "save to file" starts (default: `~/Documents`)

Settings are stored using CopyQ's `settings()` API under the `qrcode/` namespace.

## Update

```bash
copyq eval 'var c = commands(); var keep = []; for (var i = 0; i < c.length; i++) { if (String(c[i].name).indexOf("QR Code") < 0) keep.push(c[i]); } setCommands(keep);' && \
curl -s https://raw.githubusercontent.com/thereisnotime/copyq-qrcode/master/qrcode-commands.ini | \
  copyq eval 'var nc = importCommands(input()); var e = commands(); for (var i = 0; i < nc.length; i++) e.push(nc[i]); setCommands(e);'
```

## Uninstall

### CLI

```bash
copyq eval 'var c = commands(); var keep = []; for (var i = 0; i < c.length; i++) { if (String(c[i].name).indexOf("QR Code") < 0) keep.push(c[i]); } setCommands(keep);'
```

### GUI

Open CopyQ → **F6** → select and delete all commands starting with "QR Code|".
