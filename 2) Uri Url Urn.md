# URIs, URLs, and URNs

## URI (Uniform Resource Identifier)
- Identifies a specific web resource
- Can identify by location, name, or both
- Two types: **URL** and **URN**

## ⭐ URL (Uniform Resource Locator)
- Most common type of URI
- Identifies the **location** of a resource
- Components:
  - **Scheme**: protocol (e.g., HTTP, HTTPS, FTP)
  - **Host**: domain name (example.com) or IP address
  - **Path**: specific resource on the server
  - **Query parameters**: optional, for dynamic content
  - **Fragment**: optional, points to a section within a resource
- Examples:
  - `https://www.example.com/path/to/resource`
  - `https://www.example.com/search?q=term`
  - `https://www.example.com/page#section1`

## URN (Uniform Resource Name)
- Identifies a resource **by name only**, no location needed
- No scheme, domain, or path
- Example: `urn:ietf:rfc:2616`
- Useful for moving resources without changing the name
- Still experimental, not widely used


# HTTP Deep Dive - URIs, URLs, and URNs

| Type | Purpose | Components | Example | Notes |
|------|---------|------------|---------|-------|
| **URI** | Identifies a web resource | Can be by location, name, or both | N/A | Umbrella term for URLs and URNs |
| **URL** | Identifies the **location** of a resource | Scheme (HTTP/HTTPS), Host (domain/IP), Path, Query, Fragment | `https://www.example.com/path/to/resource` | Most common type of URI |
| **URN** | Identifies a resource **by name only** | Name only, no scheme, host, or path | `urn:ietf:rfc:2616` | Useful for moving resources without changing name; not widely used |
