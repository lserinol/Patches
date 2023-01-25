# Patches

https://lserinol.blogspot.com/search/label/Patches



## Linux like dmesg in Freebsd
UPDATE:  this patch is applied to Freebsd repository on  10 May 2013

http://svnweb.freebsd.org/base?view=revision&revision=250430

## clamsmtp rbl support patch
clamsmtp is lightweight anti virus smtp proxy. You can put it in front or back of your smtp server. But if you run it in front of your smtp server and relay traffic back to your original smtp server, you cannot use any rbl server.
So, I decided to write a patch which adds this new rbl option to clamsmtpd server. You can download patch from here clamsmtp rbl patch

## ucspi-tcp mysql patch

Finally, I had spare time to finish my ucspi-tcp mysql patch . Putting tcpserver rules in a mysql table has many advantages like centralized access rule lists and easy management. http://qmail.org/

## Sqlite compression
Sqlite database has no built-in compression support. But it has a feature called loadable extension, which let's developers to create any addon feature for sqlite database. I have wrote some documentation about sqlite loadable extension and how to add compress/uncompress ability to sqlite database to compress your data's on the fly.
Here is my article https://sites.google.com/site/lserinol/sqlitecompress

Currently (as sqlite version 3.5.5) has no built-in compression support. But you can easily add this feature by yourself.  sqlite has a feature called Loadable Extensions(https://www.sqlite.org/loadext.html) . Loadable extensions let's you add new features to sqlite.

First off all, you have to enable loadable extension support when you compile sqlite. All you have to do is edit "Makefile.in" file in source directory and  comment out following line:

$ TCC += -DSQLITE_OMIT_LOAD_EXTENSION=1
  
Now you can compile and install your sqlite package.

After that copy sqlite compression extension file(https://github.com/lserinol/Patches/blob/main/mycompress.c) in to sqlite's source directory (eg. sqlite-3.5.5/src).

Then  compile it:

$ gcc -I`pwd` -shared src/compress.c -o mycompress.so -lz 

now you can copy mycompress.so file in to /lib directory.

This extension adds 2 new functions called mycompress and myuncompress. 

now, run sqlite to test it.

$ load extension 

sqlite> .load mycompress.so

$ create a test table 

sqlite> create table test(name varchar(20),surname varchar(20)); 

$ insert into test table some text by compressing text,  you can also compress binary content and insert it into a blob field

sqlite> insert into test values(mycompress('This is a sample text'),mycompress('This is a sample text')); 

this shows nothing because our data is in binary format and compressed

sqlite> select * from test;

following works, it uncompresses the data

sqlite> select myuncompress(name),myuncompress(surname) from test;

Ok, now we have compression support for sqlite database. Also, it's possible to use this functions in your applications which is written in C language.
