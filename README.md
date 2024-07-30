# FixHub

Welcome to FixHub! This repository is dedicated to providing fixes, workarounds, helps, and documentation for common technical issues. Our goal is to help users troubleshoot and resolve their technical problems efficiently.

## Contents

- [Windows Fixes](#windows-fixes)

## Windows Fixes

### Fix: Winget on Windows 11 Displays Backslashes and Changes Prompt Color to Blue

I have installed Windows 11, which includes Winget version 1.2.10691. This version is unable to install packages, instead displaying backslash and changing the prompt color to blue. When I run the following command to update winget:

```powershell
Add-AppxPackage -RegisterByFamilyName -MainPackage Microsoft.DesktopAppInstaller_8wekyb3d8bbwe
```

I received the following response:
```
Add-AppxPackage : Deployment failed with HRESULT: 0x80073D02, The package could not be installed because resources it
modifies are currently in use.
error 0x80073D02: Unable to install because the following apps need to be closed
Microsoft.DesktopAppInstaller_1.17.10691.0_x64__8wekyb3d8bbwe.
NOTE: For additional information, look for [ActivityId] 81938b14-e2ac-0000-665c-9581ace2da01 in the Event Log or use
the command line Get-AppPackageLog -ActivityID 81938b14-e2ac-0000-665c-9581ace2da01
At line:1 char:1
+ Add-AppxPackage -RegisterByFamilyName -MainPackage Microsoft.DesktopA ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (Microsoft.Deskt...r_8wekyb3d8bbwe:String) [Add-AppxPackage], Exception
    + FullyQualifiedErrorId : DeploymentError,Microsoft.Windows.Appx.PackageManager.Commands.AddAppxPackageCommand
```

The installed version does not work, and updating it is not straightforward. Here's what helped me:

1. **Download the latest version**
  - Open your web browser and go to the [Windows Package Manager GitHub Releases page](https://github.com/microsoft/winget-cli/releases).
  - On the releases page, scroll to the top to find the latest release. It will typically be marked as the "Latest release."
  - Look for the `.msixbundle` or `.appxbundle` file associated with the latest release. These files are typically named as follows:
    - `Microsoft.DesktopAppInstaller_*.msixbundle`
  - Click on the file name to start the download.

2. **Open PowerShell as Administrator**
  - Right-click the Start button and select **"Windows Terminal (Admin)"** or **"PowerShell (Admin)"**.

3. **Get the PID of running winget instance**
  - In powershell, run command:
    ```powershell
    tasklist | findstr "WindowsPackageManagerServ"     
    ```

4. **Close existing instance**
  - Replace 12820 with your PID and run:
    ```powershell
    taskkill /PID 12820 /F     
    ```

5. **Re-register the package:**
  ```powershell
  Add-AppxPackage -Register -DisableDevelopmentMode "C:\Program Files\WindowsApps\Microsoft.DesktopAppInstaller_1.17.10691.0_x64__8wekyb3d8bbwe\AppXManifest.xml"
  ```

6. **Install the Package (if needed):**
  - If you have downloaded the latest '.msixbundle' or '.appxbundle', install it using:
    ```powershell
    Add-AppxPackage -Path "C:\Path\To\Downloaded\File.msixbundle"
    ```

By following these steps, you should be able to close the Microsoft.DesktopAppInstaller application and proceed with the update or installation.

You can verify result by `winget -v`
     ```

You should see something like `v1.8.1911` or newer.
