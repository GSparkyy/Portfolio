# Template for PortSwigger Lab Write-Ups

This is the template I use for documenting my write-ups. It ensures a consistent, professional structure to showcase my methodology, tools, and findings effectively.

---

## Template  

# [Lab Name Here]
> **Vulnerability Type:** [e.g., SQL Injection, XSS, SSRF]  
> **Lab URL:** [Link to the lab, if applicable]  

---

## Objective
[Briefly explain what the goal of the lab is. For example, "Exploit the SQL injection vulnerability to retrieve the admin password from the database."]

---

## Setup
- **Tools Used:** [e.g., Burp Suite, browser developer tools]
- **Environment Details:** [e.g., PortSwigger Academy, targeting login functionality]

---

## Methodology

### 1. **Discovery**
- **Initial Observations:**  
  [Describe what you noticed about the application or target. For instance, "An input field on the login page accepts user data."]  
- **Testing Approach:**  
  [Document how you tested for vulnerabilities, e.g., "Injected `' OR '1'='1` in the username field and observed that login bypassed."]

### 2. **Exploitation**
- **Payloads Used:**  
  ```plaintext
  [List any payloads or scripts you used. For example: ' OR 1=1; --']
