- We can see that the server load pages from the server like this:
    - http://localhost:8888/index.php?page=<PAGE>
- We can look for a Path Traversal vulnerability, it occurs when the servers does not filter well the pages a user is asking for.
- We could ask simply for the "signin" page on the server, but can we dig into the /etc directory or /home ?
- http://localhost:8888/index.php?page=../../../../../../../../etc/passwd
- In fact we have access to this file that no one want to expose to users.
- We just have to go back until the root of the filesystem and then we can look for sensitives files.

Flag: b12c4b2cb8094750ae121a676269aa9e2872d07c06e429d25a63196ec1c8c1d0