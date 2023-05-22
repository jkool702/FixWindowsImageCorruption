# FixWindowsImageCorruption
Set up a scheduled task to automatically fix windows image corruption in Windows 10+

There are 3 windows commands that are very useful in automatically fixing Windows image corruption:

    dism /online /cleanup-image /restorehealth
    sfc /scannow
    chkdsk /scan /perf /forceofflinefix

You can run these commands manually in an administrator cmd/powershell prompt, OR you can use the windows task scheduler to automatically run them for you on a regular basis!

The `FixWindowsImageCorruption_DISM_SFC_CHKDSK` file contains XML to set up a windows scheduled task to run the above 3 commands automatically for you on a weekly basis (Sunday morning at 3:00 AM). You can import this XML 2 different ways:

NOTE: both ways require administrator privlidges. If you accidentally open task scheduler / powershell normally, right lick the icon for it at the bottom of the screen and hit "Run as administrator". A new instance will pop up - use the new (administrator) instance and close the old (non-administrator) instance.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

**Option 1 - Use Powershell**

Open up an administrator powershell prompt and run the following 2 commands:

    (new-object System.Net.WebClient).DownloadFile('https://raw.githubusercontent.com/jkool702/FixWindowsImageCorruption/main/FixWindowsImageCorruption_DISM_SFC_CHKDSK','C:\Windows\System32\Tasks\FixWindowsImageCorruption_DISM_SFC_CHKDSK')
    schtasks /CREATE /TN 'FixWindowsImageCorruption_DISM_SFC_CHKDSK' /XML 'C:\Windows\System32\Tasks\FixWindowsImageCorruption_DISM_SFC_CHKDSK'

Copy these 2 commands and paste them into powershell by right clicking inside the powershell window.

I reccomend this way (using powershell) - since it is basically "fool-proof" 
    
--------------------------------------------------------------------------------------------------------------------------------------------------------------

**Option 2 - Use Task Scheduler**

Download the `FixWindowsImageCorruption_DISM_SFC_CHKDSK` file, open "Task Scheduler" as an administrator, click on "Import Task" (on the right side of the window), and select the  `FixWindowsImageCorruption_DISM_SFC_CHKDSK` file that you just downloaded.

--------------------------------------------------------------------------------------------------------------------------------------------------------------

You can of course also manually setup a task to run these 3 commands (`dism`, `sfc` and `chkdsk`) if ypou prefer.
