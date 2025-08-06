- There is a robots.txt file on the server used for the crawlers to index websites on search engine.
- It often reveals some directories or files that can be interesting on the server.
- In fact, we find a directory named .hidden that contains a lot of directories and subdirectories.
- Let's try to find the flag 

```bash
> wget -e robots=off --recursive --no-parent http://localhost:8888/.hidden/
> grep -R "flag"
igeemtxnvexvxezqwntmzjltkt/lmpanswobhwcozdqixbowvbrhw/README:Hey, here is your flag : d5eec3ec36cf80dce44a896f961c1831a05526ec215693c8f2c39543497d4466 
```

- How to prevent:
    1. Don't expose sensitive folders or files in robots.txt
    2. Use authentification or permissions rules on sensitives folders and files

- Impact:
    1. Information disclosure
    2. Access to hidden files/directories