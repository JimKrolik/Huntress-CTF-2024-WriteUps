Challenge:

![Challenge](images/1.challenge.PNG)

We are tasked with pulling up DNS records off of the ctf.games domain.

By running the dig command with the flag for txt records ```dig -t txt ctf.games```, we see an encoded block of text.

![DNS](images/2.dig.PNG)

After messing around with a few recipes in [Cyber Chef](https://gchq.github.io/CyberChef), I found that converting from octal reveals the flag.

![Flag](images/3.flag.PNG)

Flag: ```flag{14e072f705d45882401d141c562fdc0b}```