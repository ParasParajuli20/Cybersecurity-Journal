# **OWASP Top 10 Deep Dive**  

The **OWASP Top 10** is a standard awareness document for web application security risks, updated periodically to reflect the evolving threat landscape. As an **Application Security Pentester**, understanding these vulnerabilities is crucial for both offensive testing and defensive hardening.  

In this blog, we’ll break down each **OWASP Top 10 (2021)** vulnerability with:  
✔ **Real-world examples**  
✔ **How attackers exploit them**  
✔ **Best mitigation strategies**  

---

## **1. Broken Access Control**  
**Definition:** Unauthorized users gain access to restricted functionality/data (e.g., admin panels, sensitive files).  

### **Example Exploit:**  
- **IDOR (Insecure Direct Object Reference):**  
  ```plaintext
  https://example.com/profile?user_id=123 → Change to user_id=124 (access another user’s data).
  ```  
- **JWT Tampering:** Modifying a token’s `role: user` → `role: admin`.  

### **Mitigation:**  
- Implement role-based access control (RBAC).  
- Validate permissions on every request (never trust client-side checks).  
- Use UUIDs instead of sequential IDs.  

---

## **2. Cryptographic Failures**  
**Definition:** Weak encryption leads to data leaks (e.g., passwords, credit cards).  

### **Example Exploit:**  
- **Storing passwords in plaintext** (e.g., 2022 Twitter breach).  
- **Using deprecated algorithms** (e.g., MD5, SHA-1).  

### **Mitigation:**  
- Always use strong hashing (Argon2, bcrypt, PBKDF2).  
- Enforce TLS 1.2/1.3 (disable SSLv3, TLS 1.0).  
- Never hardcode keys/secrets in source code.  

---

## **3. Injection**  
**Definition:** Malicious data tricked into being executed (SQLi, XSS, OS command injection).  

### **Example Exploit:**  
- **SQL Injection (SQLi):**  
  ```sql
  ' OR '1'='1' --  → Dumps entire database.
  ```  
- **XSS (Cross-Site Scripting):**  
  ```html
  <script>alert(document.cookie)</script> → Steals sessions.
  ```  

### **Mitigation:**  
- Use prepared statements (parameterized queries).  
- Sanitize inputs with allowlists (not blocklists).  
- Implement CSP (Content Security Policy) for XSS.  

---

## **4. Insecure Design**  
**Definition:** Flaws in architecture/design (e.g., missing authentication checks).  

### **Example Exploit:**  
- **"Forgot Password" flow allows unlimited attempts** → Account brute-forcing.  

### **Mitigation:**  
- Follow secure-by-design principles.  
- Perform threat modeling before development.  

---

## **5. Security Misconfiguration**  
**Definition:** Default settings, verbose errors, or exposed services.  

### **Example Exploit:**  
- **Exposed `.git` directory** → Source code leakage.  
- **Default admin credentials** (`admin:admin`).  

### **Mitigation:**  
- Disable debug mode in production.  
- Regularly scan for misconfigurations (using tools like Nessus).  

---

## **6. Vulnerable & Outdated Components**  
**Definition:** Using libraries/frameworks with known CVEs.  

### **Example Exploit:**  
- **Log4j (CVE-2021-44228)** → RCE via JNDI lookup.  

### **Mitigation:**  
- Use dependency scanners (OWASP Dependency-Check, Snyk).  
- Patch immediately when updates are available.  

---

## **7. Identification & Authentication Failures**  
**Definition:** Weak login mechanisms (e.g., brute-forcing, session hijacking).  

### **Example Exploit:**  
- **No rate-limiting** → Credential stuffing attacks.  
- **Session fixation** (reusing session IDs).  

### **Mitigation:**  
- Enforce MFA (Multi-Factor Authentication).  
- Use short-lived JWT tokens.  

---

## **8. Software & Data Integrity Failures**  
**Definition:** Unauthorized code/data modifications (e.g., CI/CD breaches).  

### **Example Exploit:**  
- **Malicious npm packages** (e.g., `event-stream` incident).  

### **Mitigation:**  
- Use code signing (e.g., GPG).  
- Verify third-party dependencies before use.  

---

## **9. Security Logging & Monitoring Failures**  
**Definition:** Lack of detection for breaches.  

### **Example Exploit:**  
- Attackers **cover tracks** due to missing logs.  

### **Mitigation:**  
- Implement centralized logging.   
- Set up real-time alerts for suspicious activity.  

---

## **10. Server-Side Request Forgery (SSRF)**  
**Definition:** Forcing a server to make unauthorized requests (e.g., internal API calls).  

### **Example Exploit:**  
```plaintext
https://example.com/fetch?url=http://169.254.169.254 → AWS metadata leak.
```  

### **Mitigation:**  
- Blocklist internal IPs/reserved domains.  
- Use allowlists for URLs.  

---

## **Final Thoughts**  
The OWASP Top 10 is a **must-know** for pentesters, developers, and security teams. By understanding these vulnerabilities, you can:  
✅ **Harden applications** against common attacks.  
✅ **Write better pentest reports** with clear remediation steps.  
✅ **Stay ahead of attackers** by anticipating their moves.  

**Want to practice?** Set up a lab with **DVWA (Damn Vulnerable Web App)** or **OWASP Juice Shop** and exploit these flaws yourself!  

🔗 **Further Reading:**  
- [OWASP Official Site](https://owasp.org/www-project-top-ten/)  
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)  
 
