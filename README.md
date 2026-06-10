# 🔥 Pokemon Blaze Online — Scoop Installer

Install and update **Pokemon Blaze Online** on Windows with a single command — no manual downloads needed.

---

## What Is Scoop?

[Scoop](https://scoop.sh) is a package manager for Windows. It installs apps cleanly in your user folder — no admin rights, no registry clutter. Think of it like an app store you control from PowerShell.

---

## Installation

### 1. Install Scoop (only once)

Open **PowerShell** and run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

### 2. Add the PBO bucket (only once)

```powershell
scoop bucket add scoop-pbo https://github.com/LukasSku/scoop-pbo.git
```

### 3. Install the game

```powershell
scoop install pbo
```

✅ Done! A **Start Menu shortcut** ("Pokemon Blaze Online") is created automatically. You can also type `pbo` in any terminal to launch the game.

---

## Updating

When a new game update is released, run:

```powershell
scoop update
scoop update pbo
```

> **Important:** Always run `scoop update` first — this syncs the bucket so Scoop knows about the latest version. Then `scoop update pbo` downloads and installs it.

Your personal settings (`config.json`) and log files are **never** overwritten by updates.

---

## Uninstalling

```powershell
scoop uninstall pbo
```

To also remove the bucket:

```powershell
scoop bucket rm scoop-pbo
```

---

## Troubleshooting

| Problem | Solution |
|---|---|
| "Running scripts is disabled" | Run `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` first |
| Hash check failed | A new version was just released — wait a few hours for the auto-update or [open an issue](https://github.com/LukasSku/scoop-pbo/issues) |
| Game won't launch | Check if your antivirus is blocking `pbo.exe` |
| `scoop` not found | Close and reopen PowerShell |

---

## How It Works

This repository contains a Scoop manifest ([`bucket/pbo.json`](bucket/pbo.json)) that tells Scoop where to download PBO and how to verify it. A GitHub Actions workflow checks every 6 hours if a new version was released and updates the manifest automatically.

---

## License

The Scoop bucket files are provided as-is. Pokemon Blaze Online itself is proprietary — see [pokemonblazeonline.com](https://pokemonblazeonline.com).
