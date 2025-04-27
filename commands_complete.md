# 🧰 Linux Command Reference

## 📚 Table of Contents

- 📦 [Package & System Management](#package--system-management)
- 📁 [File & Directory Management](#file--directory-management)
- 🧠 [Shell & Process Utilities](#shell--process-utilities)
- 🌐 [Networking & Connectivity](#networking--connectivity)
- 🔐 [Security & Permissions](#security--permissions)
- 📊 [Monitoring & Diagnostics](#monitoring--diagnostics)
- 🔧 [Device & Disk Utilities](#device--disk-utilities)
- 🧪 [Development & Tools](#development--tools)
- 📝 [Documentation & Help](#documentation--help)
- 📚 [Log Files & System Info](#log-files--system-info)
- ⚙️ [Services & Daemons](#services--daemons)
- 🛡 [Firewall & Access Control](#firewall--access-control)
- 🚀 [Tips, Fixes & Config Examples](#tips-fixes--config-examples)

## 📦
## Package & System Management

---

### `apt`

High-level package manager for Ubuntu/Debian systems. Used for installing, upgrading, and managing software.  

```bash
apt [options] {command}
```

**Common commands**:

- `install` : Install a new package
- `remove` : Remove a package (preserves config files)
- `purge` : Remove a package and its config files
- `update` : Update package lists
- `upgrade` : Upgrade installed packages
- `dist-upgrade`, `full-upgrade` : Smarter upgrade (handles dependencies)
- `autoremove` : Remove unused dependencies
- `autoclean`, `clean` : Clear package cache
- `edit-sources` : Edit APT repository sources
- `list`, `list --installed` : List available or installed packages

📌 **Tags**: `#package-manager #apt #ubuntu #debian #system`

---

### `apt-cache`

Query APT’s package cache for information, search, and troubleshooting.  

```bash
apt-cache [options] command [pkg|regex]
```

**Common commands**:

- `search regex` : Search for packages by name or description
- `show` : Show details about a package
- `showpkg` : Show dependencies and versions
- `policy` : Show repository priorities
- `stats` : Show cache statistics
- `pkgnames` : List all known package names
- `unmet` : Show packages with unmet dependencies

**Options**:

- `-n`, `--names-only` : Only match package names
- `-f`, `--full` : Print full package info
- `-a`, `--all-versions` : Show all available versions

📌 **Tags**: `#apt #package-info #search #metadata`

---

### `dpkg`

Low-level package tool for installing, removing, and managing `.deb` files.  

```bash
dpkg [options] [package_name]
```

**Common options**:

- `-i`, `--install` : Install a package file
- `-r`, `--remove` : Remove a package (keep configs)
- `-P`, `--purge` : Remove package and config files
- `--list` : List installed packages
- `--listfiles` : List files installed by a package
- `--update-avail` / `--merge-avail` : Sync available packages with repository

📌 **Tags**: `#debian #dpkg #packages #low-level #install #uninstall`

---

### `snap`

Tool for managing Snap applications (sandboxed packages).  

```bash
snap [options] <command>
```

**Common commands**:

- `install <pkg>` : Install a Snap package
- `remove <pkg>` : Uninstall a Snap
- `refresh` : Update Snap packages
- `list` : Show installed Snaps
- `find` : Search for available Snaps
- `info` : Show details about a Snap
- `enable`, `disable` : Toggle Snap availability
- `start`, `stop`, `restart` : Control Snap daemons/services
- `run` : Run a command inside a Snap

📌 **Tags**: `#snap #package-manager #ubuntu #sandboxed-apps`

---

### `ubuntu-advantage`

Manage Ubuntu Pro subscription features (livepatch, extended support, etc).  

```bash
ubuntu-advantage <command> [<args>]
```

**Common command**:

- `status` : Show which Pro services are active on this system

📌 **Tags**: `#ubuntu #pro #subscription #support #canonical`

---

### `useradd`

Create a new system user.  

```bash
useradd [options] LOGIN
```

**Options**:

- `-M` : Do not create a home directory
- (Other options include setting shell, UID, groups, etc.)

📌 **Tags**: `#user #account #admin #adduser #system-users`

---

### `usermod`

Modify existing user properties, including group memberships.  

```bash
usermod [options] LOGIN
```

**Options**:

- `-a`, `--append` : Add user to additional groups (must be used with `-G`)
- `-G group1,group2` : Set supplementary groups
- `-L`, `--lock` : Lock the user's password (disable login)

📌 **Tags**: `#user #permissions #groups #lock-user #admin`

---

### `visudo`

Safely edit the `sudoers` file using a locked and syntax-checked environment.  

```bash
sudo visudo [options]
```

**Options**:

- `-f file` : Edit alternate sudoers file
- `-h` : Show help

📌 **Tags**: `#sudo #permissions #security #admin #editors`

---
## 📁
## File & Directory Management

---

### `cat`

Concatenate and display the contents of files.  

```bash
cat [OPTION] [FILE]
```

**Options**:

- `--help` : Show help message

📌 **Tags**: `#display #text #concatenate #files #stdout`

---

### `cp`

Copy files and directories.  

```bash
cp [OPTION]... SOURCE DEST
```

**Options**:

- `-i`, `--interactive` : Prompt before overwrite
- `-r`, `-R`, `--recursive` : Copy directories recursively
- `-l`, `--link` : Create hard link instead of copying

📌 **Tags**: `#copy #file-management #backup #directory #move`

---

### `cut`

Extract sections from lines of input.  

```bash
cut OPTION... [FILE]...
```

**Options**:

- `-b` : Select byte positions
- `-c` : Select character positions
- `-d` : Set delimiter
- `-f` : Select fields
- `-s` : Suppress lines without delimiters
- `--complement` : Invert selection

📌 **Tags**: `#text #fields #columns #csv #extract`

---

### `df`

Report disk space usage.  

```bash
df [OPTION] [FILE]
```

**Options**:

- `-a`, `--all` : Include pseudo/duplicate filesystems
- `-h` : Human-readable
- `-H` : SI units (base 1000)
- `-l` : Show only local file systems
- `-P` : POSIX format
- `-T` : Show filesystem type
- `--help` : Show help

📌 **Tags**: `#filesystem #storage #space #mount #disk`

---

### `du`

Estimate file and directory sizes.  

```bash
du [OPTION] [FILE]
```

**Options**:

- `-a` : Show all files, not just directories
- `-h` : Human-readable sizes
- `-s` : Show total per argument
- `-c` : Grand total
- `-d N` : Max depth N
- `--apparent-size` : Use actual file size, not block size
- `--exclude=PATTERN` : Skip matching files

📌 **Tags**: `#disk-usage #directory #filesize #storage #analyze`

---

### `find`

Search for files and directories in a path.  

```bash
find [path] [expression]
```

**Options/Expressions**:

- `-name`, `-iname` : Match filenames (case-sensitive/insensitive)
- `-path`, `-ipath` : Match paths
- `-type` : Filter by type (`f`, `d`, `l`)
- `-mtime`, `-atime`, `-ctime` : Filter by modified/access/changed time

**Examples**:

```bash
find /usr -iname '*.txt'
find . -type f -name '*.sh'
```

📌 **Tags**: `#search #files #filter #time #recursive`

---

### `ln`

Create hard or symbolic links between files.  

```bash
ln [OPTION] TARGET [LINK_NAME]
```

**Options**:

- `-s` : Create a symbolic (soft) link
- `--help` : Show help

📌 **Tags**: `#link #symlink #filesystem #reference #alias`

---

### `locate`

Find file paths using a fast database lookup.  

```bash
locate [OPTION]... PATTERN...
```

Requires `updatedb` to be run to update the file database.

📌 **Tags**: `#search #locate #files #fast #filename`

---

### `ls`

List directory contents.  

```bash
ls [OPTION]... [FILE]...
```

**Options**:

- `-a` : All files including hidden
- `-A` : All but `.` and `..`
- `-l` : Long listing (permissions, owner, size)
- `-R` : Recursive
- `-S` : Sort by file size
- `-t` : Sort by modification time
- `-1` : One file per line
- `--author` : Show author if `-l` is used

📌 **Tags**: `#list #directory #details #sort #hidden`

---

### `lsblk`

Show block device info in tree format.  

```bash
lsblk [OPTIONS] [DEVICE]
```

**Options**:

- `--help` : Show help with all available columns

📌 **Tags**: `#disk #block-device #partition #mount`

---

### `lshw`

List detailed hardware configuration.  

```bash
lshw [OPTIONS]
```

**Options**:

- `-short` : Compact summary
- `-C <class>` : Filter by class (e.g., `memory`, `display`)
- `-help` : Show help

📌 **Tags**: `#hardware #system-info #device #diagnostic`

---

### `mkdir`

Create new directories.  

```bash
mkdir [OPTION] DIRECTORY
```

**Options**:

- `-p`, `--parents` : Create parent directories as needed
- `--help` : Show help

📌 **Tags**: `#directory #create #folder #script #parent`

---

### `mount`

Mount a device or filesystem.  

```bash
mount [options] DEVICE MOUNTPOINT
```

**Common usage**:

```bash
sudo mount /dev/sdb1 /mnt/disk
```

**Options**:

- `-t <fstype>` : Filesystem type
- `-o <options>` : Mount options (e.g. `ro`, `uid=1000`)

📌 **Tags**: `#mount #fstab #filesystem #device #external`

---

### `mv`

Move or rename files and directories.  

```bash
mv SOURCE TARGET
```

**Options**:

- `--help` : Show help

📌 **Tags**: `#move #rename #files #organize #directory`

---

### `pwd`

Print current working directory.  

```bash
pwd
```

📌 **Tags**: `#cwd #location #shell #directory`

---

### `rm`

Delete files or directories.  

```bash
rm [options] FILE
```

**Options**:

- `-r`, `--recursive` : Delete directories recursively
- `-i` : Interactive (ask before deletion)
- `-v` : Verbose
- `--help` : Show help

**Examples**:

```bash
rm -i file.txt
rm -rfi directory/
```

📌 **Tags**: `#delete #remove #clean #safe #directory`

---

### `rmdir`

Remove empty directories.  

```bash
rmdir [OPTION] DIRECTORY
```

📌 **Tags**: `#delete #directory #empty #remove`

---

### `source`

Run a script in the current shell context.  

```bash
source <filename> [args]
```

📌 **Tags**: `#script #load #bash #env #current-shell`

---

### `split`

Split files into parts by size or lines.  

```bash
split [options] [input] [prefix]
```

**Options**:

- `-b <size>` : Bytes per part
- `-l <lines>` : Lines per part
- `-n <CHUNKS>` : Number of pieces

📌 **Tags**: `#split #file #batch #largefile #automation`

---

### `tar`

Create, list, or extract `.tar` archives.  

```bash
tar [options] -f archive.tar [files]
```

**Options**:

- `-c` : Create archive
- `-x` : Extract files
- `-t` : List archive contents
- `-v` : Verbose
- `-z` : Use gzip
- `-j` : Use bzip2
- `-f` : File archive to work with

📌 **Tags**: `#archive #compress #extract #backup #tarball`

---

### `touch`

Create a file or update timestamp.  

```bash
touch filename
```

📌 **Tags**: `#create #file #timestamp #placeholder`

---

### `tree`

Visual tree view of directory structure.  

```bash
tree [options] [directory]
```

**Options**:

- `-a` : Show hidden files
- `-d` : Only directories
- `-f` : Show full paths
- `--help` : Show help

📌 **Tags**: `#directory #visual #filesystem #tree`

---
## 🧠
## Shell & Process Utilities

---

### `bash`

Run shell commands or scripts.  

```bash
bash [script]
bash -x script.sh   # Debug mode
```

**Debug within script**:

```bash
#!/bin/bash -x
```

**Sectional debug**:

```bash
set -x    # Start debug
set +x    # End debug
```

📌 **Tags**: `#shell #bash #script #debug #terminal`

---

### `declare`

Set variable types or attributes in Bash.  

```bash
declare [options] name="value"
```

**Options**:

- `-a` : Indexed array
- `-A` : Associative array
- `-i` : Integer
- `-l` / `-u` : Lower/Uppercase enforcement
- `-x` : Export variable
- `-f` / `-F` : Functions
- `-g` : Global inside functions

📌 **Tags**: `#bash #variables #types #declare #functions`

---

### `eval`

Evaluate a constructed string as a command.  

```bash
eval "echo Hello $USER"
```

📌 **Tags**: `#eval #shell #dynamic #command #execute`

---

### `export`

Export variables to subprocesses.  

```bash
export VAR=value
export -p             # Show exported vars
```

**Options**:

- `-n` : Unexport a variable
- `-f` : Export functions

📌 **Tags**: `#environment #export #variables #shell`

---

### `history`

Show, search, and manage command history.  

```bash
history              # Show all
history 20           # Show last 20
history | grep apt   # Search
```

**Shortcuts**:

- `!123` : Run command #123
- `Ctrl + r` : Reverse search
- `history -d [#]` : Delete entry
- `history -c` : Clear all
- `set +o history` / `set -o history` : Toggle logging

📌 **Tags**: `#history #commands #search #recall #bash`

---

### `printf`

Formatted string output.  

```bash
printf "Name: %s\n" "$USER"
```

📌 **Tags**: `#output #print #format #script #bash`

---

### `ps`

Show current processes.  

```bash
ps aux                # Show all processes
```

**Columns**:

- `USER`, `PID`, `%CPU`, `%MEM`, `VSZ`, `RSS`, `TTY`, `STAT`, `CMD`, `START`, `TIME`

**Options**:

- `a` : Show all users
- `u` : User format
- `x` : Include processes with no TTY

📌 **Tags**: `#process #monitor #task #ps #system`

---

### `read`

Read input from stdin into variables.  

```bash
read var
read -p "Name: " name
```

**Options**:

- `-a array` : Store as array
- `-s` : Silent (e.g., password)
- `-t N` : Timeout
- `-n N` / `-N N` : Character count
- `-i text` : Show default text (with `-e`)
- `-r` : Don't interpret `\`

📌 **Tags**: `#input #stdin #bash #prompt #read`

---

### `readline` (library)

Handles input line editing in Bash (used by `read`, shell prompt).

**Examples**:

- `C-a`, `C-e` : Beginning/end of line
- `C-r` / `C-s` : Reverse/forward history search
- `M-f`, `M-b` : Forward/backward word
- `C-p`, `C-n` : Up/down in history

📌 **Tags**: `#readline #keyboard #bash #navigation #input`

---

### `set`

Configure shell behavior or list variables.  

```bash
set -e        # Exit on error
set +x        # Turn off debug
```

**Options**:

- `-e` : Exit on any error
- `-x` : Print commands before executing
- `-u` : Error on unset variables
- `-f` : Disable filename expansion
- `-C` : Prevent overwriting via `>`

📌 **Tags**: `#shell #bash #settings #debug #fail-safe`

---

### `su`

Switch user (default is root).  

```bash
su [username]
```

**Options**:

- `-l`, `--login` : Full login shell
- `-c` : Run command as user

📌 **Tags**: `#user #root #su #switch #admin`

---

### `sync`

Flush filesystem buffers to disk.  

```bash
sync
```

**Free RAM cache** (use with care):

```bash
sync; echo 1 > /proc/sys/vm/drop_caches
```

📌 **Tags**: `#disk #flush #filesystem #memory #cache`

---

### `test`

Evaluate expressions (used in scripts).  

```bash
test $a -eq 1
```

Also used via `[ expression ]`

📌 **Tags**: `#conditional #script #comparison #logic`

---

### `tmux`

Terminal multiplexer for managing sessions (not fully included here).  
Launch with:

```bash
tmux
```

📌 **Tags**: `#terminal #multiplexer #session #tmux`

---

### `unset`

Unset variables or functions in shell.  

```bash
unset varname
unset -f funcname
```

📌 **Tags**: `#shell #variables #cleanup #unset`

---
## 🌐
## Networking & Connectivity

---

### `curl`

Transfer data to/from a server using supported protocols.  

```bash
curl [options] [URL]
```

**Common options**:

- `-O` : Save as remote file name
- `-o <file>` : Save as custom name
- `-L` : Follow redirects
- `-I` : Headers only (HEAD request)
- `-d <data>` : POST data
- `-u <user:pass>` : Authentication
- `-C -` : Resume download
- `-s`, `-S` : Silent and show errors
- `--http2` : Use HTTP/2
- `-v` : Verbose output
- `--help` : Show help

📌 **Tags**: `#networking #http #download #api #web`

---

### `dig`

Query DNS records manually.  

```bash
dig [@server] name [type]
```

**Options**:

- `-x` : Reverse DNS lookup

📌 **Tags**: `#dns #lookup #resolver #dig #network-tools`

---

### `hostnamectl`

Show or set system hostname and related metadata.  

```bash
hostnamectl [subcommand]
```

**Commands**:

- `status` : Show current settings
- `set-hostname <name>` : Change hostname
- `set-icon-name`, `set-chassis` : System metadata

📌 **Tags**: `#hostname #identity #systemd #host #networking`

---

### `ifconfig` *(deprecated)*

Display or configure network interfaces.  

```bash
ifconfig
```

📌 Replaced by `ip`.

📌 **Tags**: `#interfaces #deprecated #network #ifconfig`

---

### `ip`

Modern interface for managing network settings.  

```bash
ip [options] object {command}
```

**Common examples**:

- `ip link show`
- `ip address`
- `ip route`
- `ip neigh`

**Objects**: `link`, `addr`, `route`, `neigh`, `tunnel`, etc.

📌 **Tags**: `#network #ip #interfaces #route #iproute2`

---

### `journalctl`

View logs from systemd-based services.  

```bash
journalctl [options]
```

**Options**:

- `-u <unit>` : Logs for specific service
- `-f` : Follow log (like tail)
- `-n N` : Show last N lines
- `-r` : Reverse order
- `-S`, `-U` : Since/Until date/time
- `-p` : Filter by priority
- `-x` : Add context
- `--disk-usage`, `--help`, `-k` : Kernel logs

📌 **Tags**: `#logs #journal #systemd #debug #services`

---

### `locate`

Search file names from a prebuilt database.  

```bash
locate pattern
```

Run `sudo updatedb` to refresh file database.

📌 **Tags**: `#find #files #locate #index #fast-search`

---

### `netstat` *(deprecated)*

Show networking connections, routing, and stats.  

```bash
netstat -anrt
```

📌 Use `ss` instead.

📌 **Tags**: `#network #socket #deprecated #netstat`

---

### `nmcli`

Command-line interface for NetworkManager.  

```bash
nmcli [options] object {command}
```

**Examples**:

- `nmcli connection show --active`
- `nmcli connection delete <UUID>`

**Objects**: `con`, `dev`, `nm`

**Options**:

- `-t`, `-p` : terse / pretty
- `-m` : mode
- `-f` : fields
- `-h` : help

📌 **Tags**: `#network #wifi #nmcli #connection #cli`

---

### `nm-connection-editor`

GTK GUI for editing NetworkManager connections.  

```bash
nm-connection-editor [options]
```

**Options**:

- `--create`
- `--edit=<uuid>`
- `--type=TYPE`
- `--show`

📌 **Tags**: `#network #gui #connection #nm #editor`

---

### `nmtui`

Text UI for NetworkManager (in terminal).  

```bash
nmtui
```

Launches a menu to connect, edit, and change hostnames.

📌 **Tags**: `#network #terminal #wifi #ethernet #tui`

---

### `nslookup`

Simple DNS query tool (interactive or one-shot).  

```bash
nslookup [domain] [server]
```

📌 **Tags**: `#dns #lookup #ip #resolver #nslookup`

---

### `ping`

Test network connectivity with ICMP.  

```bash
ping [host]
```

📌 **Tags**: `#ping #network #connectivity #icmp #diagnostics`

---

### `proxychains`

Force apps to use SOCKS/HTTP proxies like Tor.  

```bash
proxychains ./app
```

**Config**: `/etc/proxychains.conf`

📌 **Tags**: `#proxy #tor #routing #network #anonymity`

---

### `scp`

Secure copy between hosts via SSH.  

```bash
scp [options] source target
```

**Options**:

- `-i <identity_file>` : Use custom key
- `-r` : Recursive copy (for dirs)

📌 **Tags**: `#scp #ssh #file-transfer #remote #copy`

---

### `sftp`

Interactive file transfer over SSH.  

```bash
sftp username@host
```

**Common commands**:

- `get file`, `put file`, `ls`, `lls`, `?`, `quit`

📌 **Tags**: `#file-transfer #ssh #sftp #interactive #remote`

---

### `sha256sum`

Calculate or verify SHA-256 checksums.  

```bash
sha256sum file
```

**Options**:

- `--help` : Show help

📌 **Tags**: `#checksum #integrity #security #sha256`

---

### `smartctl`

Read SMART data from disk drives.  

```bash
smartctl [options] /dev/sdX
```

**Options**:

- `-h`, `--help` : Show help

📌 **Tags**: `#smart #disk #health #monitor #storage`

---

### `ss`

Socket statistics (replacement for `netstat`).  

```bash
ss [options]
```

**Options**:

- `-t`, `-u` : TCP/UDP
- `-l` : Listening sockets
- `-a` : All sockets
- `-n` : No DNS resolution
- `-p` : Show processes
- `--help`

**Example**:

```bash
ss -tunlp
```

📌 **Tags**: `#socket #connections #ports #ss #network`

---

### `ssh`

Connect to remote host via SSH.  

```bash
ssh user@host [options]
```

**Options**:

- `-p` : Custom port
- `-i` : Identity file
- `-x` : Disable X forwarding

**Key-related**:

- `ssh-keygen` : Generate key
- `ssh-copy-id` : Upload key to server
- `ssh-add -l` : List keys in agent

📌 **Tags**: `#ssh #remote #login #secure #terminal`

---

### `tcpdump`

Packet capture and analysis tool.  

```bash
tcpdump [options]
```

**Options**:

- `-c <num>` : Stop after <num> packets

📌 **Tags**: `#sniffer #packets #network #tcpdump #capture`

---

### `tor-instance-create`

Set up a named Tor relay instance.  

```bash
tor-instance-create mynode
systemctl start tor@mynode
```

**Directories**:

- `/etc/tor/instances/<name>/torrc`
- `/var/lib/tor-instances/<name>`

📌 **Tags**: `#tor #onion #privacy #daemon #instance`

---

### `traceroute`

Trace packet hops to a destination.  

```bash
traceroute [host] [options]
```

- `--help` : Show usage

📌 **Tags**: `#network #trace #route #diagnostic #hops`

---
## 🔐
## Security & Permissions

---

### `chfn`

Change user info fields (full name, room, work phone, etc.).  

```bash
chfn [options]
```

**Options**:

- `-h`, `--help` : Show help and exit

📌 **Tags**: `#user #profile #account #info #chfn`

---

### `chgrp`

Change group ownership of a file or directory.  

```bash
chgrp [OPTION] GROUP FILE
```

📌 **Tags**: `#group #permissions #ownership #chgrp`

---

### `chmod`

Change file or directory permission bits.  

```bash
chmod [options] mode file
```

**Symbolic examples**:

- `u=rwx`, `g=rw`, `o=r`
- `chmod u+x script.sh`

**Numeric values**:

- `7` = rwx, `6` = rw-, `5` = r-x, `4` = r--

**Options**:

- `-R`, `--recursive` : Apply to subdirs/files
- `--help` : Show help

📌 **Tags**: `#permissions #chmod #access #files #security`

---

### `chown`

Change file or directory owner and/or group.  

```bash
chown [OPTION] OWNER[:GROUP] FILE
```

**Options**:

- `-R` : Recursive

**Examples**:

```bash
sudo chown user file
sudo chown -R user:group folder
```

📌 **Tags**: `#ownership #chown #user #group #files`

---

### `loginctl`

Query and control user logins (via systemd-logind).  

```bash
loginctl [options] {command} [name]
```

**Commands**:

- `list-sessions`
- `show-session SESSION_ID --all`
- `show-user USERNAME`
- `show-user USERNAME --property=PROPERTY`

📌 **Tags**: `#login #session #systemd #user #management`

---

### `passwd`

Change a user's password.  

```bash
passwd [username]
```

Prompts for new password. If no user is given, changes current user’s password.

📌 **Tags**: `#password #security #auth #passwd`

---

### `sudo`

Run command as another user (default: root).  

```bash
sudo command
```

**Usage**:

```bash
sudo apt update
```

📌 **Tags**: `#sudo #privilege #root #admin #elevation`

---

### `su`

Switch user. Defaults to root if no username given.  

```bash
su [options] [-] [user]
```

**Options**:

- `-l`, `--login` : Start a login shell
- `-c` : Run specific command
- `exit` : Return to original user

📌 **Tags**: `#user #switch #root #su #admin`

---

### `unset`

Remove shell variables or function definitions.  

```bash
unset [-fv] name
```

**Options**:

- `-v` : Unset variable
- `-f` : Unset function

📌 **Tags**: `#shell #variables #unset #cleanup #bash`

---
## 📊
## Monitoring & Diagnostics

---

### `bmon`

Terminal-based bandwidth monitor with graphs.  

```bash
bmon
```

Visualizes bandwidth per interface.

📌 **Tags**: `#bandwidth #monitor #interface #network #bmon`

---

### `dmesg`

Print messages from the kernel ring buffer.  

```bash
dmesg
```

Useful for debugging device initialization and hardware issues.

📌 **Tags**: `#kernel #boot #hardware #diagnostics #dmesg`

---

### `dmidecode`

Display hardware info from BIOS/firmware.  

```bash
dmidecode [OPTIONS]
```

**Examples**:

```bash
dmidecode -t 17 | grep Speed
dmidecode -t memory
```

📌 **Tags**: `#hardware #bios #memory #system #dmidecode`

---

### `free`

Show memory usage (RAM + swap).  

```bash
free -h
```

**Columns**:

- `total`, `used`, `free`, `shared`, `buffers`, `cache`, `available`

📌 **Tags**: `#memory #usage #free #ram #swap`

---

### `hwinfo`

Detailed probe of all system hardware.  

```bash
hwinfo [--short] [--<HARDWARE_ITEM>] [--log FILE]
```

**Examples**:

- `hwinfo --short`
- `hwinfo --cpu`
- `hwinfo --usb`

📌 **Tags**: `#hardware #system #probe #device #info`

---

### `iostat`

Monitor CPU and disk I/O usage.  

```bash
iostat [options] [interval] [count]
```

**Options**:

- `-c` : CPU usage
- `-d` : Disk usage
- `-x` : Extended stats
- `-p` : Per-partition stats
- `-k`, `-m` : KB/MB output

📌 **Tags**: `#iostat #cpu #disk #performance #monitor`

---

### `journalctl`

View logs collected by `systemd-journald`.  

```bash
journalctl [options]
```

**Options**:

- `-u <unit>` : Logs for a service
- `-f` : Follow log
- `-n <N>` : Show last N lines
- `-S`, `-U` : Date/time filters
- `-p` : Filter by priority (e.g., `info`, `err`)
- `-x` : Show explanations
- `-k` : Kernel logs

📌 **Tags**: `#systemd #logs #debug #journal #service`

---

### `last`

Show login history from `/var/log/wtmp`.  

```bash
last
```

📌 **Tags**: `#auth #logins #history #sessions #last`

---

### `lastb`

Show failed login attempts from `/var/log/btmp`.  

```bash
lastb
```

**Options**:

- `-a` : Show host in last column
- `-d` : Resolve IP
- `-F` : Full timestamps

📌 **Tags**: `#failed-login #auth #security #lastb`

---

### `lsof`

List open files and the processes using them.  

```bash
lsof [options]
```

**Options**:

- `+D <dir>` : All open files in directory
- `-u <user>` : Opened by user
- `-c <cmd>` : Filter by process name
- `-p <PID>` : Filter by PID
- `-i` : Network connections
- `-R` : Show parent processes

📌 **Tags**: `#open-files #processes #lsof #network #debug`

---

### `ps`

Display active processes.  

```bash
ps aux
```

**Options**:

- `a` : All users
- `u` : Show user format
- `x` : Include background/daemon processes

**Common columns**:  
`PID`, `USER`, `%CPU`, `%MEM`, `VSZ`, `RSS`, `STAT`, `COMMAND`

📌 **Tags**: `#process #cpu #tasks #system #ps`

---

### `smartctl`

Query and test SMART-capable hard drives.  

```bash
smartctl [options] /dev/sdX
```

**Options**:

- `-a` : Full info
- `-H` : Health status
- `-t short` or `long` : Run self-tests

📌 **Tags**: `#disk #smart #health #monitor #drives`

---

### `top`

Dynamic real-time view of system processes.  

```bash
top
```

**Options**:

- `-h` : Show help
- `-b` : Batch mode (for logging)
- `-n <N>` : Run for N iterations
- `-d <secs>` : Refresh delay

📌 **Tags**: `#process #monitor #cpu #memory #top`

---

### `uptime`

Display current uptime, user count, and load average.  

```bash
uptime
```

📌 **Tags**: `#uptime #load #cpu #monitor #system`

---

### `watch`

Run a command repeatedly and display output.  

```bash
watch [options] <command>
```

**Options**:

- `-n <N>` : Interval in seconds
- `-d` : Highlight changes
- `-t` : No header
- `-h` : Help

📌 **Tags**: `#watch #loop #monitor #periodic #terminal`

---
## 🔧
## Device & Disk Utilities

---

### `blkid`

Identify block devices and display attributes (UUID, LABEL, TYPE).  

```bash
blkid
```

Used to reference disks in `fstab` or troubleshooting mount issues.

📌 **Tags**: `#disk #uuid #mount #device #filesystem`

---

### `cryptsetup`

Manage encrypted volumes with LUKS or plain dm-crypt.  

```bash
cryptsetup <action> [options] <args>
```

**Common actions**:

- `luksFormat`, `luksOpen`, `luksClose`, `status`

Supports advanced formats like:

- `LUKS`, `plain`, `loop-AES`, `VeraCrypt`, `BitLocker`

📌 **Tags**: `#encryption #luks #disk #security #cryptsetup`

---

### `dd`

Low-level tool for copying and converting raw data.  

```bash
dd if=<input> of=<output> [options]
```

**Options**:

- `bs=SIZE` : Read/write block size (e.g., `1M`)
- `count=N` : Number of blocks to copy
- `if=FILE` / `of=FILE` : Input/output files
- `status=progress` : Show live progress
- `skip=N`, `seek=N` : Skip input/output blocks

📌 **Tags**: `#dd #copy #raw #disk #image #clone`

---

### `fdisk`

Interactive partition manager for MBR/GPT tables.  

```bash
fdisk /dev/sdX
```

**Options**:

- `-l` : List partitions
- `-h` : Show help

📌 **Tags**: `#partition #fdisk #mbr #disk #format`

---

### `lsblk`

List block devices in tree form (no RAM disks).  

```bash
lsblk [options] [device]
```

**Options**:

- `--help` : Show column info

📌 **Tags**: `#lsblk #device #tree #block #partition`

---

### `lshw`

Detailed hardware description from system BIOS.  

```bash
lshw [options]
```

**Options**:

- `-short` : Compact summary
- `-C <class>` : Show only specific class (`memory`, `cpu`, etc.)

📌 **Tags**: `#hardware #inventory #system #lshw #cpu #ram`

---

### `mdadm`

Tool for managing software RAID arrays.  

```bash
mdadm [mode] <raiddevice> [options] <component-devices>
```

**Options**:

- `-E`, `--examine` : View array metadata on a device
- `--create`, `--assemble`, `--detail`

📌 **Tags**: `#raid #mdadm #disk #redundancy #linux`

---

### `mkswap`

Initialize a swap area on a file or device.  

```bash
mkswap [options] /path/to/file
```

**Typical setup**:

```bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=4096
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

📌 **Tags**: `#swap #memory #mkswap #swapfile #virtual-memory`

---

### `mount`

Mount a filesystem to the directory tree.  

```bash
mount [options] device dir
```

**Common examples**:

```bash
sudo mount /dev/sdb1 /mnt/usb
```

**Options**:

- `-t <type>` : Filesystem type
- `-o <options>` : Mount options like `rw`, `uid=1000`, etc.

📌 **Tags**: `#mount #filesystem #fstab #device #attach`

---

### `swapon` / `swapoff`

Enable or disable swap usage on device or file.  

```bash
swapon [options] <device>
swapoff [options] <device>
```

**Options**:

- `--show` : Show active swap
- `-h`, `--help` : Show help

📌 **Tags**: `#swap #memory #swapon #swapoff #virtual-memory`

---

### `umount`

Unmount a filesystem.  

```bash
umount [options] <device|directory>
```

**Options**:

- `-a` : Unmount all
- `-r`, `-f`, `-l`, `-n` : Additional force/safety modes
- `-h` : Show help

**Example**:

```bash
sudo umount /dev/sdb1
```

📌 **Tags**: `#umount #unmount #filesystem #detach #storage`

---
## 🧪
## Development & Tools

---

### `awk`

Pattern scanning and processing tool for structured text.  

```bash
awk [options] 'pattern { action }' input-file
```

**Common built-in variables**:

- `$0`, `$1`, ..., `$NF` : Entire line and fields
- `FS`, `OFS` : Input/output field separators
- `NR`, `FNR` : Record numbers
- `FILENAME` : Current file name

**Options**:

- `-F` : Set field delimiter (e.g., `-F,`)

📌 **Tags**: `#awk #text #processing #csv #script`

---

### `expr`

Evaluate expressions (math, strings, comparisons).  

```bash
expr 1 + 2
expr match "abc123" '[a-z]*'
```

**Operators**:

- Arithmetic: `+`, `-`, `\*`, `/`, `%`
- Comparison: `=`, `!=`, `<`, `<=`, `>`, `>=`

📌 **Tags**: `#math #comparison #string #expr #shell`

---

### `make` *(commonly used but not previously listed)*

Build automation tool, often used for compiling code via Makefile.  

```bash
make [target]
```

📌 **Tags**: `#build #makefile #compile #automation #c`

---

### `pycharm.sh`

Launch PyCharm IDE from terminal.  

```bash
./pycharm.sh
```

**Usage**:

```bash
cd /opt/pycharm*/bin
./pycharm.sh
```

📌 **Tags**: `#ide #python #pycharm #gui #dev`

---

### `qemu-img`

Manage disk image files for virtual machines.  

```bash
qemu-img command [options]
```

**Common commands**:

- `create` : Make new disk image
- `info` : Show image info
- `resize` : Resize image
- `convert` : Change formats

**Example**:

```bash
qemu-img create -f qcow2 disk.qcow2 20G
```

📌 **Tags**: `#qemu #virtual #image #disk #qcow2`

---

### `read`

Read input from user or script.  

```bash
read -p "Enter name: " name
```

**Options**:

- `-a array` : Save input to array
- `-s` : Silent (e.g., password)
- `-n N` : Read N characters
- `-t N` : Timeout
- `-r` : Raw input (no backslash escape)

📌 **Tags**: `#input #read #bash #prompt #script`

---

### `scrcpy`

Display/control Android device from desktop over USB or WiFi.  

```bash
scrcpy [options]
```

**Common options**:

- `--tcpip=<IP>` : Wireless mode
- `-K` : Disable software keyboard

📌 **Tags**: `#android #mirroring #usb #wifi #gui`

---

### `sed`

Stream editor for transforming text in pipelines or files.  

```bash
sed [options] 'script' file
```

**Options**:

- `-n` : Suppress default output
- `-e` : Add script
- `-i[SUFFIX]` : Edit in-place
- `-r` : Use extended regex
- `-f` : Load script from file

**Example**:

```bash
sed -i 's/foo/bar/g' file.txt
```

📌 **Tags**: `#sed #edit #stream #regex #in-place`

---

### `tee`

Read from stdin and write to both stdout and files.  

```bash
command | tee [options] file
```

**Options**:

- `-a` : Append to file
- `-i` : Ignore interrupt

📌 **Tags**: `#tee #stdout #log #stream #write`

---

### `tr`

Translate or delete characters from input.  

```bash
tr [options] STRING1 [STRING2]
```

**Options**:

- `-d` : Delete characters
- `-s` : Squeeze repeats
- `-c` : Use complement
- `-t` : Truncate

**Example**:

```bash
echo "hello" | tr a-z A-Z
```

📌 **Tags**: `#translate #text #tr #convert #stream`

---

### `xargs`

Build and execute commands from stdin input.  

```bash
find . -name "*.txt" | xargs rm
```

**Options**:

- `-n N` : Use N items per command
- `-I {}` : Replace with placeholder
- `-0` : NUL-delimited input (safe for filenames with spaces)

📌 **Tags**: `#xargs #stdin #automation #command-builder`

---
## 📝
## Documentation & Help

---

### `help`

Show help for Bash built-in commands.  

```bash
help [builtin]
```

Only works in Bash shell.

📌 **Tags**: `#bash #help #builtin #reference #commands`

---

### `info`

GNU hypertext manual system (like man, but linked).  

```bash
info [command]
```

Navigation uses arrow keys, `Tab`, `Enter`, and `q` to quit.

📌 **Tags**: `#manual #gnu #info #documentation #cli`

---

### `man`

Display system manual pages.  

```bash
man [section] command
```

**Examples**:

```bash
man man         # Manual about 'man'
man bash        # Full Bash manual
```

📌 **Tags**: `#manual #manpages #documentation #help #linux`

---

### `tldr`

Show simplified, community-curated command summaries.  

```bash
tldr [command]
```

**Options**:

- `--help` : Show help

Requires installation (via `npm`, `apt`, etc.)

📌 **Tags**: `#docs #tldr #reference #cheatsheet #help`

---

### `whereis`

Find binary, source, and man page for a command.  

```bash
whereis [options] program
```

**Options**:

- `-b` : Binary only
- `-m` : Manual only
- `-s` : Source only
- `-u` : Show unusual matches
- `-BMS` : Specify search paths
- `-f` : Specify filenames (when using `-BMS`)

📌 **Tags**: `#whereis #lookup #docs #man #paths`

---

### `which`

Locate a program’s executable in your PATH.  

```bash
which [options] [--] command
```

Returns the absolute path to the executable.

📌 **Tags**: `#which #path #binary #lookup #cli`

---

### `yelp`

Launch Ubuntu’s graphical help viewer (GUI-based).  

```bash
yelp
```

📌 **Tags**: `#gui #help #ubuntu #manual #yelp`

---
## 📚
## Log Files & System Info

---

### 📂 Common System Log Files (located in `/var/log/`):

| File                                          | Purpose                                       |
| --------------------------------------------- | --------------------------------------------- |
| `auth.log`                                    | Authentication and sudo usage                 |
| `boot.log`                                    | Boot events and early startup                 |
| `dmesg`                                       | Kernel hardware messages                      |
| `dpkg.log`                                    | Package management activity                   |
| `kern.log`                                    | Kernel messages                               |
| `syslog`                                      | General system messages                       |
| `wtmp`                                        | Login history (read with `last`)              |
| `btmp`                                        | Failed login attempts (read with `lastb`)     |
| `apt/history.log`                             | Apt install/remove/upgrade logs               |
| `journal/`                                    | systemd journal logs (persistent with config) |
| `/var/opt/thinlinc/sessions/<user>/xinit.log` | ThinLinc session startup logs                 |
| `/var/lib/PackageKit/offline-update-competed` | “Update Installed” marker (delete if stuck)   |

📌 **Tags**: `#logs #auth #boot #apt #systemd #journal #login`

---

### 🔎 Useful Log Access Commands

```bash
sudo cat /var/log/boot.log              # View boot process
sudo dmesg                              # Kernel hardware logs
last                                    # Show login history
lastb                                   # Show failed login attempts
sudo cat /var/log/auth.log              # Sudo/auth events
cat /var/log/apt/history.log            # Apt history
swapon --show                           # Active swap usage
```

📌 **Tags**: `#log-viewing #login-history #apt-logs #auth-log`

---

### 🧹 Clear “Update Installed” Alert

```bash
sudo rm /var/lib/PackageKit/offline-update-competed
```

Fixes recurring “Software Update Installed” alerts.

📌 **Tags**: `#update #packagekit #gui-fix #alert #cleanup`

---
## ⚙
## Services & Daemons

---

### `openvpn`

Secure VPN tunneling using `.ovpn` config files.  

```bash
sudo openvpn --config path/to/config.ovpn
```

Provides encrypted tunnels using SSL. Requires config file from VPN provider.

📌 **Tags**: `#vpn #openvpn #tunnel #secure #remote`

---

### `pipewire-pulse` (via `systemctl --user`)

Control the user-level PulseAudio service via Pipewire.  

```bash
systemctl --user status pipewire-pulse
systemctl --user start pipewire-pulse
systemctl --user stop pipewire-pulse
systemctl --user restart pipewire-pulse
```

📌 **Tags**: `#audio #pipewire #pulse #sound #service`

---

### `proxychains`

Force any command to run through configured proxies (e.g., Tor).  

```bash
proxychains ./command
```

**Config file**:

```bash
/etc/proxychains.conf
```

Used in combination with Tor or SOCKS5 proxies.

📌 **Tags**: `#proxy #privacy #tor #routing #proxychains`

---

### `rsyslogd`

System log daemon (replaces syslogd).  

```bash
rsyslogd [options]
```

**Options**:

- `-d`, `-n` : Debug / don’t daemonize
- `-f` : Specify config file (`/etc/rsyslog.conf`)
- `-v` : Show version

📌 **Tags**: `#logs #rsyslog #daemon #system #messages`

---

### `systemctl`

Manage services, daemons, and system units under `systemd`.  

```bash
systemctl [options] <command> [unit...]
```

**Commands**:

- `start`, `stop`, `restart`, `reload`
- `enable`, `disable` : Control boot autostart
- `status` : Show service state
- `list-units` : Show active units
- `edit <unit>` : Override or extend a unit file

**Examples**:

```bash
systemctl list-units --type=service
systemctl enable ssh
```

📌 **Tags**: `#systemctl #services #daemon #systemd #control`

---

### `tor-instance-create`

Create and manage additional named Tor instances.  

```bash
tor-instance-create relayname
systemctl start tor@relayname
```

**Config Paths**:

- `/etc/tor/instances/<name>/torrc`
- `/var/lib/tor-instances/<name>`

📌 **Tags**: `#tor #anonymity #onion #instance #relay #daemon`

---
## 🛡
## Firewall & Access Control

---

### `scp`

Securely copy files/directories between local and remote systems using SSH.  

```bash
scp [options] source user@host:destination
```

**Options**:

- `-i <identity_file>` : Use SSH key
- `-r` : Copy directories recursively

**Examples**:

```bash
scp file.txt user@host:/path
scp -r dir/ user@host:/path
```

📌 **Tags**: `#scp #ssh #file-transfer #remote #copy`

---

### `sftp`

Secure interactive file transfer over SSH.  

```bash
sftp username@host
```

**Common commands**:

- `get file` : Download from remote
- `put file` : Upload to remote
- `ls`, `lls`, `cd`, `lcd`, `?`, `quit`

📌 **Tags**: `#sftp #ssh #interactive #transfer #file`

---

### `ssh`

Connect to remote systems via encrypted terminal session.  

```bash
ssh [options] user@host
```

**Options**:

- `-p <port>` : Custom port
- `-i <identity_file>` : Use SSH key
- `-x` : Disable X forwarding

**Key management**:

```bash
ssh-keygen -t ed25519 -C "comment"
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
ssh-add -l
```

**Config files**:

- `~/.ssh/config` : Per-user SSH config
- `/etc/ssh/ssh_config` : System-wide SSH config
- `/etc/ssh/sshd_config` : Daemon config

📌 **Tags**: `#ssh #remote #access #auth #key`

---

### `su`

Switch to another user (defaults to root).  

```bash
su [options] [-] [user]
```

**Options**:

- `-l`, `--login` : Full login shell
- `-c` : Run command as target user
- `exit` : Return to original user

📌 **Tags**: `#su #switch-user #root #login #shell`

---

### `ufw`

Uncomplicated Firewall — CLI frontend for managing iptables rules.  

```bash
ufw [command] [rule]
```

**Common commands**:

- `status [numbered]` : View current rules
- `allow <port/service>` : Allow traffic
- `deny <port/service>` : Block traffic
- `delete <rule>` : Remove rule
- `start`, `stop`, `restart` : Control firewall
- `allow <port> comment 'description'` : Annotate rule

📌 **Tags**: `#firewall #ufw #iptables #security #access`

---
## 🚀
## Tips, Fixes & Config Examples

---

### 🧹 Fix Stuck “Update Installed” Notification

Remove the flag file that causes update notifications to repeat.

```bash
sudo rm /var/lib/PackageKit/offline-update-competed
```

📌 **Tags**: `#update #gui #bugfix #packagekit #alert`

---

### 🔑 Enable SSH on New Ubuntu Install

```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl status ssh
sudo ufw allow ssh
ssh-keygen -f ~/.ssh/known_hosts -R "192.168.1.241"
```

📌 **Tags**: `#ssh #enable #ubuntu #fresh-install #remote-access`

---

### 🌐 Proxychains + Tor Setup

Start and test Tor SOCKS5 proxy:

```bash
sudo systemctl start tor
sudo systemctl status tor
netstat -lt | grep 9050
```

Run command via Tor:

```bash
proxychains ./command
```

**Config File**:

```bash
/etc/proxychains.conf
```

📌 **Tags**: `#tor #proxy #anonymity #network #socks5`

---

### 🧠 Swap File — Create, Enable, Delete

**Create and enable**:

```bash
sudo dd if=/dev/zero of=/swapfile2 bs=1M count=4096
sudo chmod 600 /swapfile2
sudo mkswap /swapfile2
sudo swapon /swapfile2
```

**Make permanent**:
Add to `/etc/fstab`:

```
/swapfile2 none swap defaults 0 0
```

**Remove**:

```bash
sudo swapoff -v /swapfile2
sudo rm /swapfile2
sudo nano /etc/fstab  # remove line
```

📌 **Tags**: `#swap #memory #performance #virtual-memory #fstab`

---

### 📁 fstab Mount Entry Example (TrueNAS NFS Share)

**fstab line**:

```
192.168.1.240:/mnt/Main/nfs /mnt/nfs nfs uid=1000,gid=1000,mountvers=3 0 0
```

**Reload mounts**:

```bash
sudo mount -av
```

📌 **Tags**: `#fstab #mount #nfs #nas #network-storage`

---

### 🗂 Connect to Samba Share via File Manager

Use in Nautilus or "Connect to Server" dialog:

```
smb://192.168.1.187
```

📌 **Tags**: `#samba #smb #fileshare #network #gui`

---

### 💾 Clear RAM Cache (non-destructive)

```bash
sync; echo 1 > /proc/sys/vm/drop_caches
```

📌 **Tags**: `#cache #memory #performance #flush #ram`

---

### 📦 Apt Package History Log

```bash
cat /var/log/apt/history.log
```

📌 **Tags**: `#apt #install-history #log #packages`

---

### 🕵️ View Boot and Login Logs

```bash
sudo cat /var/log/boot.log
last             # from /var/log/wtmp
lastb            # from /var/log/btmp
```

📌 **Tags**: `#boot #login #history #auth #logs`

---

### 🔐 Reset SSH Host Key (IP reuse fix)

```bash
ssh-keygen -f ~/.ssh/known_hosts -R "192.168.1.241"
```

📌 **Tags**: `#ssh #hostkey #ip-conflict #known_hosts #security`

---

### 🔗 Split Large Files for Uploads

**By size (100MB)**:

```bash
split -b 100m file.zip
```

**By line count (every 4 lines)**:

```bash
split -l 4 bigfile.txt part_
```

📌 **Tags**: `#split #large-files #backup #archive #chunk`

---
