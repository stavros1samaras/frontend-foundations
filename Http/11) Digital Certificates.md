# HTTPS Infrastructure & Digital Certificates

HTTPS relies on **trust** to secure communication between clients and web servers.

---

## How HTTPS Works
1. **Authentication** – The browser verifies the authenticity of the web server.
2. **Encryption** – All communication is encrypted to ensure security and privacy.

### Analogy
- Like showing a **passport** at border control:
  - The officer trusts your passport because it is issued by a trusted government.
  - Similarly, browsers trust websites based on **digital certificates**.

---

## Digital Certificates
- Also called **SSL or TLS certificates**.
- Serve as an **official ID for websites**, proving legitimacy.
- If invalid, browsers show a **security warning**.

---

## Chain of Trust
HTTPS certificates follow a **hierarchical trust model**:

1. **Root Certificate Authority (Root CA)**  
   - Highly secure entity at the top of the hierarchy.
   - Installed in browsers’ or OS trust stores.
2. **Intermediate Certificate Authorities (Intermediate CAs)**  
   - Signed by the Root CA.
   - Delegate certificate issuance for security and scalability.
3. **End-entity Certificates (Leaf Certificates)**  
   - Installed on websites.
   - Trusted because they descend from a trusted intermediate CA.

**Trust is established** because the certificate chain traces back to a trusted Root CA.

---

## Viewing a Certificate
- Click the **padlock icon** in the browser address bar.
- View the **certificate details**:
  - Issuer
  - Validity period
  - Serial number, policies, key usage, etc.

---

## Trust Store
- A local repository of trusted Root CAs.
- Browsers trust any certificate that descends from a Root CA in the trust store.

---

**Takeaway:**  
HTTPS ensures both **authentication** and **encryption** through a chain of trust, protecting users from interception, tampering, and impersonation.
