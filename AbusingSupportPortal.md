# Abusing Support Portal
1. Let's say victim's email is victim70@gmail.com. Create an account which looks similar to victim's email (for example, victim71@gmail.com). Use fake mailer and send a request to support@target.com and ask them to change your email id from victim70@gmail.com to victim71@gmail.com
```
From: victim70@gmail.com  
Reply To: victim71@gmail.com  
To: support@target.com  
Subject: Change my E-mail address  
Message:
Hello,
 My real email address is victim71@gmail.com. I mistakenly entered wrong email id (victim70@gmail.com) which I don't use anymore. So I kindly request you to change my email address from victim70@gmail.com to victim71@gmail.com.

Thanks & Regards
Victim
```
P.S: This is not a social engineering attack. Their mail box is not filtering spoofed emails properly. That's why the vulnerability exists. Modify the message as per your choice.

2. Try to create an account using @target.com email address and check if you have any higher priviledge (like viewing others support ticket).
3. Ticket Trick:  
3.1. Generate a support ticket from attacker1@gmail.com. You'll receive an email from support+ticketID@company.com. Try to email something from attacker2@gmail.com to support+ticketID@company.com. If you can see the email at tuhinbose70@gmail.com or if you can see the email at the support portal then it's possibly vulnerable. Now use the email support+ticketID@company.com in different workspaces (like slack, yammer etc) to login to their private workspace.  
3.2. You can create tickets by sending an email to support@target.com + you can view the tickets created by you in their support portal &rarr; most support portals can be integrated with SSO (authenticated users will automatically be logged into the support desk). Sometimes application doesn't enforce e-mail verification (or maybe you can bypass it) which allows to sign up with any e-mail address and read any tickets created by that e-mail address. So in these cases, you can takeover their 3rd party accounts like twitter, GitHub, Instagram etc (if created using the email address support@target.com). For example, in case of twitter, they send their password reset emails from verify@twitter.com. So you can follow the below steps:
```
1. Create an account on target.com with verify@twitter.com (Since they doesn't enforce email verification).
2. Now request for a password reset for the email support@target.com.
3. An email will be sent from verify@twitter.com to support@target.com which contains the code.
4. A ticket will be created which consists of the email body and you can view the ticket on their support portal.
```

Reference:
- https://medium.com/intigriti/how-i-hacked-hundreds-of-companies-through-their-helpdesk-b7680ddc2d4c
- https://medium.com/@alex.birsan/messing-with-the-google-buganizer-system-for-15-600-in-bounties-58f86cc9f9a5
- https://hackerone.com/reports/498964
