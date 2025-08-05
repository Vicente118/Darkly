- We found sooner that http://localhost:8888/robots.txt have leaked sensitive information to us. There is in addition of the .hidden directory, the /whatever directory that lead to a file with credentials:
- root::437394baff5aa33daa618be47b75cb49

- With gobuster we can find a interesting page on the webapp: /admin

```bash
> ./gobuster dir -u http://localhost:8888/ -w common.txt --xl 975

/admin                (Status: 301) [Size: 193] [--> http://localhost/admin/]
/audio                (Status: 301) [Size: 193] [--> http://localhost/audio/]
/css                  (Status: 301) [Size: 193] [--> http://localhost/css/]
/errors               (Status: 301) [Size: 193] [--> http://localhost/errors/]
/favicon.ico          (Status: 200) [Size: 1406]
/fonts                (Status: 301) [Size: 193] [--> http://localhost/fonts/]
/images               (Status: 301) [Size: 193] [--> http://localhost/images/]
/includes             (Status: 301) [Size: 193] [--> http://localhost/includes/]
/index.php            (Status: 200) [Size: 6892]
/js                   (Status: 301) [Size: 193] [--> http://localhost/js/]
/robots.txt           (Status: 200) [Size: 53]
/whatever             (Status: 301) [Size: 193] [--> http://localhost/whatever/]
```

- We can then see that the credentials found can be used to connect ourselves to the /admin page.