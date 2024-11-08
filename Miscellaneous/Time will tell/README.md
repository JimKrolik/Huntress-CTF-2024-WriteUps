Challenge:

![Challenge](images/1.challenge.PNG)

We are given an executable binary and the source code.  Based on the title of the challenge, we need to perform a buffer overflow.

To do:  add debugging steps for overflow and finding offset



Once we have our final payload coded, it's time to attack the server.

I wrote a python script overflow and point the EIP register to 0x080491f5, which contains our shell.  Once we have access, I was able to retrieve the flag.

![flag](images/flag.PNG)

Flag: ```flag{4cd3b4079393e861af489ca063373f98}```