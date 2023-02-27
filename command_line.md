# Commands

## General Linux Commands

Here are collected Linux-commands, which did not find a place in other sections.

- Clear terminal screen:
```bash
clear
```
- Display current date and time
```bash
date
```
- Display in a convenient form the previous, current and next month
```bash
cal -3
```
- Display information about the domain **linux.org**
```bash
whois linux.org
```
- Save the entire site by converting links for offline use. Copying is done to a depth of 5 levels
```bash
wget --convert-links -r http://www.linux.org/
```
- Download the file **linuxmint-21.1-cinnamon-64bit.iso** to the current folder
```bash
wget https://linuxmint.astra.in.ua/iso/stable/21.1/linuxmint-21.1-cinnamon-64bit.iso
```
- Connect to **host** as **user**
```bash
ssh user@host
```
- Connect to **host** on port **port** as **user**
```bash
ssh -p port user@host
```
- Run last command
```bash
!!
```
- Display the last 50 commands typed
```bash
history | tail-50
```
- End current user session
```bash
exit
```

## Linux commands for working with directories and files

In this list, you will see Linux commands that are designed to create and remove directories and files. The list also includes commands for navigating between files.

- Display current path
```bash
pwd
```
- List directories and files
```bash
ls
```
- Display a formatted list of all directories and files, including hidden ones
```bash
ls -laX
```
- View permissions on files and directories in the current directory
```bash
ls -lh
```
- To go to your home directory
```bash
cd
```
- To go to the **/home** directory
```bash
cd /home
```
- To go to the directory one level higher
```bash
cd..
```
- To move to a directory 2 levels higher
```bash
cd ../..
```
- To switch to the directory where you were before switching to the current directory
```bash
cd-
```
- Create empty file **/home/file**
```bash
touch /home/file
```
- Output contents of **file**
```bash
more file
```
- Output first 10 lines of **file**
```bash
head file
```
- Display last 10 lines of **file**
```bash
tail file
```
- Output the contents of the file **file1** page by page to the standard output device, but with the ability to scroll in both directions (up and down), search by content, etc.
```bash
less file1
```
- Display the contents of the file
```bash
cat /home/file
```
- Display the contents of the file in reverse order (the last line becomes the first, etc.)
```bash
tac file1
```
- Edit file
```bash
nano /home/file
```
- Edit file
```bash
gedit /home/file
```
- Copy **/home/hamster/file1.txt** to **/home/file2.txt**
```bash
cp /home/hamster/file1.txt /home/file2.txt
```
- Create a directory named **dir**
```bash
mkdir /home/hamster/dir
```
- Delete directory named **dir** if it is empty
```bash
rmdir /home/hamster/dir
```
- Delete directory with all files
```bash
rm -rf /home/hamster/dir
```
- Copy directory
```bash
cp -la /dir1 /dir2
```
- Rename directory
```bash
mv /dir1 /dir2
```
- Search for a file with a name containing **file**
```bash
locate file
```

## Linux commands: working with archives

Linux commands needed to work with archives.
- Create a tar archive named **file.tar** containing **files**
```bash
tar cf file.tar files
```
- Unpack **file.tar**
```bash
tar xf file.tar
```
- Create tar archive with Gzip compression
```bash
tar cf file.tar.gz files
```
- Unpack tar with Gzip
```bash
tarxzf file.tar.gz
```
- Create a tar archive with Bzip2 compression
```bash
tar cjf file.tar.bz2
```
- Unpack tar with Bzip2
```bash
tar xjf file.tar.bz2
```
- Compress **file** and rename to **file.gz**
```bash
gzip file
```
- Uncompress **file.gz** into **file**
```bash
gzip -d file.gz
```
- Decompresses the file **file1.bz2**
```bash
bunzip2 file1.bz2
```
- Compress file **file1** with maximum compression
```bash
gzip -9 file1
```
- Create a rar archive **file1.rar** and include the file **test_file** in it
```bash
rar a file1.rar test_file
```
- create a rar archive **file1.rar** and include **file1**, **file2** and **dir1** in it
```bash
rar a file1.rar file1 file2 dir1
```
- Unpack rar archive
```bash
rar x file1.rar
```
- Create a tar archive **archive.tar** containing the file **file1**
```bash
tar -cvf archive.tar file1
```
- Create a tar archive **archive.tar** containing the file **file1**, **file2** and **dir1**
```bash
tar -cvf archive.tar file1 file2 dir1
```
- Show the contents of the archive
```bash
tar -tf archive.tar
```
- Unpack the archive
```bash
tar -xvf archive.tar
```
- Unpack archive to /tmp
```bash
tar -xvf archive.tar -C /tmp
```
- Create an archive and compress it with bzip2 (The -j switch does not work on all *nix systems)
```bash
tar -cvfj archive.tar.bz2 dir1
```
- Unpack the archive and unpack it (The -j key does not work on all * nix systems)
```bash
tar -xvfj archive.tar.bz2
```
- Create an archive and compress it with gzip
```bash
tar -cvfz archive.tar.gz dir1
```
- Unpack the archive and unpack it
```bash
tar -xvfz archive.tar.gz
```
- Create compressed zip archive
```bash
zip file1.zip file1
```
- Create a compressed zip archive and include several files and / or directories in it
```bash
zip -r file1.zip file1 file2 dir1
```
- Decompress and unpack the zip archive
```bash
unzip file1.zip
```
## Linux commands to monitor performance

Here are the Linux commands needed to monitor the operation of the OS.

- Displays the current time and system operation without shutting down and rebooting
```bash
uptime
```
- For information about loaded processes, RAM consumption
```bash
top
```
- Extended online statistics about loaded processes
```bash
htop
```
- Used and free RAM and Swap file (-m indicates that data should be displayed in MB)
```bash
free -m
```
- Displays information about mounted partitions showing total, available and used space (The -h switch does not work on all *nix systems)
```bash
df -h
```
- Lists files and directories recursively sorted in ascending order of size and allows pagination
```bash
ls -lSr | more
```
- Calculates and displays the size occupied by the 'dir1' directory (The -h switch does not work on all *nix systems)
```bash
du -sh dir1
```
- Displays the size and names of files and directories, sorted by size
```bash
du -sk* | sort-rn
```

# Сonstruction

- Count the number of files in a folder
```bash
ls /home/captain | wc -l
```
