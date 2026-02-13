# HTTP Messages

## Overview
- HTTP messages are the **core of data exchange** in HTTP.  
- Two main types:
  - **Request messages** – sent by the client to ask the server to perform an action.  
  - **Response messages** – sent by the server as a reply to a client request.  
- Both types consist of:
  1. **Start line**  
  2. **Headers block**  
  3. **Optional body (entity body)**

## HTTP Request Message
```
STRUCTURE                                                    EXAMPLE
__________________________________________________________  ______________________________
|  Start Line    |<Method> <Request-URI> <HTTP-Version>  |  |  GET /index.html HTTP/1.1  |
|  Headers Block |<Header-Name>: <Header-Value>          |  |  Host: www.example.com     |
|                |            ...                        |  |  User-Agent: Mozilla/5.0   |
|                |<Header-Name>: <Header-Value>          |  |                            |
|  Entity Body   |<Optional-Body>                        |  |  Accept: text/html         |
——————————————————————————————————————————————————————————  ——————————————————————————————
```

Accept: text/html


- **Start Line** – specifies:
  - The `<Method>` (GET, POST, etc.)  
  - The `<Request-URI>` (URL/path)  
  - The `<HTTP-Version>` 
- **Headers Block** – additional metadata (some of them are optional) such as:
  
| **Header-Name** | **Header-Value** |
|------------------|------------------|
| Content-Type | application/json |
| Accept | application/json |
| ... | ... |

- **Entity Body (optional)** – data sent to the server, e.g., login credentials, file uploads.

## HTTP Response Message

```
STRUCTURE                                                    EXAMPLE
___________________________________________________________________  ______________________________
|    Start Line  | <HTTP-Version> |<Status-Code> <Reason-Phrase>  |  |  GET /index.html HTTP/1.1  |
|  Headers Block |<Header-Name>: <Header-Value>                   |  |  Host: www.example.com     |
|                |            ...                                 |  |  User-Agent: Mozilla/5.0   |
|                |<Header-Name>: <Header-Value>                   |  |                            |
|  Entity Body   |<Optional-Body>                                 |  |  Accept: text/html         |
———————————————————————————————————————————————————————————————————  ——————————————————————————————
```

- **Start Line** – contains:
  - **HTTP version**  
  - **Status code** (3-digit number indicating request result, e.g., 200, 404)  
  - **Reason phrase** (human-readable description of the status code)  
- **Headers Block** – metadata about the response, e.g., content type, caching, server info.

| **Header-Name** | **Header-Value** |
|------------------|------------------|
| Content-Type | application/json |
| Accept | application/json |
| ... | ... |

- **Entity Body (optional)** – the content returned by the server, e.g., HTML page, JSON data.

## Key Notes
- Not all headers are used by both requests and responses.

## Example

Send a GET request
```bash
$ curl -v example.com
```
Output:
```bash

* Host example.com:80 was resolved.
* IPv6: (none)
* IPv4: 12.34.56.78, 87.65.43.21, 98.76.54.32, 23.45.67.89, 56.78.90.12, 34.56.78.90
*   Trying 12.34.56.78:80...
* Established connection to example.com (23.215.0.136 port 80) from 172.20.20.104 port 62094
* using HTTP/1.x
> GET / HTTP/1.1
> Host: example.com
> User-Agent: curl/8.16.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Content-Type: text/html
< ETag: "bc2473a18e003bdb249eba5ce893033f:1760028122.592274"
< Last-Modified: Thu, 09 Oct 2025 16:42:02 GMT
< Cache-Control: max-age=86000
< Date: Thu, 13 Nov 2025 14:38:04 GMT
< Content-Length: 513
< Connection: keep-alive
<
<!doctype html><html lang="en"><head><title>Example Domain</title><meta name="viewport" content="width=device-width, initial-scale=1"><style>body{background:#eee;width:60vw;margin:15vh auto;font-family:system-ui,sans-serif}h1{font-size:1.5em}div{opacity:0.8}a:link,a:visited{color:#348}</style><body><div><h1>Example Domain</h1><p>This domain is for use in documentation examples without needing permission. Avoid use in operations.<p><a href="https://iana.org/domains/example">Learn more</a></div></body></html>
* Connection #0 to host example.com:80 left intact


## Summary
- HTTP messages are structured to ensure **clear communication** between clients and servers.  
- Requests ask for actions, responses provide the results.  
- Understanding headers, status codes, and message bodies is essential for debugging and developing web applications.
