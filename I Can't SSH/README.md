Challenge:

![Alt text](images/1.dChallenge.PNG)

We are given an id_rsa file to work with.

![Alt text](images/2.id_rsa.PNG)

Attempting to connect with it, we receive a load key error which is indicative of a bad format.

![Alt text](images/3.ssh_loadkey_error.PNG)

Standard format for an id_rsa key has a trailing carriage return while this file does not.

![Alt text](images/4.updated_idrsa.PNG)

A carriage return was appended and I re-attempted to SSH in successfully.

Flag:  ```flag{ee1f28722ec1ce1542aa1b486dbb1361}```

![Alt text](images/5.flag.PNG)
