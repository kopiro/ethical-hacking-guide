# Local File Inclusion (RLFI)

Local File Inclusion (LFI) allows an attacker to include files on a server through the web browser.

This vulnerability exists when a web application includes a file without correctly sanitising the input, allowing and attacker to manipulate the input and inject path traversal characters and include other files from the web server.

[Local File Inclusion (LFI) [Definitive Guide] - Aptive](https://www.aptive.co.uk/blog/local-file-inclusion-lfi-testing/)

## PHP

Start to test if your PHP script allows LFI.

```txt
/script.php?page=../../../../../../../../etc/passwd
```

### PHP wrappers

#### php://input

PHP `expect://` allows execution of system commands, unfortunately the expect PHP module is not enabled by default.

```txt
php://input&cmd=$REMOTE_COMMAND
```

#### php://filter

`php://filter` allows to include local files and base64 encodes the output. Therefore, any base64 output will need to be decoded to reveal the contents.

```txt
php://filter/convert.base64-encode/resource=$REMOTE_FILE_PATH
```

#### zip://

The zip wrapper processes uploaded `.zip` files server side allowing the upload of a zip file using a vulnerable file function exploitation of the zip filter via an LFI to execute.

```txt
zip://path/to/shell-uploaded-to-server.zip`
```

### Other links

[PHP Remote File Inclusion command shell using data://](https://www.idontplaydarts.com/2011/03/php-remote-file-inclusion-command-shell-using-data-stream/)
