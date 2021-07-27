## Useful bash variables:

- `$1`, `$2`, `$3`, ... are the [positional parameters][1].
- `"$@"` is an array-like construct of all positional parameters, `{$1, $2, $3 ...}`.
- `"$*"` is the IFS expansion of all positional parameters, `$1 $2 $3 ...`.
- `$#` is the number of positional parameters.
- `$-` current options set for the shell.
- `$$` pid of the current shell (not subshell).
- `$_` most recent parameter (or the abs path of the command to start the current shell immediately after startup).
- `$IFS` is the (input) field separator.
- `$?` is the most recent foreground pipeline exit status.
- `$!` is the PID of the most recent background command.
- `$0` is the name of the shell or shell script.

Most of the above can be found under [Special Parameters][2] in the Bash Reference Manual. There are all the [environment variables set by the shell][3].

For a comprehensive index, please see the [Reference Manual Variable Index][4].  
Reference : [StackOverflow][5]

  [1]: https://www.gnu.org/software/bash/manual/html_node/Positional-Parameters.html
  [2]: https://www.gnu.org/software/bash/manual/html_node/Special-Parameters.html
  [3]: https://www.gnu.org/software/bash/manual/html_node/Shell-Variables.html
  [4]: https://www.gnu.org/software/bash/manual/html_node/Variable-Index.html
  [5]: https://stackoverflow.com/questions/5163144/what-are-the-special-dollar-sign-shell-variables