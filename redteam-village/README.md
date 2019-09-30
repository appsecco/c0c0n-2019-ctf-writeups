# RedTeam Village CTF Write-up

## CTF Portal

https://ctf.redteamvillage.org/

## Attack

* The CTF portal gave 1 target IP - 34.89.165.167
* We found an SSH, RDP and web server running on the target
* Using the provided clue `victimcorporation`, we were able to browse to `http://34.89.165.167/victimcorporation/`
* We ran `dirb` against the URL `http://34.89.165.167/victimcorporation/` and found a directory `config`
* On subsequent bruteforce for filenames on `http://34.89.165.167/victimcorporation/config` we found `config.zip` which we were able to download
* An XML file inside gave us the credentials for `guestuser`
* We were able to SSH in to `34.89.165.167` using `guestuser` credential
* Navigating the filesystem, we were able to find another file revealing the credential of `appuser` who has `Local Administrator` privilege
* We also found another system in the LAN with IP `<IP>`
* We were able to laterally move to this system using `appuser` credential and login over RDP
* This new system was part of a domain controller
* We identified the `SQL Server` by resolving `MSSQL-SERVER` hostname from this domain joined machine

At this point, we were not able to connect to the SQL Server since there was no TCP/IP listener for it.

## Result

We ended up being #1 in the Red Team category for this event, with maximum points in the category. Since we were not able to reach the final objective of compromising the domain controller, the 1st prize for the event went to the highest scorer in the Blue Team category.