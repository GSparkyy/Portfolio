# SQL Injection Vulnerability Allowing Login Bypass
> **Vulnerability Type:** SQL Injection  
> **Lab URL:** [SQL Injection Lab on PortSwigger](https://portswigger.net/web-security/sql-injection/lab-login-bypass)  

---

## Objective
Exploit the SQL injection vulnerability to log in as the "administrator" user.

---

## Setup
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Academy SQL Injection Lab

---

## Methodology

### 1. **Discovery**
- **Initial Observations:**  
  Identified two input fields (Username and Password) on the login page that accept user input. No additional inputs or interactive elements were available.  

- **Testing Approach:**  
  - Tested the Username field with a single quotation mark (`'`) and observed an SQL-related error message.  
  Entered two quotation marks (`''`) and received "Invalid username or password."  
  These behaviors suggested the username field was processing user input directly within an SQL query, indicating a vulnerability.

---

### 2. **Exploitation**
- **Approach:**  
  Used SQL injection to manipulate the query logic, bypassing the password check by commenting out the remaining query.  

- **Payloads Used:**  
  ```plaintext
  administrator'--
