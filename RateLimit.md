# Bypassing Rate Limit Protection
1. Ip Rotator - If developer implemented rate limit in such a way that the application blocks the ip address of attacker after few requests, then you may try using IP Rotator extension to change your IP in each requests.
2. Add the following headers in the request:
```
X-Originating-IP: 127.0.0.1
X-Forwarded-For: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1
X-Client-IP: 127.0.0.1
X-Host: 127.0.0.1
X-Forwared-Host: 127.0.0.1
X-Forwarded-For: 127.0.0.1
```
Instead of 127.0.0.1, try using 127.0.0.2, 127.0.0.3,...  
Even you can try using double X-Forwared-For header:
```
X-Forwarded-For:
X-Forwarded-For: 127.0.0.1
```
3. Try changing user-agent, cookies.
4. Append null bytes (%00, %0d%0a, %0d, %0a, %09, %0C, %20) to the original endpoint (Ex: ```POST /forgot-password%20 HTTP/1.1```). 
Also try adding the bytes after the value of parameter (like ```email=tuhin@gmail.com%20```)
5. Race condition. Read [this](https://thezerohack.com/how-i-might-have-hacked-any-microsoft-account) as a reference.
6. Add any random parameter in the request.
```
POST /forgot-password?fake=1 HTTP/1.1
Host: target.com
...

email=victim@gmail.com&alsofake=2
```
7. Change the request body (Form to JSON, XML or vice-versa).
8. Change request methods (POST to PUT or GET).
9. If developer implemented captcha based protection then try [Captcha Bypass Techniques](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/Captcha.md).
10. Gmail + and . trick.
11. Change api version (Ex: api/v2/1729/confirm-email to api/v1/1729/confirm-email).
