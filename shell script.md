in if condition:

`-z` : checks if a string is empty or not
`-d` : checks if a directory exists or not
`-f` : checks if a file exists in current directory or not

example:

```sh
#!/bin/bash
if [ ! -z ${DB_BACKUP_PATH} ]; then
	cd ${DB_BACKUP_PATH}
	if [ ! -z ${DB_DELETE_DATE} ] && [ -d ${DB_DELETE_DATE} ]; then
		rm -rf ${DB_DELETE_DATE}
	fi
	echo "${DB_DELETE_DATE} was deleted"
fi
```

```sh
#!/bin/bash
FILE="/path/to/your/file"

if [ -f "$FILE" ]; then
	echo "File $FILE exists."
else
    echo "File $FILE does not exist."
fi
```