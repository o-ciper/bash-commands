# Bash Commands in Ubuntu

## Restart Network Manager

```bash
sudo systemctl restart NetworkManager.service
```

## List disk partitions excluding snaps

```bash
lsblk -e7
```

## List free disk spaces. Also clean up snap and loop devices from df output in Ubuntu 18.04 and 20.04

```bash
df -h -x squashfs -x tmpfs -x devtmpfs --total
```

You can add an alias for the `df` command to your .bashrc or .bash_aliases file if you wish

```bash
alias df='df -h -x squashfs -x tmpfs -x devtmpfs'
```

## Find where a program is installed

It works regardless of whether the program is in your path (/sbin, /usr/sbin, and /usr/local/sbin are often omitted for normal users; and third party products can be installed all over the place with /opt a common location)   or not.  It works with programs installed via package managers and added via other means.  It's completely independent of distribution package managers.

```bash
locate -r bin/<program_name>\$
```

for example:

```bash
locate -r bin/synaptic\$
```

or, `which`, if the the executable is in the $PATH.
`which` searches for executables in the directories specified by the environment variable PATH. And if found out, the full pathname of this executable will be printed. i.e. `which` searches only for binaries in $PATH.

```bash
which <executable_name>
```

or, `whereis` searches for executables, source files, and manual pages using a database built by system automatically.

```bash
whereis <executable_name>
```

or

```bash
apt-cache policy <program_name>
```

## Execute TRIM manually

```bash
sudo fstrim -av
```

This operation may last for minutes; it then looks as if the terminal has frozen. That's not true, however; simply wait patiently....

*Note: on a few SSD models (specifically two models from Crucial), executing this command when there's high disk activity (I/O activity), might cause problems. So only apply it when there's not much activity going on. Preferably with all other applications closed.*

## Bootup time

```bash
systemd-analyze
```

## Watch network traffic

```bash
sudo nethogs -a
```

## Update youtube-dl

If you installed it with `pip3` then use

```bash
pip3 install --upgrade youtube_dl
```

If you installed it with `sudo` then use

```bash
sudo pip3 install --upgrade youtube_dl
```

If you installed it with the `apt` package manager then use

```bash
youtube-dl -U
```

If you installed it with `curl` to `/usr/local/bin/` then you have to create a symlink because youtube-dl will probably produce the following error:

```bash
/usr/bin/env: ‘python’: No such file or directory
```

so create a symlink with

```bash
sudo ln -s /usr/bin/python3 /usr/local/bin/python
```

## Generate 12 character long password

```bash
pwgen -s 12 -1 -y
gen_pass 12 #Look at .bashrc for this. It's an alias.
```

## My local network ip address

```bash
hostname -I
```

## Search for a text with a pattern in a directory or file

```bash
grep -rnw '/path/to/somewhere/' -e 'pattern'
```

## List files and directories we have in the current directory but not hidden files

```bash
ls
```

## List every file and directory we have in the current directory including hidden files

```bash
ls -a
```

## Get the last command you ran that starts with for example `whereis`

```bash
!whereis
```

## Prepend to the last command you ran with `!!`

```bash
<prepended_command> !!
```

for example

```bash
sudo !!
```

## use space bar to expand the last command you ran when using `!!` or `!<commmand>`. But first you need to add `bind Space:magic-space` to the .bashrc

```bash
sudo !! # Hit space and the code will expand
```

## use ctrl-p to expand the last command you ran when using `!!` or `!<commmand>`. You don't need to modify .bashrc

```bash
!which # Hit space and the code will expand
```

## Gives a long list of files and directories we have in the current directory with more information about them but not hidden files

```bash
ls -l
```

## Gives a long list every file and directory we have in the current directory with more information about them including hidden files

```bash
ls -la
```

## Print current working directory with the absolute path

```bash
pwd
```

## `cd <target>` with target argument will change the directory to the target

```bash
cd /home/Desktop
```

## To go one level up to the root use

```bash
cd ..
```

## Go to home directory from where ever you are

```bash
cd
```

or

```bash
cd ~
```

## If you want to change directory and get back to the directory you were before, use for example

```bash
pushd /usr/var/wwww
```

Now to get back to where you were before

```bash
popd
```

## If you listed files and don't know what type those files are. A file might be a text file or it could be a folder

Because Linux doesn't necessarily need a file extension. In that case you can use

```bash
file <file_or_folder_name>
```

## Finding files

The `locate` command. It takes the filename of part of a filename as argument. It will give the absolute path of a file that contains the file name or part of it

```bash
locate <filename>
```

`locate` looks at a database for the locate command. If you issue the locate command on a fresh linux install it probably won't work, because a database is not created yet. Linux possibly updates this database once a day

If you want to manually update this database, you can do it as follows

```bash
sudo updatedb
```

## If you want to find out if a command is installed or where it is installed, for example the "cal" command that displays a simple calender, run the following command

```bash
which <command>
```

## You can use the "history" command to print all the commands that you ran

```bash
history
```

## Help commands

The most simple command is `whatis`. e.g

For some commands like `cd`, it will not work

```bash
whatis cal
```

## I want to do something that involves time; but I don't know exactly which command to use. In that case

```bash
apropos time
```

## You can look at he reference manuels. e.g

```bash
man ls
```

## For some commands like "cd", which is a basic shell command, there won't be a man page

## Make a directory

```bash
mkdir Junk
```

## If you run "touch" for an existing file, it will only update the date it is accessed. It wont affect the content

```bash
touch <filename>
```

## If you want to create a file, run the "touch" command with a file name that doesn't exist

```bash
touch file2
```

## Create multiple files

```bash
touch file3 file4.txt file5
```

## If I want to make a copy of a file from another directory to my current working directory, e.g

`cp <path_of_original_file> <new_file_name>`

```bash
cp ~/.bashrc bashrc
```

## If I want to make a copy of a file in the same directory (say, for a back up of the original file)

```bash
cp bashrc bashrc.bak
```

## Renama or Move a file

### Rename a file

```bash
mv bashrc.bak bashrc
```

if there is already an existing file named bashrc, it will overwrite it

## Removing files

### `rm` command

```bash
rm <filename1> <filename2> ....
```

Remove all files in a directory

```bash
rm *
```

Remove all the files that start with "file"

```bash
rm file*
```

Removing directories whether it is empty or not

```bash
rm -r <directory1> <directory2> ....
```

 Remove a directory named Junk3

```bash
rm -r Junk3
```

`-r` means execute the command recursively, causing to remove the folders, subfolders and files in it

### Removing directories that are only empty

You can't remove directories that are not empty with `rmdir` command

If you run it with global "*" character it will only remove the empty directories and leave the others

```bash
rmdir <directory1> <directory2> ....
```
