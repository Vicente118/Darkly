- We have a page where we can post some feedback. It's a great entry for stored XSS. If we can store javascript code into the Html page, each time a user will load this page, the javascript will be executed on the client side. It can for exemple lead to cookie stealing and session hijacking.

- Here is a xss payload that works: <svg/onload=alert('XSS')>
- <svg> is a html balise for Scalable Vector Graphics and can be used to integrate code.
- onload is a event handler that is triggered when the element is loaded into the DOM
- alert shows a pop up, so if we have this pop up, that means that we successfully injected javascript code in client side.