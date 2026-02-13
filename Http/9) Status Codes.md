# HTTP Status Codes
Docs: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status

HTTP status codes describe **how the server responded** to an HTTP request.  
They are grouped by the **first digit**.

---

## 1xx — Informational
Server received the request and is still processing.

| Code | Meaning |
|------|---------|
| **100 Continue** | Server expects more data. |
| **101 Switching Protocols** | Switching to another protocol (e.g., WebSocket). |
| **103 Early Hints** | Client can start preloading resources. |

---

## 2xx — Success
The request was successfully received and processed.

| Code | Meaning |
|------|---------|
| **200 OK** | Request successful, returning data. |
| **201 Created** | Resource successfully created. |
| **202 Accepted** | Request received but not yet processed. |
| **204 No Content** | Successful request, no response body. |

---

## 3xx — Redirection
The client must take additional action (e.g., follow a redirect).

| Code | Meaning |
|------|---------|
| **301 Moved Permanently** | Resource permanently moved to new URL. |
| **302 Found** | Temporary redirect. |
| **304 Not Modified** | Cached version should be used. |
| **307 Temporary Redirect** | Redirect without changing HTTP method. |

---

## 4xx — Client Errors
The request is invalid or unauthorized.

| Code | Meaning |
|------|---------|
| **400 Bad Request** | Invalid or malformed request. |
| **401 Unauthorized** | Authentication required or incorrect. |
| **403 Forbidden** | Request understood but not allowed. |
| **404 Not Found** | Resource does not exist. |

---

## 5xx — Server Errors
The server failed to process a valid request.

| Code | Meaning |
|------|---------|
| **500 Internal Server Error** | Generic server error. |
| **502 Bad Gateway** | Invalid response from upstream server. |
| **503 Service Unavailable** | Server overloaded or down for maintenance. |
| **504 Gateway Timeout** | Upstream server did not respond in time. |

## Handling HTTP Status Codes in Frontend

```bash
const res = await fetch("/api/users/123");

if (res.ok) {
    console.log("Success:", res.status);
}
```

