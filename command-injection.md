# Command Injection

Command injection is an attack in which the goal is execution of arbitrary commands on the host operating system via a vulnerable application. Command injection attacks are possible when an application passes unsafe user supplied data (forms, cookies, HTTP headers etc.) to a system shell.

In this attack, the attacker-supplied operating system commands are usually executed with the privileges of the vulnerable application. Command injection attacks are possible largely due to insufficient input validation.

[Command Injection - OWASP](https://www.owasp.org/index.php/Command_Injection)

## Command injection

Try to insert a `;` (`%3b`) after the parameter to terminate the previous command and execute a new one. Try also with **EOL** (`%0d%0a`), backtick or `$(cmd)` to evaluate code or other bash operators, like `&&, ||`

## C binary using `strcmp`

If you are dealing with a binary that is doing a string comparison using `strncmp` or `strcmp`, you can bypass this check by inserting a **EOL** after the string compared against.

In an interactive shell, you can use CTRL+m to insert a new-line.

```bash
$ $COMMAND "$STRING(CTRL+m)
> bash"
```

## Escaping spaces

Escaping spaces is never a solution to avoid command injections.

You can easily avoid using spaces by using `{cat,flag.txt}` instead of `cat flag.txt`

[Bash Brace Expansion Cleverness | Jon Oberheide](https://jon.oberheide.org/blog/2008/09/04/bash-brace-expansion-cleverness/)
