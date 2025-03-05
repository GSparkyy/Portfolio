# 2FA broken logic

> **Vulnerability Type:** Authentication  
> **Lab URL:** [Authentication Lab](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-broken-logic)

---

## Objective  
Bypass 2FA and access the "my account" page on Carlos' account.

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

---

### 1. **Discovery**  
- **Initial Observations:**  
  - When logging into the provided account, there are two `/login2` URLs.
- **Testing Approach:**  
  - Checking the two `/login2` URLs, one doesn't have the `mfa-code` parameter, and one does. The first sends the code to the email, the second checks for the code to log you in. Using Burp Repeater, I send an MFA code to Carlos.
  - Using Burp Intruder, I brute force Carlos' MFA code. Using the intercept function, I change the verify parameter to Carlos, input his obtained MFA code, and log into his account to complete the lab.

### 2. **Exploitation**  
- **Payload Used:**
  ```
  Bruteforce Burp Intruder
  ```
  ---
### 3. **Screenshots**
Creating the MFA code and sending it to carlos
![Screenshot 2025-03-05 184242](https://github.com/user-attachments/assets/657312e3-ab65-4680-84b1-16b3664b9423)
Intruder showing a successful 302 code showing the code is 1127
![Screenshot 2025-03-05 184320](https://github.com/user-attachments/assets/f09c88f9-8f22-4cb9-9d9d-71a6e9f9e3fa)
