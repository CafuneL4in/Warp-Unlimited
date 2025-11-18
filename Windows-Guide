# ⚙️ Warp AI Unlimited — Full Cleanup & Fresh Account Setup Guide

This guide walks you through performing a complete cleanup of Warp from your system to start fresh with a new account.  
All steps are fully self-contained and designed to ensure no leftover data remains.

---

## 1. Log Out from Warp Website
- Open the Warp website.
- Log out of your current account.
- Close your browser to clear any active session.

---

## 2. Uninstall the Warp Application
- Go to **Settings → Apps → Installed Apps**
- Find **Warp**
- Select **Uninstall** and confirm

This removes the main program but not hidden leftovers.

---

## 3. Clean Warp Local Data, Configs & Services
Run the following command in **PowerShell as Administrator** to remove any remaining Warp directories:

### 🔧 System Cleanup Command

# Search common locations for Warp leftovers
$searchPaths = @(
  "C:\Program Files",
  "C:\Program Files (x86)",
  "$env:LOCALAPPDATA",
  "$env:APPDATA",
  "C:\Users\Public"
)

foreach ($sp in $searchPaths) {
    Write-Output "Searching $sp for Warp files..."
    Get-ChildItem -Path $sp -Recurse -Force -ErrorAction SilentlyContinue -Include *Warp* |
        ForEach-Object {
            try {
                Write-Output "Deleting: $($_.FullName)"
                Remove-Item -Path $_.FullName -Recurse -Force
            } catch {
                Write-Output "Could not delete: $($_.FullName) - $($_.Exception.Message)"
            }
        }
}


---


### ⚡ Fast Clean (Recommended)
# Run in PowerShell as Administrator
Write-Host "Starting Fast Warp Registry Cleanup..." -ForegroundColor Cyan

# Specific known locations (Fast)
$warpKeys = @(
    "HKCU:\Software\Warp",
    "HKLM:\SOFTWARE\Warp",
    "HKCU:\Software\Microsoft\Windows\CurrentVersion\Uninstall\Warp*",
    "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Warp*",
    "HKCU:\Software\WOW6432Node\Warp",
    "HKLM:\SOFTWARE\WOW6432Node\Warp"
)

$deleted = 0
foreach ($key in $warpKeys) {
    try {
        if (Test-Path $key) {
            Write-Host "Deleting: $key" -ForegroundColor Yellow
            Remove-Item -Path $key -Recurse -Force -ErrorAction Stop
            $deleted++
        }
    } catch {
        Write-Host "Failed to delete: $key" -ForegroundColor Red
    }
}

# Check Run keys for Warp entries
$runKeys = @(
    "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run",
    "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"
)

foreach ($runKey in $runKeys) {
    try {
        $props = Get-ItemProperty -Path $runKey -ErrorAction SilentlyContinue
        $props.PSObject.Properties | Where-Object { $_.Name -match "Warp" -and $_.Name -ne "PSPath" } | ForEach-Object {
            Write-Host "Removing Run entry: $($_.Name)" -ForegroundColor Yellow
            Remove-ItemProperty -Path $runKey -Name $_.Name -Force -ErrorAction Stop
            $deleted++
        }
    } catch {}
}

# Limited targeted search (only likely locations - Much Faster)
$targetPaths = @(
    "HKCU:\Software",
    "HKLM:\SOFTWARE",
    "HKCU:\Software\Microsoft\Windows\CurrentVersion\Uninstall",
    "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall"
)

Write-Host "`nSearching common locations for Warp entries..." -ForegroundColor Cyan

foreach ($path in $targetPaths) {
    try {
        Get-ChildItem -Path $path -ErrorAction SilentlyContinue -Depth 1 |
            Where-Object { $_.PSChildName -match "Warp" } |
            ForEach-Object {
                try {
                    Write-Host "Deleting: $($_.PSPath)" -ForegroundColor Yellow
                    Remove-Item -Path $_.PSPath -Recurse -Force -ErrorAction Stop
                    $deleted++
                } catch {}
            }
    } catch {}
}

Write-Host "`n=== Cleanup Complete ===" -ForegroundColor Green
Write-Host "Total items deleted: $deleted" -ForegroundColor Green


### 🔍 Deep Clean (Optional)
# Run in PowerShell as Administrator

$warpKeys = @(
  "HKCU:\Software\Warp",
  "HKLM:\SOFTWARE\Warp",
  "HKCU:\Software\Microsoft\Windows\CurrentVersion\Uninstall\Warp*",
  "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Warp*",
  "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run",
  "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"
)

foreach ($key in $warpKeys) {
    try {
        # Find matching keys
        $matches = Get-ItemProperty -Path $key -ErrorAction SilentlyContinue | Out-String
        if ($matches -match "Warp") {
            Write-Output "Deleting registry key: $key"
            Remove-Item -Path $key -Recurse -Force -ErrorAction SilentlyContinue
        }
    } catch {}
}

# Extra: search entire registry for "Warp" (this takes time)
Write-Output "Searching registry for 'Warp' entries..."
Get-ChildItem -Path HKCU:\, HKLM:\ -Recurse -ErrorAction SilentlyContinue |
    Where-Object { $_.Name -match "Warp" } |
    ForEach-Object {
        try {
            Write-Output "Deleting: $($_.Name)"
            Remove-Item -Path $_.PsPath -Recurse -Force -ErrorAction SilentlyContinue
        } catch {}
    }

Write-Output "Warp registry cleanup completed!"

---

## 5. Generate a Temporary Email
- Visit a temporary email service (e.g., Temp-Mail)
- If you used temp-mail before, clear the website’s **local storage** first.

This ensures you don’t get an email previously associated with Warp.

---

## 6. Create a New Warp Account
- Sign up using the temporary email address
- Complete verification if required
- Avoid using any previous Warp details

---

## 7. Reinstall Warp & Sign In
- Download the latest Warp installer
- Install normally
- Log in using your new temporary email address

You should now have a fresh, clean Warp installation.

---

# 🎉 Setup Complete!
After following these steps, you successfully:
- Removed all Warp leftover files
- Cleared system & registry traces
- Generated a new email identity
- Reinstalled Warp from scratch

---

# ⚠️ Important Notes
- Always run PowerShell as **Administrator**
- Restart your PC after registry cleanup
- Temporary emails should be used **only** for creating new Warp accounts
- Deep clean is optional but more thorough

