name: Kevin Wong

date: 7/5/2022

file: PXEBootWindowsServerADWDS.md.md

desc: Installing Windows via Windows Deployment Services(WDS) and PXEBooting



- Error Message: "The specified server name is invalid or does not exist in the directory service."
  - Resolved
  - NETBios name is truncated due to length.  If you look in DNS, I assume the name is listed as "deploymentserver" but in NETBios it is "deploymentserve". For WDS to initialize, you need to keep the name length below 16 characters.  If you rename your server to "deploymentsvr" (or something less than 16 characters), it will work.

    - Steps:

      1. Run: wdsutil /uninitialize /server:deploymentserve
      2. Rename computer to something less than 16 chars (deploymentsvr, deployserver, wdsserver, etc.)
      3. Reboot
      4. Run: wdsutil /verbose /progress /initialize-server /server:NewServerName /reminst:c:\RemoteInstall 
