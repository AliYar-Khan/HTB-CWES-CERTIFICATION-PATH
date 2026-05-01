**HTTP** stands for Hyper Text Transfer Protocol
**Hyper Text** text that contains link and reference to other resources
**HTTP** communication consists of a client and server. Client request a resource by visiting a URL, server returns the resource. Default port is 80 for this communication

**URL** Uniform Resource Locator
resources are accessed over network with URL which specifies many more specifications other than just visit a website by URL

example

https://admin:password@inlanefreight.com:80/dashboard.php?login=true#status

**Scheme** http:// or https:// 
this defines the protocol used by client to access the website. 's' at the end is for secure which uses encryption for the traffic being sent

**User Info** admin:password
this specify the user credentials that can be used to authenticate to host followed by a "@"

**host / domain** inlanefreight.com it specifies the location of the resource. It can be a hostname or IP address

**Port** 80. it is a virtual endpoint managed by OS for managing traffic between different applications and services. 80 is default for http and 443 for https

**Path** /dashboard.php points to the resource being accessed. it can be any file, image etc for example index.html

**Query String** ?login=true information passed to web server or application as a key value pair

**Fragment** #status an internal page reference, sometimes called a name anchor.

Not all components are required to access a resource. The main mandatory fields are the scheme and the host, without which the request would have no resource to request.

**HTTP Flow** 
![[HTTP_Flow.png]]

The above image shows the working of HTTP. User enter the address/hostname in address bar and it ask DNS about the location of the server where the site is hosted. DNS responds with IP address of the server and the browser/client then hit a GET request to the IP at default port 80. Server receives the request, process the request and by default, servers are configured to return an index file when a request for `/` is received.

In this case, index.html is returned with a response code of 200 which means request was successful.

# **cURL** 
**cURL** stands for client URL
command line tool and library that primarily supports HTTP along with many other protocols

we can send request to any web server as follows
```
curl inlanefreight.com
```

it will not render the html, CSS and JavaScript like browser but will show it in raw format.

it can also be used to download a page as follows:
```
curl -O inlanefreight.com/index.html 
% Total % Received % Xferd Average Speed Time Time Time Current Dload Upload Total Spent Left Speed 100 464 0 464 0 0 17858 0 --:--:-- --:--:-- --:--:-- 18069
```
Output will be saved in current folder as index.html

cURL has many options which can be seen by running following command:
```
curl -h
```
