- This page is used to recover password only using the e-mail in the http request. http://localhost:8888/index.php?page=recover
- We can intercept the request with Burp in order to modify the mail and get the recovery mail to modify the password. The server just take the mail in account without any verification.

Flag: 1d4855f7337c0c14b6f44946872c4eb33853f40b2d54393fbe94f49f1e19bbb0