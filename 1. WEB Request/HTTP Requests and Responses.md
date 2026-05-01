HTTP communication consists of HTTP request and HTTP response.
HTTP request is sent by a client (curl/browser) to server containing all information that we need from server (URL, path, parameters etc), server then process the request and send a HTTP response back to client containing the data/resource we requested

## HTTP Request
A get http request is shown in the screenshot

![[raw_request.png]]

first line contains the method, path, HTTP version separated by spaces. Method defined the type of action we are requesting the server to perform in this get a resource
path represents the path to the resource on the server and HTTP version

**NOTE:** HTTP version 1.X sends requests as clear-text, and uses a new-line character to separate different fields and different requests. HTTP version 2.X, on the other hand, sends requests as binary data in a dictionary form.

Next lines contains headers and their corresponding values each termination with a new line, which will validate the request. Finally it can end with request body and data

## HTTP Response
Following image an example HTTP response from server
![[raw_response.png]]
first line contains the version and http response code. Response code is used to determine the request status for example was successful or not found etc

Next lines contain headers and their values. Finally it may end with body or data. Body can be html file or data in JSON format or any other resource like image etc


