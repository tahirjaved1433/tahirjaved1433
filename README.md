aNotepadaNotepad - free online notepad
Features
Register/Login
 
RDP Code
Share
name: CI


on: [push, workflow_dispatch]


jobs:

  build:


    runs-on: windows-latest


    steps:

    - name: Download

      run: Invoke-WebRequest https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-windows-amd64.zip -OutFile ngrok.zip

    - name: Extract

      run: Expand-Archive ngrok.zip

    - name: Auth

      run: .\ngrok\ngrok.exe authtoken $Env:NGROK_AUTH_TOKEN

      env:

        NGROK_AUTH_TOKEN: ${{ secrets.NGROK_AUTH_TOKEN }}

    - name: Enable TS

      run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server'-name "fDenyTSConnections" -Value 0

    - run: Enable-NetFirewallRule -DisplayGroup "Remote Desktop"

    - run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" -Value 1

    - run: Set-LocalUser -Name "runneradmin" -Password (ConvertTo-SecureString -AsPlainText "P@ssw0rd!" -Force)

    - name: Create Tunnel

      run: .\ngrok\ngrok.exe tcp 3389

Public Last updated: 2023-08-17 11:52:06 AM

Comments
Rebin  •  1 month 24 days ago Reply
Good bro
Milton  •  1 month 20 days ago Reply
Not Workes
EHTASHAM  •  1 month 18 days ago Reply
working smooth. thnx
not work  •  1 month 12 days ago Reply
not work received error
ci  •  1 month 6 days ago Reply
ci
Auth error  •  1 month 3 days ago Reply
Recived Auth error : 
Error: Process completed with exit code 1.

Your Name
Comment

Download on the Apple Store   Get it on Google Play

© 2009-2023 aNotepad.com

About | Privacy | Features | Resume Builder | Free Fax | Report Abuse

aNotepad.com is your everyday online notepad. You can take notes and share notes online without having to login.
You can use a rich text editor and download your note as PDF or Word document.
Best of all - aNotepad is a fast, clean, and easy-to-use notepad online.
