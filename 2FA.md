# Testing 2 Factor Authentication
1. Response/Status Code Manipulation.
2. Brute force otp.
3. Otp doesn't expire after usage.
4. Request 2 tokens from account A and V. Use the A's token in V's account.
5. Try to go directly to the dashboard URL without solving the 2FA. If not success then try adding the referral header to the 2FA page url while going to dashboard.
6. Search the 2FA code in response/js files using burp search.
7. CSRF/Clickjacking to disable 2FA.
8. Enabling 2FA doesn't expire previous sessions.
9. Login using OAuth to bypass 2FA [Mostly N/A].
10. No 2FA required for disabling 2FA.
11. Password can be reset via forgot password without 2FA.
12. Enter 0's in the code. For example, if it's a 6 digit code use 000000 as 2FA.
13. Request Manipulation: Try sending null response for JSON, change the "otprequired" parameter from true to false[Application may allow to create an account using that phone number without any otp validation], remove the 2fa code, remove both code and parameter, in JSON give email as an array, [my medium writeup](https://infosecwriteups.com/email-and-phone-number-verification-bypass-worth-85dbaa794b28).
14. [OpenID Misconfiguration](https://youst.in/posts/bypassing-2fa-using-openid-misconfiguration/)
15. Code doesn't expire after 4-5 hours.
16. Backup code facility: After successful login, generate the backup code generate request from your browser. You may able to get the backup codes.
Generate the following request after login:
```
POST /api/enable-2fa HTTP/1.1
Host: target.com
........

{"action":"backup_codes","email":"victim@gmail.com"}
```
See [here](http://c0d3g33k.blogspot.com/2018/02/how-i-bypassed-2-factor-authentication.html).

17. Check whether 2FA page is diclosing some sensitive info that you didn't know previously (like Ph. No.).
18. Permanent Dos on Unregistered Users:
```
        I. Create an account with victim@gmail.com (If there is no email verification). Now enable 2FA in the account. So now victim can't create an account as it'll ask for 2FA code.
        II. Can't enable 2fa without email verification? Register with your email and verify it ---> Enable 2fa ---> Change your email to victim.
```
19. Try to perform different authenticated requests(profile details change, api create/delete etc) without solving the 2fa.
20. OTP Bypass in JSON:
```
{
        "code":[
                "1000",
                "1001",
                "1002",
                "1003",
                "1004",
                ...
                "9999"
                ]
}
```
21. Backup code abuse using the above methods.

Reference:
- https://youtu.be/X2WfhBYQ2fY
- https://twitter.com/tuhin1729_/status/1414813055054086152
