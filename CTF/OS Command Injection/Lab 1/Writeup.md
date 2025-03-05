# Blind OS Command Injection with Output Redirection

> **Vulnerability Type:**   OS Command Injection  
> **Lab URL:** [OS Command Injection Lab](https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection)

---

## Objective  
Execute the `whoami` command and retrieve the output. Given the hint that there is a writable folder at `/var/www/images/`, where you can redirect the output from the injected command to. Then, use the image loading URL to retrieve the contents of the folder.

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

--- 

### 1. **Discovery**  
- **Initial Observations:**  
  - The only input fields I found were on the feedback page: Name, Email, Subject, and Message.
- **Testing Approach:**  
  - Submitted feedback and scanned the HTTP request using Burp Scanner. Identified an OS command injection vulnerability in the email, message and subject parameters of the request.
  - Also found potential SQL injection and shell injection vulnerabilities, but focused on OS command injection since it is the lab's main focus.
  - Using the hint about the writable file at `/var/www/images/`, crafted a payload to write the details of the `whoami` command to a `.txt` file: `whoami>/var/www/images/output.txt`. Received an HTTP/2 200 OK response.
  - Found an HTTP request calling an image. Changed the filename to `output.txt` and got the response: `peter-jQZtiR`, completing the lab.

---

### 2. **Exploitation**  
- **Payload Used:**  
  ```shell
  ||whoami>/var/www/images/output.txt||
  ```
### 3. **Screenshots**
Putting the initial finding of Burp scanner into repeater to show the OS command injection vulnerability. (notice the "Could not save")
![Screenshot 2025-03-05 131324](https://github.com/user-attachments/assets/3512a326-fcc2-45af-a063-f54c82f8102a)
---
The whoami command being saved to output.txt
![Screenshot 2025-03-05 131425](https://github.com/user-attachments/assets/b93ad343-94b1-476e-abeb-983830dcb9a0)
Completing the lab by pulling the information from output.txt
![Screenshot 2025-03-05 131518](https://github.com/user-attachments/assets/df92335c-baec-4b40-9b45-9bd0efb9fdd2)
