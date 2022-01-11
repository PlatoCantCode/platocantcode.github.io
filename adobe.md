#### Adobe Reader Install (Silent and customizable  for enterprises)
1. Download the official adobe customization tool
 (https://ardownload2.adobe.com/pub/adobe/acrobat/win/AcrobatDC/misc/CustWiz2000920067_en_US_DC.exe)
 
 2. Download adobe DC reader / adobe DC pro
 Google to find latest, or go through the adobe website and use the IT Manager link.
 
 3. unzip the exe file and go into the folder that contains the MSI
 4.  edit the msi with the customization tool
 5.  Install the msi with the transform set. (/Q if quiet is desired)
```powershell
.\AcroRead.msi TRANSFORMS=acroread.mst /Q
 ```
  
 6. Open and verify it worked
 7. Update with Help - > Product updates
	 1. once downloaded (it'll be silent)
		 1. re-run help-> product updates to ensure 'install' was selected
		 2. Close out of adobe reader while install takes place
		 3. reboot machine and verify
	 2. or use update MSI's for fully automated deployment 
	 3. or use the cli for it... but this works for now



#### VDI Specifics that may be desired
 ```powershell

# Turn off license background service
# May break existing named account licensing. But is fine if just using reader
Get-Service -Name AdobeARMservice | Stop-Service
Get-Service -Name AdobeARMservice | Set-Service -StartupType Disabled

# Disable update background tasks
# USE WITH CAUTION This disables all updates
Get-ScheduledTask -TaskName "Adobe Acrobat Update Task", AdobeGCInvoker-1.0* | Disable-ScheduledTask

#VDI 
#Turn off all Document Cloud service access - READER SPECIFIC
# USE WITH CAUTION 
New-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Adobe\Acrobat Reader\DC\FeatureLockdown\cServices" -Name bToggleAdobeDocumentServices -PropertyType DWord -Value 1 -Force
```
 
 #### Extra Links
 Adobe Enterprise toolkit
 ([Enterprise Toolkit for Acrobat DC Products (adobe.com)](https://www.adobe.com/devnet-docs/acrobatetk/index.html)
 
 
 #### MST Example File that I use
 - No EULA Prompt
 - Sets default reader (stops end user prompt)
 - Sets default install location
 - silent install
 - silent install of trusted adobe certificates for product updates and online features
 - disables document cloud services
 - disables preference sync
 - ALLOWS product updates
 
Remove the .txt extension.
**example mst file below**
[AcroRead 2-remove-txt.mst.txt](https://github.com/PlatoCantCode/platocantcode.github.io/files/7848997/AcroRead.2-remove-txt.mst.txt)
