in the below command:
`0 0 * * * /root/backups/export.sh database collection >> /root/backups/export.txt 2>&1`

- `>> /root/backups/export.txt`: This redirects the standard output (stdout) of the script to a file named `export.txt` in the `/root/backups` directory. The `>>` operator means that the output will be appended to the file, rather than overwriting it each time the script runs.
    
- `2>&1`: This part is about redirecting the standard error (stderr) to the same place as the standard output (stdout). Essentially, it's saying "redirect error messages to the same place we're redirecting the standard output."