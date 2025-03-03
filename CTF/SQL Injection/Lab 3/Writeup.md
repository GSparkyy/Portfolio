# SQL Injection UNION Attack: Retrieving Data from Other Tables  

> **Vulnerability Type:** SQL Injection  
> **Lab URL:** [SQL Injection Lab](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables)

---

## Objective  
Utilize an input field vulnerable to SQL Injection to extract user login credentials from the given columns "username" and "password" in the "users" table.

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

---

## Methodology  

### 1. **Discovery**  
- **Initial Observations:**  
  Among the three input fields available (the "username" and "password" fields on the "My Account" page, and the filter on the homepage), only the homepage filter was vulnerable.  
- **Testing Approach:**  
  - Tested the homepage filter with `'--` to trigger an error; then proceeded to test with `''--` which didn't provoke an error.  
  - Proceeded with a `UNION SELECT` statement to retrieve data from the "username" and "password" columns in the "users" table.  
  - Successfully extracted the credentials for "administrator" (`administrator:iin3r22buytsh3dk0u07`), granting access to the administrator's account and completing the lab.

### 2. **Exploitation**  
- **Payload Used:**  
  ```sql
  ' UNION SELECT username, password FROM users--  
