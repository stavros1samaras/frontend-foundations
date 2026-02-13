# HTTP Methods

## What they are
HTTP methods define **what action the client wants the server to perform** on a resource.

## Main HTTP Methods

| HTTP Method | Purpose                                     | Body Allowed | Typical Use Case                         |
|-------------|----------------------------------------------|--------------|--------------------------------------------|
| GET         | Request data from a resource                 | No           | Fetching pages, fetching API data          |
| POST        | Send data to the server (create resource)    | Yes          | Creating users, forms, uploads             |
| PUT         | Fully replace an existing resource           | Yes          | Full updates (overwrite)                   |
| DELETE      | Delete the specified resource                | Sometimes    | Removing users, items, posts               |
| HEAD        | Same as GET but without response body        | No           | Check metadata (size, last-modified)       |
| PATCH       | Partially update a resource                  | Yes          | Update single fields of a resource         |
| OPTIONS     | Returns allowed methods / CORS info          | No           | Preflight requests, CORS checks            |


### GET
```bash
GET /users/123 HTTP/1.1
Host: api.example.com
```
```bash
curl -v https://api.example.com/users/123
```


### POST
```bash
POST /users HTTP/1.1
Host: api.example.com
Content-Type: application/json
{
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```
```bash
curl -v -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"John Doe","email":"john.doe@example.com"}'
```
### DELETE
```bash
DELETE /users/123 HTTP/1.1
Host: api.example.com
```
```bash
curl -v -X DELETE https://api.example.com/users/123
```


## Important Notes

### 1. HTTP methods appear **only in requests**, never in responses.
- Request example: `GET /users`
- Response example: `200 OK` (status code, not a method)

### 2. A request can contain **only one method**.
- You cannot have GET + POST in the same request.

### 3. POST, PUT, PATCH typically have bodies.
- GET and HEAD usually do not.

### 4. Loading a webpage creates **many HTTP requests**, not just one.
- HTML, CSS, JS, images, fonts, etc.

### 5. Some methods are often blocked
