install generally typescript
`npm install -g typescript`

----------

check typescript version
`tsc --version`

-------

compile `.ts` file to `.js` file
`tsc [file_name].ts`

compile in watch mode
`tsc -w [file_name].ts`

------

create `tsconfig.json` file
`tsc --init`

-----

create `package.json` file and create a npm project

`npm init -y`

----

run file with `ts-node` package

1. first install `typescript` , `ts-node`, `nodemon` packages
	`npm install -D typescript`
	`npm install -D ts-node`
	`npm install -D nodemon`
2. run project in normanl way
	`ts-node [file_name].ts`
3. run project in watch mode
	`nodemon --exec "ts-node" [file_name].ts`

----

