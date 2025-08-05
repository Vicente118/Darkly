- We can see with the inspect tool in the browser that there is a cookie:

i_am_admin : 68934a3e9455fa72420237eb05902327

- The cookie is md5 encoded let's decode this: 68934a3e9455fa72420237eb05902327 -> false
- Let's change the cookie from false to true.
- true in md5 is -> b326b5062b2f0e69046810717534cb09
- Once we have change the cookie we get admin right (In theory) and we get the flag.