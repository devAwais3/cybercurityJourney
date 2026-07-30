# LINUX COMMAND LINE

The Linux command line is a text interface to your computer.
Also known as shell, terminal, console, command prompts and many others, is a computer program intended to interpret commands.
Allows users to execute commands by manually typing at the terminal, or has the ability to automatically execute commands which were programmed in “Shell Scripts”.

## HISTORY
   - The Bourne Shell (sh) was originally developed by Stephen Bourne while working at Bell Labs.
   - Released in 1979 in the Version 7 Unix release distributed to colleges and universities.
   - The Bourne Again Shell (bash) was written as a free and open source replacement for the Bourne Shell.
Given the open nature of Bash, over time it has been adopted as the default shell on most Linux systems.

## Some Basic linux commands

### pwd : Print Working Directory
- `pwd` → shows full path of current directory

### cd : Change Directory
- `cd <path>` → go to specified directory
- `cd ..` → move up one directory
- `cd` → go to home directory
- `cd -` → go to previous directory
- `cd ~` → go to home directory (alternative)
- `cd /` → go to root directory

### ls : List
- `ls` → list files/folders in current directory
- `ls -a` → show all files, including hidden (dotfiles)
- `ls -l` → long format (permissions, owner, size, date)
- `ls -al` / `ls -la` → combine hidden + long format
- `ls -R` → list recursively (includes sub-directories)
- `ls -h` → human-readable file sizes (with -l)
- `ls -t` → sort by modification time
- `ls -S` → sort by file size

### cat : Concatenate/display file content
- `cat filename` → print file content to screen
- `cat > filename` → create new file (type content, Ctrl+D to save)
- `cat filename1 filename2 > filename3` → merge two files into a new one
- `cat -n filename` → display with line numbers

### cp : Copy
- `cp source destination` → copy file
- `cp -r source destination` → copy directory (recursive)
- `cp -i source destination` → prompt before overwrite
- `cp -v source destination` → verbose (show what's copied)

### mv : Move/Rename
- `mv source destination` → move file/folder
- `mv oldname newname` → rename file/folder
- `mv -i source destination` → prompt before overwrite

### mkdir: Make Directory
- `mkdir dirname` → create new directory
- `mkdir -p path/to/dir` → create nested directories at once
- `mkdir dir1 dir2` → create multiple directories

### rm : Remove
- `rm filename` → delete file
- `rm -r dirname` → delete directory and all contents
- `rm -f filename` → force delete (no confirmation)
- `rm -rf dirname` → force delete directory + contents (use carefully)
- `rm -i filename` → prompt before deleting
