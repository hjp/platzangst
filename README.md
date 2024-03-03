Platzangst
==========

Monitor free space on multiple hosts and take action if it runs low.

The script takes the name of a configuration file as its single
argument. This file must be in JSON format and contain a dict with the
following keys:

| Key | Description |
|-|-|
| `hosts` | A list of host names |
| `filesystems` | A list of file systems |
| `min_free_pct` | minimum acceptable free space in % |
| `interval` | check interval in seconds |
| `action` | A command to invoke if space runs low. Preferably as a list |

The script uses SSH to connect to each host and run the `df` command to
determine free blocks and inodes on each of the file systems. If either
falls below `min_free_pct`, `action` is invoked. `action` may be a
single string or a list of arguments (with first argument being the
command name). The latter is safer and preferred. See
https://docs.python.org/3/library/subprocess.html#subprocess.Popen for a
full discussion how this parameter is interpreted.

See [test.json](test.json) for an example.

This repo also contains a sample action
[terminate_all_pgsessions](terminate_all_pgsessions), which connects to
the local PostgreSQL and terminates all sessions.
