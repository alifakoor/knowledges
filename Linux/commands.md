## shell globbing (wildcards)
### *
`echo *` echo all filenames that are in the current directory
`echo at*` all filenames that start with `at`
`echo *at` all filenames that end with `at`
`echo *at*` all filenames that contain `at`
### ?
`echo b?at` match `boat` and `brat`



## less

When running `less`, you’ll see the contents of the file one screenful at a time.
Press the spacebar to go forward in the file and press `b` (lowercase) to skip back one screenful. To quit, press `q`.


## diff
To see the differences between two text files, use diff:
`diff file1 file2`


## file
show the file format
`file [filename]`


## find and locate
It’s frustrating when you know that a certain file is in a directory tree somewhere but you just don’t know where. Run find to find file in dir as follows:
`find dir -name [filename] -print`

Most systems also have a locate command for finding files. Rather than searching for a file in real time, locate searches an index that the system builds periodically. Searching with locate is much faster than find, but if the file you’re looking for is newer than the index, locate won’t find it.


## head and tail
`head /etc/passwd` shows the first 10 lines
`tail /etc/passwd` shows the last 10 lines


## changing password
`passwd`


## changing shell
`chsh`


## dot files
These are files and directories whose names begin with a dot (.).
You can run into problems with globs because `.*` matches `.` and `..` (the current and parent directories). You may wish to use a pattern such as `.[^.]*` or `.??*` to get all dot files except the current and parent directories.


## environment and shell variables
The main difference between environment and shell variables is that the operating system passes all of your shell’s environment variables to programs that the shell runs, whereas shell variables cannot be accessed in the commands that you run.

assign and environment variable
```sh
STUFF=blah
export STUFF
```

`PATH` is a special environment variable that contains the command path (or path for short), a list of system directories that the shell searches when trying to locate a command. For example, when you run `ls`, the shell searches the directories listed in `PATH` for the ls program.

add directory to `PATH`:
`PATH=dir:$PATH`
`PATH=$PATH:dir`


## command line editing
![[Pasted image 20240629110243.png]]



## manual page
`man ls`

`man -k [keyword]` for example `man -k sort`:
This is helpful if you don’t quite know the name of the command that you want.
The output includes the manual page name, the manual section (see below), and a quick description of what the manual page contains.

![[Pasted image 20240630084116.png]]

Some common terms have many matching manual pages across several sections. By default, man displays the first page that it finds. You can select a manual page by section.
`man 5 passwd`



## Command for see usage of directories and files
`du -skh * | sort -h`


## Change permission of all folder in directory
to change permission all folder in directory:  
`sudo chmod -R 777 /directory/`
  
permission:  
[u(user)g(group)o(other)a(all)]  
0 – no permission  
1 – execute  
2 – write  
3 – write and execute  
4 – read  
5 – read and execute  
6 – read and write  
7 – read, write, and execute


## Check folder and subfolder size
`du -ah . | sort -rh | head -n 50`


## Install .deb files on ubuntu
`sudo dpkg -i [file_name].deb`


## Search in file's content
command for search in all file's content in a directory
`grep -r [pattern] [directory]`


## Print last 10 lines of file
we can use `tail` command for print last 10 lines of file
e.g:
`tail [file_name]`


