Challenge:

![Challenge](images/1.challenge.PNG)

We are presented with a web page to attempt to find a flag.

Logging into the web page with the default credentials, we see a tab for the API Docs.

![Login](images/2.login.PNG)

Looking around, we find the admin authorization is looking for a base64 encoded cookie.

![API documentation - base64 cookie](images/3.api.base64cookie.PNG)

Additionally, if we look at the authorization settings, we can see the laytout for the cookie is 'username.isAdmin.expirationTime'.

![API Cookie Structure](images/3a.cookiestructure.PNG)

Opening BurpSuite and logging in with the intercept on, we see a cookie get generated.

![BurpSuite Login](images/4.loginBurp.PNG)

We can decode the cookie to find the username, the 'isAdmin' flag, and the session expiration value.

![Decoded session cookie](images/5.base64decode.PNG)

I then updated the value to set 'isAdmin' to a one and re-encoded the cookie.

![Re-encoded session cookie](images/6.base64encode.PNG)

Changing the auth cookie out and forwarding the request, we now see the admin panel.

![Re-encoded session cookie](images/7.substitutecookie.PNG)

![Admin Dashboard](images/8.adminlogin.PNG)

Additionally, we can now access the Logs tab, which appears to give us visibility into the operating system.

If we examine one of the plants, we can see there is an option to set an alert command.

![Alert Command](images/10.alertcommand.PNG)

This corresponds with one of the API options we have to trigger the send mail.

![API Send Mail](images/11.sendmailapi.PNG)

We can update the send mail command and append ```&& cat flag.txt```

![Updated command](images/12.updatecommand.PNG)

Finally, we will authorize the API and trigger the command, we can see it successfully sent.

![API authorized](images/13.sendmailsuccessful.PNG)

![API executed](images/14.sendmailsuccessful.PNG)

If we go review the log, we will find our flag.

![Flag](images/15.flag.PNG)

Flag: ```flag{c29c4d53fc432f7caeb573a9f6eae6c6}```
