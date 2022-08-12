---
layout: page
title: The Unix Shell
subtitle: Command Subsitution
minutes: 15
---
> ## Learning Objectives {.objectives}
>
> * Understand the need for flexibility regarding arguments
> * Generate the values of the arguments on the fly using command substitution
> * Understand the difference between pipes/redirection, and the command substitution operator

## Introduction


### xargs

This does not work
$ find acsoe | ls
acsoe		presentations
$ 

Find pipes a list of files to ls.
ls ignores input and just does a normal listing of the current working directory.
Lots of commands expect a list of arguments, not standard input. Is there anything to help?


The "xargs" command runs the same command on all files specified in the input.
Usually used with "find" output, e.g.:
find . -name '*.nc' | xargs chmod u=rwx
Changes permissions on all .nc files.

by default splits the file list into batches:
chmod 644 file1 file2 … file100
chmod 644 file101 file102 … 
use "-n 1" if the command can only process one file at a time:
find . -name '*.tar' | xargs -n 1 tar -tvf
displays contents of all 'tar' files found


Use find piped to xargs to do something (wc, ls –l , head -1, etc)

### Other ways to move data around

There are a lot of tools to help you move data from one machine to another. Common ones are:
FTP
SFTP
Rsync
Wget
Curl

wget makes it easy to grab resources from a http or ftp address.
(curl is a similar tool)

Have a look at the following address in a web browser. Note it's not a http address.
 ftp://sparc-ftp1.ceda.ac.uk/sparc/hres/1_second/text/2011/03020/
 Get one of the files with wget from the command line.






### I'm a terminal based editor get me out of here!

Some editors use the terminal window.
The default editor used by some commands means you need to know how to get out of them sometimes. 
If you are not used to them you can get stuck.
Emacs – get out with ^X ^C   (maybe need ^G^X^C)
Vi – get out with escape, then :q! then enter. 


