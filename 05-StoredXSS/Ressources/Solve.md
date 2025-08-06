- We have a page where we can post some feedback: http://localhost:8888/index.php?page=feedback. It's a great entry for stored XSS. If we can store javascript code into the Html page, each time a user will load this page, the javascript will be executed on the client side. It can for exemple lead to cookie stealing and session hijacking.

- Here is a xss payload that works: <img onload="alert('HACKED')" />a
- We will use a simple <img > tag that support javascriipt code and will print HACKED with a pop up on the screen.
- The xss indeed worked and gives us the flag.

How to prevent this type of attack ?
    1. HTML encode specific characters like <>&'"
    2. Use sanitizer loke DOMPurify that only allow safe tag ike <b> <i>
    3. Modify HTTP Header (CSP) to increase security: Content-Security-Policy: script-src 'self'; object-src 'none'; base-uri 'none';
    4. Never trust user input a use the Zero Trust principles

Impact: 
    1. Steal of cookies and sessions hijacking
    2. Data stealing
    3. Redirection to a malicious website