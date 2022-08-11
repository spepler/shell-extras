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

### rsync

copies files over the network (or locally)
where destination files already exist, copies only what is required to update any differences
push / pull files over ssh:
rsync user@host:remote_path local_path	← pull
rsync local_path user@host:remote_path	← push
requires no special configuration (though remember to set up ssh keys)
similar to scp syntax, e.g. remote path is relative to home directory unless starts with /

Useful flags for rsync:
-r (recursive) – go down the directory tree copying stuff.
-c (checksum) – when deciding what files to send, look not only at size and timestamp but if necessary also file contents
--delete  – remove files from destination not present at source end.  (Test with -n first!)
-v (verbose) – list files that are transferred (or deleted)
-n (dry run) – go through the motions but do not actually transfer (or delete) files. Useful with -v.
-a (archive) – copy recursively and try to copy permissions, ownership, etc.

Copy the data in the acsoe directory to an acsoe2 directory with rsync. Use the –v (verbose) option so you can see what is happening.
Run the command again and note what is copied.
Add a new file to acsoe directory, modify another file and delete a third. Run the command a third time. 
Try rsync to the remote machine used in the scp exercise. 

### Pattern matching: globs

Unix shells recognises various wildcards in filenames. We have seen these two:
* matches any number of characters
? matches one character
These filename matching patterns, known as "globs", are replaced with a list of matching filenames before the command is executed.
$ ls
1	3	5	a1	b1	c1	d1
  4	a	b	c	d

$ ls *1
a1 b1	c1	d1

$ ls ??
a1 b1 c1	d1


Here is another glob for you
[…] matches any of the characters listed (or range of characters, e.g. [0-9])

$ ls [a-c]*
a a1 b b1 c c1

And another glob
{fred, barny, wilma} matches any of the comma separated names listed.
For example ls *.{jpg,png} will list all your jpg and png files.


Use glob matching in acsoe/freetex-98/jungfrau
Make a for loop that word counts only files from that date range 


### I'm a terminal based editor get me out of here!

Some editors use the terminal window.
The default editor used by some commands means you need to know how to get out of them sometimes. 
If you are not used to them you can get stuck.
Emacs – get out with ^X ^C   (maybe need ^G^X^C)
Vi – get out with escape, then :q! then enter. 


