all data is encrypted so that anyone doing MITM attack cannot see the data
## **Overview** 
With http, all the traffic data was transmitted in plain text as shown in the image below:

![[https_clear.png]]

Login credentials can be seen clearly. Anyone on same network can intercept above traffic and see the credentials.

As contrast with HTTPS, the data is encrypted as shown below

![[https_google_enc.png]]

**NOTE:** Data will be encrypted but the destination and other info are still available to be seen 

## HTTPS Flow

User request to server at port 80, but server redirect to 443 with redirect 302.  Next Client sent a "Client hello" packet to share info about itself. Then server replies with a "Server hello" packet with Server key. Then Client sent the client key and secure connection is established with encrypted handshake as shown below

![[HTTPS_Flow.png]]
## cURL for HTTPS
Works with HTTPS without any special configuration. However if we come across a website with invalid SSL certs, then it will throw error
Modern browser also restrict user to visit such websites.
To test without this warning use "-k" flag with curl

```
curl -k https://www.inlanefreight.com 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN"> 
<html><head> 
...SNIP...
```
