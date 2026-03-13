# Frontend Security Vulnerabilities – Notes

These notes describe security vulnerabilities that can be largely **prevented from the frontend side (client/browser)**.

---

## 1. Cross-Site Scripting (XSS – DOM / Client)

### What it is
Occurs when user input is inserted into the DOM without sanitization and malicious JavaScript gets executed.

### Bad Example
```javascript
element.innerHTML = userInput
```

If a user provides:
```html
<script>alert("Hacked")</script>
```
the script will execute in the browser.

### Safer Approach
```javascript
element.textContent = userInput
```

In React avoid using:
```javascript
dangerouslySetInnerHTML
```

### Best Practices
- Use `textContent` instead of `innerHTML`
- Escape user input
- Avoid dynamic HTML injection
- Sanitize user-generated content

---

## 2. Prototype Pollution

### What it is
Prototype pollution allows an attacker to modify the prototype of a JavaScript object and affect the behavior of the entire application.

### Attack Example
```json
{
 "__proto__": { "isAdmin": true }
}
```

If unsafe object merging happens, this property can spread to other objects.

### Best Practices
- Validate user input objects
- Avoid unsafe object merges
- Use safe deep-cloning libraries
- Block `__proto__`, `constructor`, and `prototype` properties

---

## 3. Open Redirect

### What it is
Occurs when the application redirects users to a URL provided by the user.

### Bad Example
```javascript
window.location = params.redirect
```

Example URL:
```
site.com/login?redirect=https://evil.com
```

After login, the user gets redirected to a malicious site.

### Safer Approach
Use a whitelist of allowed routes:
```javascript
const allowedRoutes = ["/dashboard", "/profile"]
```
Check the redirect target before navigating.

---

## 4. Sensitive Data Exposure (Frontend)

### What it is
Sensitive data is exposed inside the frontend bundle.

### Examples
- API keys inside JavaScript
- Secrets inside React code
- Private tokens inside environment variables that are bundled

Example:
```javascript
const API_KEY = "sk_live_123456"
```

Anyone can see this using browser DevTools.

### Best Practices
- Never store secrets in the frontend
- Keep sensitive keys on the backend
- Use backend proxy APIs
- Treat frontend code as public

---

## 5. Client Storage Leaks

### What it is
Sensitive data stored in:
- localStorage
- sessionStorage
- IndexedDB

If an XSS vulnerability exists, attackers can steal this data.

### Bad Example
```javascript
localStorage.setItem("jwt", token)
```

### Best Practices
- Store only non-sensitive data
- Use short-lived tokens
- Avoid storing authentication tokens in localStorage
- Prefer httpOnly cookies (handled by backend)

---

## 6. Third-Party Script Risk

### What it is
When scripts are loaded from external CDNs and the CDN becomes compromised.

```html
<script src="https://cdn.example.com/script.js"></script>
```

If the script changes, malicious code may execute in your application.

### Solution – Subresource Integrity (SRI)
```html
<script
 src="https://cdn.com/lib.js"
 integrity="sha384-xxxxx"
 crossorigin="anonymous">
</script>
```

The browser verifies the script hash.  
If the script changes, it **will not execute**.

---

## Quick Summary

Frontend developers should mainly protect against:

1. XSS (DOM injection)  
2. Prototype pollution  
3. Open redirects  
4. Sensitive data exposure  
5. Client storage leaks  
6. Third-party script risks

These vulnerabilities cover a large percentage of **client-side attacks in web applications**.