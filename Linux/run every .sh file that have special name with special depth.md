```sh
find . -maxdepth 2 -type f -name "*runner*.sh" -exec chmod +x {} \; -exec {} \;
```

Here’s what this command does:

- `find . -maxdepth 2`: Searches the current directory and one level of directories beneath it (the directories alongside your current location).
- `-type f`: Looks for files only.
- `-name "*runner*.sh"`: Matches files that include `runner` in their name and end with `.sh`.
- `-exec chmod +x {} \;`: Makes each matched file executable. Replace this with `-exec bash {} \;` if you don't want to change the file permissions permanently.
- `-exec {} \;`: Executes each matched file. This part runs each script found by the `find` command.


for once you want to go through the directory and then run the .sh file:

```sh
find . -maxdepth 2 -type f -name "*runner*.sh" -exec sh -c 'cd "$(dirname "$1")"; ./$(basename "$1")' sh {} \;
```

`-exec sh -c 'cd "$(dirname "$1")"; ./$(basename "$1")' sh {} \;`: This part is new. Here's what it does:

- `sh -c '...' sh {}`: Executes a shell command, passing the found file path (`{}`) as an argument. The `sh` after `-c '...'` is passed to the script as `$0`, which is the name of the running shell script (not used in this case), and `{}` is passed as `$1`, the first argument to the shell script, which represents the path of each found file.
- `cd "$(dirname "$1")"`: Changes the directory to the one containing the found file. `dirname "$1"` extracts the directory part of the file's path.
- `./$(basename "$1")`: Executes the script. `basename "$1"` extracts the filename from the file's path, ensuring that the script runs even if you're not in its directory initially.



