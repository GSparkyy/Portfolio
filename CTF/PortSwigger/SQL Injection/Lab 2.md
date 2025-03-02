# SQL Injection UNION Attack: Finding a Column Containing Text

> **Vulnerability Type:** SQL Injection  
> **Lab URL:** [SQL Injection Lab](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text)

---

## **Objective**

Identify:
1. The number of columns in the query.
2. Columns that can handle textual data for extracting information.

---

## **Setup**

- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab

---

## **Methodology**

### **1. Discovery**

- **Initial Observations:**  
  While testing the "My account" page, its input fields ("Username" and "Password") did not seem vulnerable to SQL injection attacks. Shifting focus to the "Refine your search:" filter settings on the homepage revealed a vulnerability:  
  - Adding `'--` at the end of a query caused an error, while appending `''--` did not. This indicated potential SQL injection susceptibility within the filter functionality.

- **Testing Approach (Steps):**
  1. Start with a basic `UNION SELECT` payload to identify the number of columns in the query.  
  2. Gradually append `NULL` values to the payload (e.g., `UNION SELECT NULL`, `UNION SELECT NULL,NULL`, etc.).  
  3. Continue until a payload does not produce an error. This confirms the number of columns.  
     - Example: `UNION SELECT NULL, NULL, NULL` (if no error, there are three columns).  
  4. Replace `NULL` in each column sequentially with textual data (e.g., `'test'`) to determine which column(s) accept text.  
     - Example: `UNION SELECT NULL, 'test', NULL`.

---

### **2. Exploitation**

- **Payload Example Used:**  
  ```sql
  UNION SELECT NULL, 'example_text', NULL

 ---

 ### **3. Conclusion**
 In my lab there was 3 columns, and the second column was able to be used to extract data.
