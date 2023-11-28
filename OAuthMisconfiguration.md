# OAuth Misconfiguration

1. Open Redirection to OAuth token stealing: changing redirect_uri to bing.com; use IDN Homograph; other bypasses.
2. Change Referral header to bing.com while requesting OAuth.
```
GET /oauth/token/google HTTP/1.1
Host: target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
...
Referer: https://evil.com
```
3. Pre Account Takeover: Create an account with victim@gmail.com with normal functionality. Create account with victim@gmail.com using OAuth functionality. Now try to login using previous credentials.
4. OAuth Token Re-use.
5. Missing or broken state parameter ([CSRF Bypass](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/CSRF.md))
6. Lack of origin check ([Lack_Of_Origin_Check.html](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/payloads/Lack_Of_Origin_Check.html))
7. Open Redirection on another endpoint ---> Redirect to that endpoint via redirect_uri
8. Look for additional parameters in the requests. For example, if there is an email parameter after signin (i.e. code=OAUTH_TOKEN&state=ANTI.CSRF.TOKEN&email=attacker@gmail.com) then try to change the email parameter to victim's email.
9. Try to remove email from the scope and add victim's email manually.
10. Only company's email is allowed? Replace `hd=company.com` to `hd=gmail.com`
11. Check for client_secret parameter in burp search/github dorking.
12. Go to the browser history and check if the token is present in the history.
13. Facebook OAuth Misconfiguration: https://salt.security/blog/oh-auth-abusing-oauth-to-take-over-millions-of-accounts


#### Reference:
- https://twitter.com/tuhin1729_/status/1417843523177484292
- https://portswigger.net/web-security/oauth
