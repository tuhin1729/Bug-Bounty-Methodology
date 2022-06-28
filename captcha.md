# Captcha Bypass

1. Response manipulation.
2. Use previously used token.
3. Use any token with same length(+1/-1).
4. Remove the param value or remove the entire parameter.
5. Change method from POST to GET(or PUT) and remove the captcha.
6. Change body to JSON or vice-versa.
7. Try OCR.
8. Check whether the captcha is in the source code. (Ex: 2+2)
9. Check whether the value of the captcha is in the source code.
10. Try to use the same captcha value several times with the different sessionIDs.
11. JSON Body? Combine 6 and 5.
12. Add headers:
```
X-Forwarded-Host: 127.0.0.1
X-Forwarded-For: 127.0.0.1
X-Originating-IP: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1
X-Client-IP: 127.0.0.1
X-Host: 127.0.0.1
```
