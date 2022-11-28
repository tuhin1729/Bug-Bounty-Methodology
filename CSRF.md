# Bypassing CSRF Protection
1. Remove the entire token parameter with value/Remove just the value.
2. Use any other random but same length token.
3. Use any other random (length-1) or (length+1) token.
4. Use attacker's token in victim's session.
5. Change the method from POST to GET and remove the token.
6. If request is made through PUT or DELETE then try POST /profile/update?_method=PUT HTTP/1.1 or 
```
POST /profile/update HTTP/1.1
Host: example.com
...

_method=PUT
```
7. If token is sent through custom header; try to remove the header.
8. Change the Content-Type to application/json, application/x-url-encoded or form-multipart, text/xml, application/xml.
9. If double submit token is there (in cookies and some header) then try CRLF injection.
10. Bypassing referrer check:  
i. If the referrer header is checked but only when it exists in the request then add this piece of code in your csrf poc: ```<meta name="referrer" content="never">```  
ii. Regex Referral bypass:  
```
https://attacker.com?target.com
https://attacker.com;target.com
https://attacker.com/target.com/../targetPATH
https://target.com.attacker.com
https://attackertarget.com
https://target.com@attacker.com
https://attacker.com#target.com
https://attacker.com\.target.com
https://attacker.com/.target.com
```
11. CSRF token stealing via xss/htmli/cors.
12. JSON Based:  
i. Change the Content-Type to text/plain, application/x-www-form-urlencoded, multipart/form-data and check if it accepts.  
ii. Use flash + 307 redirect.
13. Guessable CSRF token.
14. Clickjacking to strong CSRF token bypass.
15. Type Juggling.
16. Set the csrf token to "null" or add null bytes.
17. Check whether csrf token is sent over http or sent to 3rd party. See [here](https://hackerone.com/reports/15412)
18. Generate multiple csrf tokens, observe the static part. Keep it as it is and play with the dynamic part.

Reference:
- https://book.hacktricks.xyz/pentesting-web/csrf-cross-site-request-forgery
- https://twitter.com/tuhin1729_/status/1447400377553350656
