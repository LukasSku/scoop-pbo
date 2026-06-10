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

1. Open Windows PowerShell (Press the Windows Key, type "powershell", and hit Enter).
2. PowerShell needs permission to execute the installer script. Run this command first:
   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
