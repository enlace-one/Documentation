# Top Useful Hints

Use tab-complete! 

# Common
`ls`	`cd ..`	`pwd`	`exit`

`mkdir` 	`rmdir`	`nano`	`less`

`cat`	`head`	`tail`

`md5sum filename.txt`

`sha256sum filename.txt`

`cp source to dest`

`echo “hidden text” > filename.txt:hiddenpart`

`more < filename.txt:hiddenpart`

# locate password - find files
`grep [searchterm] /etc/shadow` a pwfile

`ls -l  | grep 'yyyy-mm-dd'` Find files by date modified or name

`find -iname "me.txt"`

`logger “[message]”`

`cd /var/log` syslog

`apt-get install [programname]`

`apt-get remove [programname]`

`apt-get update`

`apt-get upgrade` 

`apt-get clean`

`apt update –y && apt upgrade –y && apt 	dist-upgrade `


`adduser [username] sudo`

`su 	#switch user`

`id root 	#info about root`

`whoami`

`history`

`chmod [u (user) | g (group) | o (others) | a 	(all)] [+ | - | =] [r | w | x]`
`chmod a=r` read only for all

`sudo apt install app_name`
`service app_name start`
`service app_name stop`

# Network
`arp-scan 192.168.1.0/24`

`traceroute 4.4.4.4`

`ping 4.4.4.4`

`ifconfig`

`iwconfig`

`dig google.com` 	#dns lookup

`dig dell.com MX`

`dig dell.com axfr` 	#attempts zone transfer

`dnsenum dell.com`

`arp –a` 		#show arp table

`route` #show route table

`curl google.com` 	#gets 

`rdesktop www.dell.com`

`whois google.com`

`telnet www.campus.edu 21` #service p21

`telnet 10.9.2.3`

`netstat -r`	#view routing table

`scanless -t example.com -s spiderip

`scanless -l` #gives a list of services instead of spiderip

`ifconfig eth0 0.0.0.0 up `

`ifconfig eth0 1.1.1.1 netmask 255.255.255.0` #Sets IP 

# Vim Cheat Sheet

## Basics
- `vim <filename>`: Open a file in Vim.
- `:q`: Quit Vim.
- `:q!`: Quit without saving changes.
- `:w`: Save the current file.
- `:wq`: Save and quit.
- `:x`: Save and quit (same as `:wq`).
- `u`: Undo the last change.
- `Ctrl + r`: Redo the last undone change.

---

## Modes
- **Normal mode**: Default mode for navigation and commands.
- **Insert mode**: Enter text (`i`, `I`, `a`, `A`, `o`, `O` to enter).
- **Visual mode**: Select text (`v` for character-wise, `V` for line-wise, `Ctrl + v` for block).
- **Command mode**: Execute commands (type `:` to enter).

---

## Navigation
- `h`: Move left.
- `l`: Move right.
- `j`: Move down.
- `k`: Move up.
- `0`: Move to the beginning of the line.
- `^`: Move to the first non-whitespace character of the line.
- `$`: Move to the end of the line.
- `w`: Jump to the beginning of the next word.
- `e`: Jump to the end of the current/next word.
- `b`: Jump to the beginning of the previous word.
- `gg`: Go to the beginning of the file.
- `G`: Go to the end of the file.
- `:n`: Go to line number `n`.

---

## Editing
- `x`: Delete the character under the cursor.
- `X`: Delete the character before the cursor.
- `dd`: Delete the current line.
- `yy`: Copy (yank) the current line.
- `p`: Paste after the cursor.
- `P`: Paste before the cursor.
- `r<character>`: Replace the character under the cursor.
- `cw`: Change the word under the cursor.

---

## Search and Replace
- `/text`: Search for `text` forward.
- `?text`: Search for `text` backward.
- `n`: Repeat the last search in the same direction.
- `N`: Repeat the last search in the opposite direction.
- `:%s/old/new/g`: Replace all occurrences of `old` with `new` in the file.

---

## Visual Mode
- `v`: Start visual mode (character-wise selection).
- `V`: Start visual mode (line-wise selection).
- `Ctrl + v`: Start visual mode (block selection).
- `d`: Delete selected text.
- `y`: Yank (copy) selected text.
- `>`, `<`: Indent or un-indent selected text.

---

## Advanced
- `:!<command>`: Run a shell command.
- `:set nu`: Show line numbers.
- `:set nonu`: Hide line numbers.
- `:split <filename>`: Split the window horizontally.
- `:vsplit <filename>`: Split the window vertically.
- `Ctrl + w + w`: Switch between windows.

---

## Exiting Split Windows
- `:q`: Close the current split.
- `:qa`: Quit all windows.


