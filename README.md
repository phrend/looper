# looper
Looper is a looping (and parallel) ssh utility that allows you to specify the user to ssh as, the number of simultaneous connections, timeouts, command files (loops), and specify different output formats.

# Usage
```
SYNOPSIS
    looper [-c command_file] [-d] [-h] [-k proc_timeout] [-l login_name]
                [-m max_connections] [-o prefix|raw] [-s ssh_options]
                [-t ssh_timeout] fqdn1 [fqdnN]

DESCRIPTION
    This is a script to connect to multiple servers, via ssh, in parallel, run
    remote commands, and log the output.

OPTIONS
    -c                     The path to the config/command file (required)
    -d                     Dry-run (just show what would have been done)
    -h                     Print this help message
    -k proc_timeout        Kill stale procs after <proc_timeout> seconds
                             (default: 600)
    -l login_name          Specifies the user to log in as on the remote machine
    -m max_connections     The max number of simultaneous connections to run
                             (default: 25)
    -n node_file           The path to a file containing all of the fqdn's you
                           want to loop through
    -o output_format       Sets the output format:
                             default : output with separating lines (default)
                              prefix : prefix all output with the 'fqdn: '
                                 raw : just the raw server output
    -s ssh_options         Additional ssh arguments you want to set (like -t)
                             (they must be wrapped in quotes)
                             note: if you use -t, remember to include 'exit'
                             at the end of your command file)
    -t connecttimeout      The ssh connecttimeout value (in seconds)
                             (default: 20)

    The final argument(s) must be space separated fqdn's, like:
      fqdn1 fqdn2 fqdn3

EXAMPLES
    looper -c commands.looper fqdn1 fadn2
    looper -s '-t' -m 10 -o prefix -t 5 -c commands.looper fqdn1 fadn2
    looper -d -c commands.looper fqdn1 fadn2
```
# Known Bugs
<no known bugs, but there probably are some!>

# Possible Enhancements
1. add an arg so you can directly pass a command (for one-liners)
2. allow for a config file to set options
3. allow the command file to include config params
     maybe have the app split the original .loop file in to <blah>.config and <blah>.loop and then use those
4. consider changing -c to a positional argument, since it's required
5. silent option - only the command output is sent to stdout (for scripting)
6. find a nice way to output progress/how many servers are remaining
7. show error and total server count while looping
8. add an arg to define the log retention time
9. add a function for isDebug() to clean the code up a bit
10. append error in server's log when proc is killed via killOldProcs()

# Similar (better?) Tools
[pssh] <https://code.google.com/archive/p/parallel-ssh/>

[Massh] <http://m.a.tt/er/massh/>

[DSH] <https://www.netfort.gr.jp/~dancer/software/dsh.html.en>

[Ansible] <https://www.ansible.com/>
