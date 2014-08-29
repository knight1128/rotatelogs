rotatelogs
==========

apache 2.2.x rotatelogs patch in time

What is it
==========

When time changed from past to future, function of rotatelogs is well working.

But, When time changed from future to past, rotatelogs is not working

This is a example below.

\#] date

2011. 02. 14. (mon) 17:04:31 KST


\#] ./rotatelogs aaa-%y%m%d 86400
1

2

3

on other terminal, I runed 'date 112001002007'.)

changed

^D


\#] ls -al aaa*

-rw-r--r--  1 root root 14 11/20 01:00 aaa-110214

   (I expected rotatelogs would rotate logs, but it is not splitted!!!!)
   


So. I made a patch for this. I know this patch is not pretty. :)

I patched and uploaded rotatlogs.c in http 2.2.13. 


After installing, I tested it.


\#] date


2011. 02. 14. (mon) 17:10:31 KST


\#] ./rotatelogs aaa-%y%m%d 86400

1

2

3

  (on other terminal, I runed 'date 112001002007'.)
  
changed

^D

\#] ls -al aaa*

-rw-r--r--  1 root root       8 11/20 01:00 aaa-071119

-rw-r--r--  1 root root       6  2/14  2011 aaa-110214

  (This was what I wanted.)
  

Sometimes CMOS of servers do not work well, Time information could be moved to past or future. 

