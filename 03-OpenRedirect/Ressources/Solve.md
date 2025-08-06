- We see that there is some links to facebook, twitter,... pages.
- When we intercept them with burpsuite, we can see this 

```
    GET /index.php?page=redirect&site=facebook HTTP/1.1
    Host: localhost:8888
    sec-ch-ua: "Chromium";v="135", "Not-A.Brand";v="8"
    sec-ch-ua-mobile: ?0
    sec-ch-ua-platform: "Linux"
    Accept-Language: en-US,en;q=0.9
    Upgrade-Insecure-Requests: 1
    User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
    Sec-Fetch-Site: same-origin
    Sec-Fetch-Mode: navigate
    Sec-Fetch-User: ?1
    Sec-Fetch-Dest: document
    Referer: http://localhost:8888/
    Accept-Encoding: gzip, deflate, br
    Cookie: I_am_admin=68934a3e9455fa72420237eb05902327
    Connection: keep-alive
```

- We could modify the rediction website -> it's an open redirect vulnerability because we have control of the redirection.


How to prevent this type of attack ?
    1. Replace this kind of code:

    ```php
        header("Location: " . $_GET['site']);
    ```

    By 

    ```php
        $sites = [
        'facebook' => 'https://facebook.com/YourPage',
        'twitter' => 'https://twitter.com/YourPage',
        ];

        if (isset($_GET['site']) && array_key_exists($_GET['site'], $sites)) {
            header("Location: " . $sites[$_GET['site']]);
        } else {
            // redirect to a safe fallback
            header("Location: /");
        }
    ```
    
    Allowing only certains websites redirection prevent for this type of vulnerability.


Impact:
    1. Phishing: We could redirect someone to a phishing website.
    2. Stealing credentials or session under certain conditions.