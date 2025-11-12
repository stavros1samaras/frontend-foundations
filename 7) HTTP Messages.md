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

---

## HTTP Request Message
```
Start Line    |<Method> <Request-URI> <HTTP-Version>  |  EX    GET /index.html HTTP/1.1
Headers Block |<Header-Name>: <Header-Value>          |  AM    Host: www.example.com
              |            ...                        |  PL    User-Agent: Mozilla/5.0
              |<Header-Name>: <Header-Value>          |  E     
Entity Body   |<Optional-Body>                        |  ->    User-Agent: Mozilla/5.0
```

Accept: text/html


- **Start Line** – specifies:
  - The **HTTP method** (GET, POST, etc.)  
  - The **target resource** (URL/path)  
  - The **HTTP version**  
- **Headers Block** – additional metadata such as:
  - Content type (`Content-Type`)  
  - Authentication (`Authorization`)  
  - Caching instructions, cookies, etc.  
- **Entity Body (optional)** – data sent to the server, e.g., login credentials, file uploads.


---

## HTTP Response Message
- **Start Line** – contains:
  - **HTTP version**  
  - **Status code** (3-digit number indicating request result, e.g., 200, 404)  
  - **Reason phrase** (human-readable description of the status code)  
- **Headers Block** – metadata about the response, e.g., content type, caching, server info.  
- **Entity Body (optional)** – the content returned by the server, e.g., HTML page, JSON data.




---

## Key Notes
- Not all headers are used by both requests and responses.  
- In command-line testing with `curl`:
  - `>` indicates parts of the **HTTP request**  
  - `<` indicates parts of the **HTTP response**  

---

## Summary
- HTTP messages are structured to ensure **clear communication** between clients and servers.  
- Requests ask for actions, responses provide the results.  
- Understanding headers, status codes, and message bodies is essential for debugging and developing web applications.
