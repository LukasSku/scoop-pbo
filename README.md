# Pokemon Blaze Online (PBO) via Scoop

This repository contains the official Scoop package manifest for Pokemon Blaze Online. Using Scoop, you can install, update, and manage the PBO Launcher & Game Client directly from the Windows PowerShell—without manual zip downloads, manual extraction, or installation wizards.

---

## What is Scoop and Why Use It?

Scoop is a command-line installer (package manager) for Windows. Instead of downloading files from a website and cluttering your system registry, Scoop:
* Installs everything cleanly inside your user directory (`C:\Users\YourName\scoop`).
* Automatically sets up command-line paths and Start Menu shortcuts.
* Isolates game data so updates never overwrite your personal configurations (`config.json`) or log files.

---

## Step 1: Install Scoop (If you do not have it)

Execute this in Powershell to install Scoop
   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
   ```

   
## Step 2: Install Pokemon Blaze Online


# 1. Add the PBO bucket to your Scoop setup (only needed once)
   ```powershell
   scoop bucket add scoop-pbo [https://github.com/LukasSku/scoop-pbo.git](https://github.com/LukasSku/scoop-pbo.git)
   ```

# 2. Install the game
   ```powershell
   scoop install pbo
   ```
