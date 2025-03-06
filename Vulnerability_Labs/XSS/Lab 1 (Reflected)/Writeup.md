# Reflected XSS into HTML Context with Most Tags and Attributes Blocked

> **Vulnerability Type:** Reflected XSS 
> **Lab URL:** [XSS Lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked)

---

## Objective  
Perform an XSS (cross-site scripting) attack to call the `print()` function whilst bypassing the WAF (web application firewall).

---

## Setup  
- **Tools Used:** Burp Suite  
- **Environment Details:** PortSwigger Lab  

---

## Methodology  

### 1. **Discovery**  
- **Initial Observations:**  
  Upon opening the homepage, notice the search bar and input a `<script>` tag. Get the response "tag is not allowed," showing this is possibly vulnerable to XSS but has a filter.

- **Testing Approach:**  
  - Using the [XSS Cheat Sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) provided by PortSwigger for a more efficient approach. I send the request to Intruder with the area between the `<` and `>` characters highlighted for brute force. The payloads "body" and "custom tags" are the only ones that return a status code of 200 instead of 400 (error), showing the WAF doesn't filter them out.
  - I then switch the payload to `<body x=l>` with the `x` being highlighted in Intruder to test for events. `onresize` seems the easiest to perform via link that has a 200 status code.
  - Final payload with the event, tag, and print function being called via iframe hosted on the provided exploit server:

  ```html
  <iframe src="https://0a6d000003f9ebf28259109e006a003c.web-security-academy.net/?search=%22%3E%3Cbody onresize=print()%3E" onload=this.style.width='100px'>

### 2. **Exploitation**  
- **Payload Used:**  
  ```XSS
  <x> - `x` highlighted in Intruder to get vulnerable tag
  <body x=1> - with `x` highlighted in Intruder to get vulnerable event
### 3. **Screenshot**
  Below is a screenshot of the 200 status codes in BurpSuite Intruder showing the vulnerable tags.
![Screenshot 2025-03-04 123948](https://github.com/user-attachments/assets/7b71eae3-cc15-4794-9235-4a4812f2e4d5)
