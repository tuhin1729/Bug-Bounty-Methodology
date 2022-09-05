# Denial of Service
1. Application has a functionality where we can invite users via email &rarr; Try sending email invite to an invalid email address like ```anyemail$1@anything.com``` or ```thisdoesntexists@tuhin1729.com```. If success then find out which Email Service Provider (by looking into email header or use mxtoolbox.com) the application is using. Check the hard bounce limit of that email provider (For example, hard bounce limit of AWS SES, Hubspot is arround 5%). If the bounce rate reached then the service provider will block company's service. As a result, they'll not be able to send emails anymore.
2. Long Password Dos: Use a [very long string](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/payloads/password.txt) in the password field while creating account/updating password. If you observe a long delay (generally more than 10,000 milliseconds) in receiving response/get a 5XX status code then the application seems to be vulnerable. 
3. Long String Dos: Look for any input field (like name, address etc) whose value is stored in the database. Enter a [very long string](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/payloads/password.txt) in those parameters and look for delay/5xx status code. In case, the application has a feature where you can search for others' profile, use the long string in attacker's account and try searching for attacker's account from victim's account. Look for delay/5xx status code.
4. If application has a feature where you can upload an image, try uploading [lottapixel.jpg](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/payloads/lottapixel.jpg) and wait for a 5xx. In case, GIF files are allowed, try [uber.gif](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/payloads/uber.gif). If SVG file uploads are allowed, then try [bllionlaugh.svg](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/payloads/bllionlaugh.svg)
5. For wordpress websites, look for [CVE-2018-6389](https://hackerone.com/reports/752010). 
6. Apapche HTTP Server Byte Range DoS: If the application is using Apache 1.3.x, 2.0.x<2.0.64, 2.2.X<2.2.19 then add this [header](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/payloads/apachedos.txt) to any request.
7. Dos via Web Cache Poisoning: In case, you are able to redirect users by exploiting a web cache poisoning vulnerability, then try redirecting them to an invalid port (for example, example.com:1729). 
8. Try null bytes (%00, %0d%0a, %0d, %0a, %09, %0C, %20) in different input fields.
9. Abusing Referrer cookie.
10. Upload feature? &rarr; Upload a very large file to consume memory. If blocked, try redirection.
11. Missing rate limit on register/contact form &rarr; Memory corruption.
12. Permanent DoS on unregistered users: Check for account lockout. Also try 18th testcase of [Testing 2 Factor Authentication](https://github.com/tuhin1729/Bug-Bounty-Methodology/blob/main/2FA.md)
13. Send a message to victim from attacker &rarr; Delete attacker's account. Now try to open the inbox of victim.
14. If the application is using JSON, try using ```null``` as a value of some input field.

Reference:
- https://medium.com/swlh/top-25-denial-of-service-dos-bug-bounty-reports-4aaeb4e9a052
- https://infosecwriteups.com/kill-em-with-laughter-the-billion-laughs-attack-through-image-uploads-4e9c57ca6434
