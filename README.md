# Patches

https://lserinol.blogspot.com/search/label/Patches



## Linux like dmesg in Freebsd
UPDATE:  this patch is applied to Freebsd repository on  10 May 2013

http://svnweb.freebsd.org/base?view=revision&revision=250430

## Sqlite compression
Sqlite database has no built-in compression support. But it has a feature called loadable extension, which let's developers to create any addon feature for sqlite database. I have wrote some documentation about sqlite loadable extension and how to add compress/uncompress ability to sqlite database to compress your data's on the fly.
Here is my article https://sites.google.com/site/lserinol/sqlitecompress

## clamsmtp rbl support patch
clamsmtp is lightweight anti virus smtp proxy. You can put it in front or back of your smtp server. But if you run it in front of your smtp server and relay traffic back to your original smtp server, you cannot use any rbl server.
So, I decided to write a patch which adds this new rbl option to clamsmtpd server. You can download patch from here clamsmtp rbl patch

## ucspi-tcp mysql patch

Finally, I had spare time to finish my ucspi-tcp mysql patch . Putting tcpserver rules in a mysql table has many advantages like centralized access rule lists and easy management. http://qmail.org/
