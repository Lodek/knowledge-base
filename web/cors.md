```yaml
date: 2020-10-29
type: notes
tags:
  - web
  - cors
```
- CORS is a standard that introduces new headers to share resources across origins
- An origin is considered equal if they have the same: port, protocol and domain name / ip
- It's my understanding that CORS is a measure at a browser level against some sort of XSS
- How does CORS work? Does the browser even make the request? Does the server receive the request and deny it?
- The request does go through. The browser throws an error if the response does not contain the appropriate headers and hides the response body
- The `Origin` header is added by the browser and the `Access-Control-Allow-Origin` header, added by the server, must container the Origin in order for the browser to allow the content to be displayed

- By default, cookies are not sent on a CORS request, to do so the `withCredentials` value in a `XMLHttpRequest` must be set to true.
- For CORS requests with credentials, the server must responde with a `Access-Control-Allow-Credentials: true` otherwise the browser will reject the response. Furthermore, the response `Access-Control-Allow-Origin` must be equal to the `Origin` header, likewise responses that fail this condition are rejected.
