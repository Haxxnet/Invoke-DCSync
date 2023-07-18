<div align="center" width="100%">
    <h1>Invoke-DCSync</h1>
    <p>PowerShell Script to DCSync NT Password Hashes from Active Directory for Password Auditing</p><p>
    <a target="_blank" href="https://github.com/l4rm4nd"><img src="https://img.shields.io/badge/maintainer-LRVT-orange" /></a>
    <a target="_blank" href="https://GitHub.com/Haxxnet/Invoke-DCSync/graphs/contributors/"><img src="https://img.shields.io/github/contributors/Haxxnet/Invoke-DCSync.svg" /></a><br>
    <a target="_blank" href="https://GitHub.com/Haxxnet/Invoke-DCSync/commits/"><img src="https://img.shields.io/github/last-commit/Haxxnet/Invoke-DCSync.svg" /></a>
    <a target="_blank" href="https://GitHub.com/Haxxnet/Invoke-DCSync/issues/"><img src="https://img.shields.io/github/issues/Haxxnet/Invoke-DCSync.svg" /></a>
    <a target="_blank" href="https://github.com/Haxxnet/Invoke-DCSync/issues?q=is%3Aissue+is%3Aclosed"><img src="https://img.shields.io/github/issues-closed/Haxxnet/Invoke-DCSync.svg" /></a><br>
        <a target="_blank" href="https://github.com/Haxxnet/Invoke-DCSync/stargazers"><img src="https://img.shields.io/github/stars/Haxxnet/Invoke-DCSync.svg?style=social&label=Star" /></a>
    <a target="_blank" href="https://github.com/Haxxnet/Invoke-DCSync/network/members"><img src="https://img.shields.io/github/forks/Haxxnet/Invoke-DCSync.svg?style=social&label=Fork" /></a>
    <a target="_blank" href="https://github.com/Haxxnet/Invoke-DCSync/watchers"><img src="https://img.shields.io/github/watchers/Haxxnet/Invoke-DCSync.svg?style=social&label=Watch" /></a><p>
    <a href="https://www.buymeacoffee.com/LRVT" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>
</div>

## 💎 Features

Invoke-DCSync is a PowerShell wrapper script around popular tools such as PowerView, Invoke-Mimikatz and ADRecon. 

It automates the task of dumping NT password hashes from an Active Directory environment. The script was designed for Active Directory password audits, where extracted password hashes undergo a cracking process in order to outline password strength and policy weaknesses. 

The script will parse the output of Mimikatz's DCSync and create two separate folders with output files:
- A directory `CUSTOMER` with detailed information about an Active Directory user and its NT password hash. The import file in this directory will later be used to establish a reference between an AD user and a cracked password hash.
- A directory `PTF` with information about NT password hashes only. This folder may be shared with an external security vendor that conducts offline password cracking. No user information are stored in this directory. Only plain NT hashes.

## 🎓 Usage

To utilize this PowerShell script, it's recommended to disable Antivirus/EDR. Alternatively, if no advanced EDR is in use, it may be sufficient to bypass AMSI for the current PowerShell process.

The script must be run in the context of an Active Directory domain user with DCSync rights. Usually, a Domain Administrator (DA) user account is privileged and recommended for easy of use. You may obtain a PowerShell terminal in the context of such domain user via the following PowerShell command:

````powershell
runas.exe /netonly /noprofile /user:example.com\dcsyncuser "powershell.exe -ep bypass"
````

Other from that, it's a matter of running the PowerShell .PS1 script:

````powershell
iex(new-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/Haxxnet/Invoke-DCSync/main/Invoke-DCSync.ps1')
````

You will be prompted about the target AD domain. Confirm to start the DCSync extraction process of NT password hashes. 

As soon as the script finishes, a new Windows file explorer will open automatically and display the relevant output directories.
