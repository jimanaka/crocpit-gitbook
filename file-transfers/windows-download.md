---
description: Windows File Downloads Techniques
---

# 🪟 Windows Download

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

