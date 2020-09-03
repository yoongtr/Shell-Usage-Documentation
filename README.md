# Shell Usage for Dummies
Documentation based on materials from [MIT The Missing Semester of Your CS Education course](https://missing.csail.mit.edu)

## 1. Shell overview
### What is shell?
* A program that takes commands from the keyboard and gives them to the operating system to perform
### What is bash?
* Bourne Again SHell, a very widely used shell
### Is there any other (cooler) shell?
* I use Z shell (zsh - an extended version of bash) with ohmyzsh configurations from Ming Rui 
* Check [this file] for how to install zsh with Ming Rui's configs

## 2. Basic Shell Usage
* When you open the server, you should see something like this:
 ```shell
 user.name@server-name-ip-11-222-333-444:~$
 ```
  - The part `user.name@server-name-ip-11-222-333-444` indicates the machine you are on, the `~` symbol means that you are in the home directory (aka the path that you will reach when you type `cd`) and `$` means that you are not the root user.
  - Root is the superuser account in Unix and Linux. This user will have access to all command and files, with powers that normal user cannot such as installing software or changing file ownership. If a user is provided root access, the user can use the `sudo` command (short for SuperUser DO). 
  - However, with great power comes great responsibility. You _might easily break something_ while using `sudo`. This will affect a lot of people if you are sharing a server with others. In short, do _NOT_ `sudo` into a shared server if you're not sure!

* Common shell commands can be found under this [Bash Scripting Cheatsheet](https://devhints.io/bash). It works for Z shell too!

* When you are uncertain, `-h` or `--help` flag will print out the short explanation for the command. Try `ls -h` and see.

* Common commands to note for dummies:
  - `pwd`: print your current working directory.
  - `cd`: take you to home directory.
      - `cd` + path: take to the specific path.
      - `cd .`: current directory.
      - `cd ..`: go up one level, i.e. parent directory.
      - `cd -`: go back one level.
  - `ls`: list files inside your current directory.
      - `ls -lah -t`: list all files, including hidden file (`-a` flag), in long format (`-l` flag), in human readable size (`-h` flag), ordered by recency (`t` flag).
      - `ls` + path: list all files inside specific path
  - `cat` + filename: print file, i.e. shows the contents of the file in your terminal. Works for multiple files too.
  - `vim` + filename: open vim editor to view or edit the file. See section 4 for more information on vim editor.
  - `mkdir`: makes a new directory. E.g. `mkdir ~/shell-usage/dummies`
  - `touch`: creates a new file. E.g. `touch filename.txt`
  - `cp`: copy files. E.g. `cp [source directory] [destination directory]`. Works for multiple files too.
  - `mv`: move files or change file name. Same usage as `cp`.
  - `head -n [N] filename`, `tail -n [N] filename`: prints first (head) or last (tail) N lines of a file
  - `rsync`: to sync your local files to the server and vice versa. See [Rsync Cheat Sheet](https://devhints.io/rsync).
  
* How to keep your scripts running on the server even though you lost connection: use `tmux` (see [Tmux Cheat Sheet](https://tmuxcheatsheet.com)) or `screen` ([Screen Cheat Sheet](https://gist.github.com/jctosta/af918e1618682638aa82)).
  
* For each command there are certain flags, for example typing `ls` will give you the list of files inside your current directory. However to see all hidden files, you need to use the `a` flag, i.e. by typing `ls -a`. To see all the details about the flags, use the `man` command. E.g. `man ls`.

## 3. STDIN, STDOUT, and basic piping

## 4. Vim editor

## 5. Some additional stuff
* If you want to have some modifications to your shell commands, e.g. you want a shorter way of typing `ssh -N -f -L [port]:localhost:[port] username@servername` every time you want to tunnel to server, you can edit it in your ~/.zshrc file.
* Start editing with `vim ~/.zshrc`
* At the end of the file you can add:
```shell
function tunnel() {
 ssh -N -f -L localhost:$1\:localhost:$1 $2@$3
}
```
* After this, whenever you want to tunnel just type `tunnel [port] username@servername`
* This works for any command!

## Important things to note while using a shared server
* Do _NOT_ sudo into a server that you have root access. This will affect the whole server and other people who are using it.
* Use a virtual environment or Docker to do your projects and install dependencies.
