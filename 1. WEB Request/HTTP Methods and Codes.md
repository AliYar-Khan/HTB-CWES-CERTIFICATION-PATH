HTTP supports multiple methods for accessing a resource. In the HTTP protocol, several request methods allow the browser to send information, forms, or files to the server. These methods are used, among other things, to tell the server how to process the request we send and how to reply.

## Request Methods
The following are some of the commonly used methods:

|**Method**|**Description**|
|---|---|
|`GET`|Requests a specific resource. Additional data can be passed to the server via query strings in the URL (e.g. `?param=value`).|
|`POST`|Sends data to the server. It can handle multiple types of input, such as text, PDFs, and other forms of binary data. This data is appended in the request body present after the headers. The POST method is commonly used when sending information (e.g. forms/logins) or uploading data to a website, such as images or documents.|
|`HEAD`|Requests the headers that would be returned if a GET request was made to the server. It doesn't return the request body and is usually made to check the response length before downloading resources.|
|`PUT`|Creates new resources on the server. Allowing this method without proper controls can lead to uploading malicious resources.|
|`DELETE`|Deletes an existing resource on the webserver. If not properly secured, can lead to Denial of Service (DoS) by deleting critical files on the web server.|
|`OPTIONS`|Returns information about the server, such as the methods accepted by it.|
|`PATCH`|Applies partial modifications to the resource at the specified location.|
The list only highlights a few of the most commonly used HTTP methods. The availability of a particular method depends on the server as well as the application configuration

## Status codes
Status codes provide the information about the status of the request to the client. An HTTP server can send five classes of status code

|**Class**|**Description**|
|---|---|
|`1xx`|Provides information and does not affect the processing of the request.|
|`2xx`|Returned when a request succeeds.|
|`3xx`|Returned when the server redirects the client.|
|`4xx`|Signifies improper requests `from the client`. For example, requesting a resource that doesn't exist or requesting a bad format.|
|`5xx`|Returned when there is some problem `with the HTTP server` itself.|

 Commonly used status codes are:

| **Code**                    | **Description**                                                                                                                                           |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `200 OK`                    | Returned on a successful request, and the response body usually contains the requested resource.                                                          |
| `302 Found`                 | Redirects the client to another URL. For example, redirecting the user to their dashboard after a successful login.                                       |
| `400 Bad Request`           | Returned on encountering malformed requests such as requests with missing line terminators.                                                               |
| `403 Forbidden`             | Signifies that the client doesn't have appropriate access to the resource. It can also be returned when the server detects malicious input from the user. |
| `404 Not Found`             | Returned when the client requests a resource that doesn't exist on the server.                                                                            |
| `500 Internal Server Error` | Returned when the server cannot process the request.                                                                                                      |
## GET
Whenever we visit a website, browser defaults to GET method. It is used to get resource from a server. Once the browser receives the initial page, it can send various type of requests using different methods.

## HTTP Basic Auth
Whenever we try to visit a page and it asks for username and password, it is using HTTP basic auth. Handled by the web server without actually touching the application.

![[http_auth_login.jpg]]

if we try with curl and check the response header it will say `Access Denied`. 

```
aliyark145@htb[/htb]$ curl -i http://<SERVER_IP>:<PORT>/ 
HTTP/1.1 401 Authorization Required 
Date: Mon, 21 Feb 2022 13:11:46 GMT 
Server: Apache/2.4.41 (Ubuntu) 
Cache-Control: no-cache, must-revalidate, max-age=0 
WWW-Authenticate: Basic realm="Access denied" 
Content-Length: 13 
Content-Type: text/html; charset=UTF-8 

Access denied
```

but when provided with username and password

```
aliyark145@htb[/htb]$ curl -u admin:admin http://<SERVER_IP>:<PORT>/ 
<!DOCTYPE html> 
<html lang="en"> 
<head> 
...SNIP...
```

or can directly provide username and password in url as well

```
curl http://admin:admin@<SERVER_IP>:<PORT>/
```

Both will work.

## HTTP Authorization Header
When we hit with curl -I we will get headers including Authorization as shown

```
curl -I https://<Serverip>:<PORT>/
...
Authorization: Basic YWRtaW46YWRtaW4=
...
```
The value `YWRtaW46YWRtaW4=` is base64 encoded admin:admin. This represents the HTTP Basic Auth. If we use modern method like JWT, this will be `Bearer` and token will be longer encrypted one

This header can be passed as command line argument as well as shown below:

```
curl -H "Authorization: Basic YWRtaW46YWRtaW4=" https://<Serverip>:<PORT>/
```

It will work just fine.

## GET Parameters
Get params (short for parameters) are the values sent to server to retrieve data based on user input data. example get request with params

```
aliyark145@htb[/htb]$ curl 'http://<SERVER_IP>:<PORT>/search.php?search=le' -H 'Authorization: Basic YWRtaW46YWRtaW4=' 

Leeds (UK) 
Leicester (UK)
```

The search.php is the resource which will take the request, extract the param, processes it and then return the data (mostly in JSON format).

## POST
As contract to GET request (used for requesting pages or data), POST is used to transfer user file or data to the server.
It sends the data in the body of the request

**Benefits**
- Lack of logging 
	- don't need to log the request as data can be very large in case of files etc
- Less encoding requirements
	-  in case of GET, the URL params are encoded as URL's are meant to be shared. POST body is not encoded except the characters that are used to separate data/params.
- More data can be sent:
	- Depends on browser to browser and server to server, typically and should be below 2000 characters

## Login Forms
In case of GET, we send data in the URL for authentication purposes. With POST request, we can data in the request body as shown in the screenshot


The data in raw form will be as follows:
```
username=admin&password=admin 
```

Using cURL we send the same request as follows:

```
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/

...SNIP...
        <em>Type a city name and hit <strong>Enter</strong></em>
...SNIP...
```

**Tip:** Many login forms would redirect us to a different page once authenticated (e.g. /dashboard.php). If we want to follow the redirection with cURL, we can use the `-L` flag.

## Authenticated Cookies
Once we logged in using the credentials, we should receive a Set-Cookie header in response which will make our session persistent. In this way we don't have to login again to see the page. 

```
aliyark145@htb[/htb]$ curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/ -i 
HTTP/1.1 200 OK 
Date: Server: Apache/2.4.41 (Ubuntu) 
Set-Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1; path=/ 
...SNIP... 
	<em>Type a city name and hit <strong>Enter</strong></em> 
...SNIP...

```

We can use the returned cookie to interact with the website without needing to provide credentials again as follows:

```
aliyark145@htb[/htb]$ curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/ 

...SNIP... 
	<em>Type a city name and hit <strong>Enter</strong></em> 
...SNIP...
```

It can specified as header as well

```
curl -H 'Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/

```

Cookies can be seen in browser Local Storage of Applications Tab. There we can set and remove cookies. Valid cookie are enough to by pass authentication and this makes it an essential part of some web attacks, like Cross-Site Scripting.

## JSON Data

JSON stands for JavaScript Object Notation
It is format of data to send and receive data between client and server. In case of this, `Content-Type` header will be set to `application/json` 

Using cURL we can send a request with JSON data and receive data as follows:

```
aliyark145@htb[/htb]$ curl -X POST -d '{"search":"london"}' -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php 

["London (UK)"]
```

-d represents data being sent
-b for cookie
-H for headers

["London (UK)"] is the result received in JSON format