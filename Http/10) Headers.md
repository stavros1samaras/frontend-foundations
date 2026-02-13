# HTTP Headers

HTTP headers are **key-value pairs** that provide metadata about a request or response.  
They influence how the server and client handle the connection and data.

---

## Header Categories

1. **General Headers**  
   Apply to both requests and responses.
   - Examples: `Date`, `Connection`

2. **Request Headers**  
   Found in HTTP requests; describe the client and its expectations.
   - Examples: `User-Agent`, `Accept`, `Authorization`

3. **Response Headers**  
   Found in HTTP responses; describe the server or the returned content.
   - Examples: `Server`, `Set-Cookie`, `WWW-Authenticate`

4. **Entity Headers**  
   Describe the body content of requests or responses.
   - Examples: `Content-Length`, `Content-Type`, `Content-Encoding`

5. **Custom Headers**  
   Created by developers as needed, usually prefixed with `X-`.
   - Example: `X-Custom-Header: myvalue`

---

## Example: GET Request with Custom Header

```bash
curl -H "User-Agent: MyApp/1.0" \
     -H "X-Custom-Header: demo" \
     https://httpbin.org/get
```
## Example
```bash
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data', {
      method: 'GET',
      headers: {
        'Authorization': 'Bearer YOUR_TOKEN',
        'Accept': 'application/json',
        'X-Custom-Header': 'MyApp'
      }
    });
```

# Important HTTP Headers for Frontend

HTTP headers are key-value pairs that provide metadata about requests and responses.

| Header Name           | Type       | Description |
|----------------------|------------|-------------|
| `Authorization`      | Request    | Used to send credentials or tokens to authenticate the client. |
| `Accept`             | Request    | Indicates the content types the client can process (e.g., `application/json`). |
| `Content-Type`       | Request/Response | Specifies the media type of the request or response body (e.g., `application/json`). |
| `User-Agent`         | Request    | Identifies the client application/browser making the request. |
| `Cookie`             | Request    | Sends stored cookies to the server. |
| `Set-Cookie`         | Response   | Server sends cookies to be stored by the client. |
| `Cache-Control`      | Request/Response | Controls caching behavior (e.g., `no-cache`, `max-age=3600`). |
| `Accept-Encoding`    | Request    | Indicates which content encodings (gzip, br, deflate) the client supports. |
| `Content-Length`     | Request/Response | Size of the body in bytes. |
| `Connection`         | Request/Response | Controls whether the connection stays open (`keep-alive`) or closes. |
| `X-Requested-With`   | Request    | Commonly used in AJAX requests to indicate XMLHttpRequest. |
| `Origin`             | Request    | Indicates the origin of the request, used in CORS. |
| `Access-Control-Allow-Origin` | Response | Used in CORS to specify which origins are allowed to access the resource. |
| `ETag`               | Response   | Provides a version identifier for caching purposes. |
| `Last-Modified`      | Response   | Indicates the last modification date of the resource. |
| `Location`           | Response   | URL to redirect the client (used in 3xx responses). |
