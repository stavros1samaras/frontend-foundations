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

## Summary
- HTTP messages are structured to ensure **clear communication** between clients and servers.  
- Requests ask for actions, responses provide the results.  
- Understanding headers, status codes, and message bodies is essential for debugging and developing web applications.
