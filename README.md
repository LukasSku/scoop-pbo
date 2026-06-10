# 🔥 Pokemon Blaze Online — Scoop Bucket

> Install, update, and manage **Pokemon Blaze Online** on Windows with a single command — no manual downloads, no installers, no hassle.

This is the official [Scoop](https://scoop.sh) bucket (package repository) for **Pokemon Blaze Online (PBO)**. It lets you install and maintain the PBO Launcher & Game Client entirely from PowerShell.

---

## 📖 Table of Contents

- [What Is Scoop?](#-what-is-scoop)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Updating the Game](#-updating-the-game)
- [Uninstalling](#-uninstalling)
- [What Gets Installed?](#-what-gets-installed)
- [Persisted Data](#-persisted-data)
- [How Auto-Updates Work](#-how-auto-updates-work)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Project Structure](#-project-structure)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🧰 What Is Scoop?

[Scoop](https://scoop.sh) is a **command-line package manager for Windows** — similar to `apt` on Linux or `brew` on macOS. Instead of downloading `.exe` installers from websites, Scoop:

| Benefit | Description |
|---|---|
| **Clean installs** | Everything lives inside `C:\Users\<YourName>\scoop` — nothing is scattered across your system or written to the registry. |
| **One-command updates** | Run `scoop update <app>` and you're on the latest version. |
| **Easy rollback** | Something broke? Roll back to the previous version instantly. |
| **No admin required** | Scoop installs in user-space, so you never need "Run as Administrator". |
| **Persisted data** | Your personal config and logs survive updates automatically. |

---

## ✅ Prerequisites

- **Windows 10** or later (64-bit)
- **PowerShell 5.1+** (pre-installed on Windows 10/11)
- An active internet connection

---

## 🚀 Quick Start

### Step 1 — Install Scoop (skip if you already have it)

Open **PowerShell** and run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

> **What does this do?**
> - The first line allows PowerShell to run scripts downloaded from the internet (required by Scoop).
> - The second line downloads and executes the Scoop installer.

You can verify the installation by running:

```powershell
scoop help
```

### Step 2 — Add the PBO bucket

A "bucket" in Scoop is a repository of package definitions. You only need to add it **once**:

```powershell
scoop bucket add scoop-pbo https://github.com/LukasSku/scoop-pbo.git
```

### Step 3 — Install the game

```powershell
scoop install pbo
```

That's it! Scoop will:
1. Download the latest PBO release (`.zip`) from the official server.
2. Verify the download's integrity using a SHA-256 hash.
3. Extract it into your Scoop apps directory.
4. Create a **Start Menu shortcut** called "Pokemon Blaze Online".
5. Add `pbo.exe` and `pbo_no_updater.exe` to your system `PATH`.

You can now launch the game by:
- Clicking the **"Pokemon Blaze Online"** shortcut in the Start Menu, **or**
- Running `pbo` in any terminal.

---

## 🔄 Updating the Game

When a new version is available, simply run:

```powershell
scoop update pbo
```

To update **Scoop itself** and all buckets first (recommended):

```powershell
scoop update
scoop update pbo
```

> **Note:** Your personal configuration (`config.json`) and `logs` folder are **persisted** — they will never be overwritten by an update.

---

## 🗑️ Uninstalling

To completely remove PBO from your system:

```powershell
scoop uninstall pbo
```

This removes the game files and shortcuts but keeps your Scoop installation intact.

To also remove the bucket:

```powershell
scoop bucket rm scoop-pbo
```

---

## 📦 What Gets Installed?

| File / Component | Description |
|---|---|
| `pbo.exe` | The main launcher with auto-updater — **this is what you'll normally use**. |
| `pbo_no_updater.exe` | A standalone game client without the built-in updater. Useful if you prefer Scoop to handle updates. |
| Start Menu shortcut | Points to `pbo.exe` for easy access. |

**Default install location:**

```
C:\Users\<YourName>\scoop\apps\pbo\current\
```

---

## 💾 Persisted Data

Scoop's `persist` feature ensures the following files/folders survive across updates and reinstalls:

| Path | Purpose |
|---|---|
| `config.json` | Your personal game configuration (settings, preferences). |
| `logs/` | Game log files for debugging. |

These are symlinked from the Scoop persist directory:

```
C:\Users\<YourName>\scoop\persist\pbo\
```

You can safely back up this folder to preserve your settings.

---

## ⚙️ How Auto-Updates Work

This repository includes a **GitHub Actions workflow** that runs automatically **every 6 hours**. Here's what it does:

1. Downloads the latest PBO release from the official server.
2. Computes a SHA-256 hash of the downloaded file.
3. Compares it against the hash stored in [`bucket/pbo.json`](bucket/pbo.json).
4. If the hash has changed (meaning a new version was released), it updates the manifest and pushes the change.

This means the Scoop bucket always stays in sync with the latest PBO release — **no manual intervention needed**.

---

## 🔧 Troubleshooting

### "Running scripts is disabled on this system"

Run this in PowerShell before installing Scoop:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Hash check failed during install

This usually means a new game version was just released and the manifest hasn't been updated yet. The auto-update workflow runs every 6 hours. You can either:

- Wait a few hours and try again.
- [Open an issue](https://github.com/LukasSku/scoop-pbo/issues) asking for an immediate update.

### The game won't launch

1. Make sure your antivirus isn't blocking `pbo.exe`.
2. Try running the game from PowerShell to see any error output:
   ```powershell
   pbo
   ```
3. Check the log files in `C:\Users\<YourName>\scoop\persist\pbo\logs\`.

### Scoop command not found

If `scoop` isn't recognized after installation, close and reopen your PowerShell window or run:

```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","User")
```

---

## ❓ FAQ

**Q: Do I need admin privileges?**
No. Scoop and PBO install entirely in your user directory.

**Q: Can I use the built-in PBO updater alongside Scoop?**
Yes — `pbo.exe` includes its own updater. However, if you prefer to manage updates through Scoop, you can use `pbo_no_updater.exe` instead.

**Q: Where does the game download come from?**
The official PBO download server hosted on Backblaze B2 (`pbo-downloads.s3.eu-central-003.backblazeb2.com`).

**Q: How do I check which version I have installed?**
```powershell
scoop info pbo
```

**Q: Can I install PBO alongside a manual (non-Scoop) installation?**
Yes, but you'll have two separate copies of the game. They won't interfere with each other.

---

## 📂 Project Structure

```
scoop-pbo/
├── bucket/
│   └── pbo.json              # Scoop manifest — defines version, download URL, hash, etc.
├── .github/
│   └── workflows/
│       └── main.yml           # GitHub Actions workflow for auto-updating the hash
└── README.md                  # This file
```

### `bucket/pbo.json` — The Manifest

This is the core of the Scoop bucket. It tells Scoop:

- **Where** to download the game from (`url`)
- **How** to verify the download (`hash` — SHA-256)
- **What** to extract (`extract_dir`)
- **Which** executables to add to your PATH (`bin`)
- **What** shortcuts to create (`shortcuts`)
- **Which** files to preserve across updates (`persist`)

---

## 🤝 Contributing

Found a bug or want to improve something? Contributions are welcome!

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/my-improvement`)
3. Commit your changes (`git commit -m "Add my improvement"`)
4. Push to your branch (`git push origin feature/my-improvement`)
5. Open a Pull Request

---

## 📄 License

The Scoop bucket configuration files in this repository are provided as-is. Pokemon Blaze Online itself is proprietary software — see [pokemonblazeonline.com](https://pokemonblazeonline.com) for details.
