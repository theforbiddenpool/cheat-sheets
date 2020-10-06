## `man`
Provides in-depth documentation about many programs and utilities.
```
$ man [no.chapter] <topic>
```
- `-f` → show all man pages containing `<topic>` string in their name.
- `-k` → show all man pages that discuss a specified subject.
- `-a` → display all pages with the given name, one after the other.
	
## Locating applications
```
$ which <name-program>
$ whereis <name-program>
```
`whereis` looks for packages in a broader range of system directories.

## Viewing files
Command | Options | Description
--- | --- | ---
`cat` | | used for files that are not very long. It's able to concatenate and append files.
`cat > <filename> << EOF` | | create a file, fill it with content until EOF is typed.
`tac` | | look at a file backwards, starting with the last line.
`less` | | paging program, used for view large files.
`tail` | | prints the last 10 lines of a file.
| |	`-n <num>` | change the number of lines.
|	| `-f` | continually monitor new output in a growing file.
`head` | | prints the first 10 lines of a file.

## I/O Redirection
_Change input from stdin to file:_
```
$ command < input-file
```

_Redirect output from stdout to file:_
```
$ command > output-file
```

_Redirect error messages from stderr to file:_
```
$ command 2> error-file
```

_Redirect error messages from stderr to the same file as stdout:_
```
$ command >& all-output-file
```

## `find`
Recurses down the filesystem tree from any particular directory and locate files that match specified conditions.
```
$ find <directory> options
```
- `-name` → list files with a certain pattern in their name.
- `-iname` → also ignore the case of file names.
- `-type` → restrict the results to a certain filetype (`d` - directory; `l` - symbolic links; `f` - regular file).

- `-exec` → execute a command on the files that match the search criteria.
- `-ok` → same as `-exec`, but prompt you for permission before executing the command.
	
- `-ctime` → when the inode metadata last changed.
- `-atime` → last accessed/last read.
- `-mtime` → last modified/last written. There are similar options with minutes (-cmin, -amin, -mmin).
- `-size` → finds files based on sizes. The default is 512-byte blocks.

## `diff`
Used to compare files and directories.
```
$ diff [options] <file1> <file2>
```
- `-c` → provides a listing of differences that include 3 lines of context before andafter the lines differing in context.
- `-r` → recurse into subdirectories.
- `-i` → ignore the case of letters.
- `-w` → ignore differences in white space (spaces, tabs).

Compare three files at once. It uses one file as the reference basis for the other two.
```
$ diff3 <file1> <base-file> <file2>
```

## `file`
In Linux, a file's name is more meaningful for the user than for the system itself. Most applications directly examine a file's content to see what kind of object it is. The real nature of a file can be ascertained by using:
```
$ file <file-name>
```

## `rsync`
`rsync` is a very efficent tool to copy data because trys to avoid unnecessary copy by checking if the file is the same and only coping the files that have changed.
```
$ rsync [options] <source> <destination>
```
- `-r` → recurse into directories.
- `-n` → dry run option, doesn't copy. Used for testing.

## Compressing data
Compressing data saves disk space and reduces the time it takes to transmit files over networks. There are multiple utilities: **gzip**, the most frequently used, **bzip2**, which produces smaller files, **xz** the most efficient compression utility used in Linux, and **zip**, not used very often in the Linux world. gzip, bzip2 and xz are only compression algorithms, they will compress all files individually.

### `gzip`
_Compress a file:_
```
$ gzip <file>
```
- `-r` → recurses into directories.
-	`-d` → decompress the file.
	
_Uncompress a file:_
```
$ gunzip <file>
```

### `zip`
_Compress files:_
```
$ zip <name-zipped> <files..>
```
- `-r` → recurse into directories.
	
_Unzip a file:_
```
$ unzip <file-name>
```

### `tar`
It allows you to create or extract files from an archive file (tarball). At the same time you can optionally compress while creating the archive and decompress while extracting it.
```
$ tar <options> <files..> 
```
- `x` → extract files.
- `v` → verbose.
- `c` → create a new archive.
- `f <name-tarball>` → use specified archive file. If not given tar will first examine $TAPE variable, and next its defaults.
- `z` → compress using gzip.
- `j` → compress using bzip2.
- `J` → compress using xz.
- `t` → list the contents of the tar file.

## `dd`
Make copies of raw disk space.
```
$ dd <options>
```
- `if=FILE` → input file / input device node.
-	`of=FILE` → output file / output device node.
-	`bs=BYTES` → read and write up to BYTES bytes at a time.
-	`conv=CONVS` → convert the file (e.g. ucase).

## Accounts, Users and Groups
_List current logged-on users:_
```
$ who
```

_Identify the current user:_
```
$ whoami
```

_Show the last time each user logged into the system:_
```
$ last [options] [username...] [tty...]
```

_Add a new user:_
```
$ sudo useradd [options] <name-user>
```
- `-m` → create user's home directory if it does not exist.
-	`-g <name>` → the group name or number of the user's initial login group.
-	`-G <names...>` → list of supplementary groups which the user is also member of.
-	`-s <path-to-shell>` → the name of the user's login shell.

_Deleting a user:_
```
$ sudo userdel [options] <name-user>
```
-	`-r` → remove files in the user's directory along with the home directory itself.

_Show information about a user:_
```
$ id <name-user>
```
The default value is the current user.

_Change password of user:_
```
$ passwd <name-user>
```

_Configure the password expiration information for a user:_
```
$ chage <name-user>
```

_Edit a user:_
```
$ sudo usermod [options] <name-user>
```
-	`-G <name-group>` → add user to a new group, removing him from other groups.
-	`-a` → append group to the group list.

_Add a new group:_
```
$ sudo groupadd [options] <name-group>
```

_Deleting a group:_
```
$ sudo groupdel [options] <name-group>
```

_Edit a group:_
```
$ sudo groupmod [options] <name-group>
```
-	`-g` → change the Group ID (gid).
-	`-n` → change the name of the group.
	
## File Permissions
_Change user ownership of a file or directory:_
```
$ chwon <name-user> <file>
```

_Change group ownership of a file or directory:_
```
$ chgrp <name-group> <file>
```

_Change permissions of a file or directory:_
```
$ chmod <permissions> <file>
```

### Permissions
*Absolute Mode*
Code | Description
--- | ---
0 | No permission
1 | Execute
2 | Write
3 | Execute + Write
4 | Read
5 | Read + Execute
6 | Read + Write
7 | Read + Write + Execute
	
*Symbolic Mode*
Code | Description
--- | ---
+ | Adds permission
- |  Removes permission
= | Sets the permission and overrides the permissions set earlier
u | user
g | group
o | others

## `echo`
Displays text. Can be used to display a string on stdout or in a new file, and to view the values of environment variables.
```
$ echo [options] <text>
$ echo $VARIABLE
```
- `-e` → enables interpretation of \; `\n` → new line, `\t` → horizontal tab

## z Command Family
There are special versions of some programs to work with compressed files. Some are: `zcat`, `zless` / `zmore`, `zgrep`, and `zdiff`. For files compressed with bzip2 use bz instead of z and for xz use xz.

## `sed`
Used to modify the contents of a file. It can filter texts as well perform substitutions in data streams. The data from the input is taken and moved to a working space, where the list of modifications is applied, and the final contents are moved to stdout.

_Specify editing commands at the command line, and print to stdout:_
```
$ sed -e <commands> <filename>
```

_Specify scriptfile containing sed commands, and print to stdout:_
```
$ sed -f <script-file> <filename>
```

_Save changes in the input file:_
```
$ sed -i <commands> <filename>
```

### Basic Operations
_Substitute first string occurence in a line:_
```
$ sed /s/string/replace_string/ <file>
```

_Substitute all string occurrences in a line:_
```
$ sed /s/string/replace_string/g <file>
```

_Substitute all string occurences in a range of lines:_
```
$ sed 1,3s/string/replace_string/ <file>
```

*e.g.* Convert 01/02 to JAN/FEB:
```
$ sed -e 's/01/JAN' -e 's/02/FEB/' <file>
```

## `awk`
Used to extract and then print specific contents of a file. Often used to construct reports, manipulate data files, retrieving, and processing text.
```
$ awk [options] <command> <file>
```
-	`-f` → specify a script file to be executed.
- `-F <separator>` → separate prints by the chosen separator.
	
### Basic Operations
_Print entire file:_
```
$ awk '{ print $0 }' <file>
```

_Print the first field (column) of every line, separated by ":":_
```
$ awk -F: '{ print $1 } <file>
```

_Print first and sixth field of every line, separated by ":":_
```
$ awk -F: '{ print $1 $6 }' <file>
```

## `sort`
Used to rearrange the lines of a text file, either in ascending or descending order, according to a sort key. The default sort key is order of the ASCII characters. It does not save in the file.
```
$ sort [options] <filename>
```
- `-r` → sort lines in reverse order.
-	`-u` → check for unique values after sorting the lines (same as uniq).

## `uniq`
Used to remove duplicate lines in a text file. Requires that the duplicate entries to be removed are consecutive, so it's best to use sort first.
```
$ uniq [options] <filename>
```
-	`-c` → count the number of duplicate entries.
	
## `paste`
Merges line of files, used to create a single file. The different columns are identified based on delimiters.
```
$ paste [options] <filename1> <filename2>
```
-	`-d<delimiters>` → specify a list of delimiters. Each delimiter is used in turn until the list is  exhausted.
-	`-s` → append the data in series rather than in parallel.

## `join`
It joins lines of two files on a common field.
```
$ join [options] <file1> <file2>
```

## `split`
Used to split a file into equal-sized (default 1000 lines) segments for easiers viewing and manipulation. By default, the prefix is added in the file's name.
```
$ split <file> [prefix]
```

## `grep`

Used primarily as a text searching tool. It can files for specified patterns and can be used with regular expressions.
```
$ grep [pattern] <filename>
```
-	`-v` → print the lines that do not match the pattern.
-	`-C n` → print n lines of context for each match.

## `tr`

Used to translate specified characters into others or delete them.
```
$ tr [options] <set1> [set2]
```
-	`-s` → removes repeated characters, leaving only one of each.
-	`-d` → delete specified characters.
-	`-c` → instead of deleting, prints the specified characters.
	
`[:space:]` → space\
`[:digit:]` → digits

## `tee`
Take the output from any command, sends it to stdout and save it to a file.
```
$ <command> | tee <file>
```

## `wc`
Counts the number of lines, words and characters in a file or list of files.
```
$ wc [options] <files...>
```
-	`-l` → display the number of lines.
-	`-c` → display the number of bytes.
-	`-w` → display the number of words.

## `cut`
Used for extract specific columns on column-based files. The default column separator is the tab character.
```
$ cut [options] <file>
```
-	`-d <separator>` → change the separator
-	`-f <field>` → the number of field to display

# Network
## `ip`
`ip` is a very powerful program that can do many things, used to substitute older utilities such as ifconfig and route.

_View IP Address:_
```
$ ip addr show
```

_View the routing information:_
```
$ ip route show
```

## `ping`
Used to check whether or not a machine can recieve and send data through the network.
```
$ ping [options] <hostname>
```
-	`-c <num>` → limits the number of packets that ping will send before it quits.
	
## `traceroute`
Used to inspected the route which the data packet takes to reach the destination host.
```
$ traceroute [options] <domain>
```

## `iptraf`
Monitors network traffic in text mode.
```
$ iptraf
```

## `wget`
Used to download files and information, when a browser is not the best option. It handles multiple types of downloads.
```
$ wget [options]  <url>
```

## `ftp`
One of many FTP command line tools. For secure mode of connection, use sftp.

_Connect to a ftp server:_
```
$ ftp -p <url>
```

_List the contents of that FTP server:_
```
> ls

```
_Dowload a file from the server:_
```
> get <name-file>
```

_Quit the FTP server:_
```
> quit
```

## `ssh`
Useful for administering systems to which you have remote access.
```
$ ssh <remote-system> <command>
```

## `scp`
Allows you to securely move files between two networed hosts. It uses the SSH protocol for transferring data.
```
$ scp <local-file> <user>@<remotehost>:<directory-to-paste>
```

---
## `pdftk`
PDF Toolkit, can perfom a very large variety of sophisticated tasks.

_Merge two documents:_
```
$ pdftk <first-file> <second-file> cat output <output-file>
```

_Write only pages 1 and 2 of a file:_
```
$ pdftk A=<file> cat A1-2 output <output-file>
```

_Rotate all pages 90º clockwise:_
```
$ pdftk A=<file> cat A1-endright output <output-file>
```

_Encrypt a PDF file, receiving a prompt to set the required password (max 32 characters):_
```
$ pdftk <file> output <output-file> user_pw PROMPT
```

# Processes
## `ps`
Used to view the running processes.
```
ps [options]
```
-	`a` → lits all processes with a terminal (tty), or to list all processes when used together with the x option.
-	`x` → list all processes owned by you, or list all processes when used together with the a option.
-	`u` → display user-oriented format.
-	`o <attr,...>` → allows you to specify which attributes you want to view. Some are stat, priority, pid, pcup, and comm.
-	`r` → restrict the selection to only running processes.
-	`c` → show the true command name (comm).

## `pstree`
Displays the processes running on the system in the form of a tree diagram, showing the relationship between processes. Repeated entries of a process are not displayed.
```
$ pstree [options] [pid, user]
```

## `kill`
Sends the specified signal to the specified processses or process groups
```
$ kill [options] <pid>
```

## `top`
Repetitive update of ps. Each line in the process list displays information about a process. The information displayed is: 
1. process identification number (PID)
2. process owner (USER)
3. priority (PR) and nice values (NI)
4. virtual (VIRT)
5. physical (RES) and shared memory (SHR)
6. status (S)
7. percentage of CPU (%CPU) and memory (%MEM) used
8. execution time (TIME+) and command (COMMAND)

Key | Description
--- | ---
t	| display or hide summary information (rows 2 and 3)
m	| display or hide memory information (rows 4 and 5)
A	| sort the process list by top resource consumers
r	| renice (change the priority of) a specific processes
k	| kill a specific process
f	| enter the top configuration screen
o	| interactively select a new sort order in the process list

## `jobs`
Displays all jobs running in background. The background jobs are connected to the terminal window, so if you log off, the jobs utility will not show the ones started from that window.
```
$ jobs [options]
```
-	`-l` → includes the PID of the background jobs.

## `at`
Execute any non-interactive command at a specified time.
```
$ at now + 2 days
> command
```

## `sleep`
Suspends execuction of a command or job for the specified period of time.
```
$ sleep <number[SUFFIX]>
```
-	`SUFFIX` → `s` seconds, `m` minutes, `h` hours, `d` days

# Sources
[Introduction to Linux – edX](https://www.edx.org/course/introduction-to-linux)