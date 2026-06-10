# Fix WinGet Error `0x8a15005e` and Install Google Chrome

The error:

```text
Failed when searching source: msstore
0x8a15005e
```

usually indicates that WinGet cannot validate the Microsoft Store source.

## 1. Reset WinGet Sources

Open **PowerShell as Administrator** and run:

```powershell
winget source reset --force
winget source update
```

---

## 2. Check WinGet Version

```powershell
winget --version
```

If your version is old, update **App Installer** from the Microsoft Store.

---

## 3. Bypass Certificate Pinning (Temporary Workaround)

Enable the workaround:

```powershell
winget settings --enable BypassCertificatePinningForMicrosoftStore
```

Then try installing Chrome:

```powershell
winget install --id Google.Chrome --exact --source winget
```

Or search for Chrome:

```powershell
winget search chrome
```

After installation, disable the workaround:

```powershell
winget settings --disable BypassCertificatePinningForMicrosoftStore
```

---

## 4. Install Chrome Using the WinGet Repository

Avoid the Microsoft Store source:

```powershell
winget install --id Google.Chrome --exact --source winget
```

---

## 5. Install Chrome Directly (No WinGet Required)

```powershell
$installer = "$env:TEMP\ChromeSetup.exe"

Invoke-WebRequest `
    -Uri "https://dl.google.com/chrome/install/latest/chrome_installer.exe" `
    -OutFile $installer

Start-Process $installer -ArgumentList "/silent /install" -Wait
```

---

## 6. Gather Diagnostic Information

If the problem persists, collect the following:

```powershell
winget --version
winget source list
```

Share the output for further troubleshooting.

---

## Expected Result

After a successful installation, verify Chrome:

```powershell
chrome --version
```

or

```powershell
& "$env:ProgramFiles\Google\Chrome\Application\chrome.exe" --version
```
