- We can guess that there is an admin user and try to brute force his password with Burpsuite on this page http://localhost:8888/index.php?page=signin
- Using Burpsuite we can intercept the request and insert a payload (Our wordlist), we will ask Burp (Intruder) to insert the password in the request and send them all until we find a positive response.
- In fact we fond that the password of the user admin is "shadow"

Flag: b3a6e43ddf8b4bbb4125e5e7d23040433827759d4de1c04ea63907479a80a6b2