# Linux Exercises
Remember to use `<command> --help` or `man <command>` to get more info on a command.
All exercises should be solved using only a single command.

First, create a personal folder to work in:
`mkdir /home/yourname && cd /home/yourname`

1. Open nano, and copy-paste the content of `poem.md` into it it. Save the file as `poem.md`
2. Display a file
	- Display the whole `poem.md` file
	- Display the first 20 lines of `poem.md`
	- Display the first 20 characters of `poem.md`
	- Display the last 20 lines of `poem.md`
	- Display the last 20 characters of `poem.md`
	- Display lines 10 to 20 of `poem.md` (tip: use the pipe symbol)
3. Writing to a file
	- Print "Hello world." to the screen
	- Write "Hello world." to `hello.txt`
	- Append " How are you?" to `hello.txt` as well
	- Write lines 10 to 20 of `poem.md` to a file called `short_poem.md`
4. Find
	- Find all `.so` files inside of the `/usr/lib` directory
5. Filter 
	- In `poem.md`, find all lines containing the word: "the" (tip: combine the command you used in 2. with pipe (`|`) and another command)
	- In `poem.md`, find all lines NOT containing the word: "the"
6. Size & Archives
	- Look at the total disk size of `/home/yourname`
	- Put the folder into an archive named `yourname.tar`
	- What is the size of the tarball?
7. Find which of your current running processes is consuming the most CPU?
  - If you are running inside of Docker, there will be very few programs!
  - What is the command to stop that process? **Just think of the command, don't actually execute it**