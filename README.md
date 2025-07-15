# 💥 SQL Injection Exploitation using OWASP Juice Shop & ZAP Proxy

This project explores the risks of SQL Injection by demonstrating how malicious users can exploit insecure database queries in web applications. Using OWASP Juice Shop and tools like Kali Linux and ZAP Proxy, we perform both manual and automated SQL Injection attacks, and discuss best practices for securing web apps from such vulnerabilities.

---

## 🎥 Video Demonstration

**YouTube**: [ZAP Proxy & SQL Injection Demo](https://your-link-here)

---

## 🔐 What is SQL Injection?

SQL Injection is a technique where attackers insert or "inject" malicious SQL code into input fields to manipulate a database query. If successful, this can give attackers access to data they shouldn’t see, allow them to bypass login pages, or even take over the backend system entirely.

---

## ⚠️ Why Is It Dangerous?

- Allows unauthorized access to databases
- Enables data exfiltration, manipulation, or deletion
- Can lead to full system compromise
- Often results from poor input validation and insecure query building

---

## 🧪 Lab Environment & Tools

- **Kali Linux** (running in VMware)
- **Node.js & npm** (for Juice Shop)
- **OWASP Juice Shop** (vulnerable web application)
- **ZAP Proxy (Zaproxy)** – automated scanner and traffic interceptor
- **Firefox** – browser used with manual proxy settings

---

## ⚙️ Manual SQL Injection Attack

### 1. Set Up Juice Shop

``` bash
sudo apt update && sudo apt install -y nodejs npm
git clone https://github.com/juice-shop/juice-shop.git
cd juice-shop
npm install
npm start
Visit http://localhost:3000 in your browser.

```

## 2. Perform SQL Injection
Go to the login page

``` bash

In the email field, enter: ' OR '1'='1'--

```

Leave the password blank

Log in

## 🎯 Result: Access granted using an altered SQL query like:

```

sql
Copy
Edit
SELECT * FROM users WHERE email = '' OR '1'='1' --' AND password = '';
This always evaluates as true, granting access without valid credentials.

```

## 🧰 ZAP Proxy Walkthrough – Automated SQL Injection Detection

Step 1: Install ZAP

```
bash
Copy
Edit
sudo apt update && sudo apt install zaproxy -y
zaproxy &
Step 2: Re-Run Juice Shop
bash
Copy
Edit
cd juice-shop
npm start
Juice Shop is now running at: http://localhost:3000

```

## Step 3: Configure Proxy in Firefox
Go to Firefox settings → Network → Manual Proxy Configuration

Set:

HTTP Proxy: 127.0.0.1

Port: 8080

Check "Use this proxy for all protocols"

## Step 4: Intercept & Scan with ZAP
Visit Juice Shop in Firefox while ZAP is running

ZAP intercepts traffic and runs active scans

Result: 14 vulnerabilities found, including critical SQL Injection

## Step 5: Exploit Confirmed
Re-test with the ' OR '1'='1'-- injection and confirm successful login.

## 🔒 How to Prevent SQL Injection
✅ Use Prepared Statements / Parameterized Queries
SELECT * FROM users WHERE email = ? AND password = ?;

✅ Input Validation and Sanitization
Restrict and validate user input; avoid dangerous characters

✅ Limit Privileges
Use non-admin database accounts for web apps

✅ Use Web Application Firewalls (WAFs)
Block known malicious payloads

✅ Regular Pen Testing & Code Audits
Continuously test and patch your web apps

## 📌 Key Takeaways
SQL Injection is a serious vulnerability that can be exploited with minimal effort

Tools like ZAP Proxy automate detection and confirm vulnerabilities

Mitigating SQLi requires strong security practices at the development and infrastructure levels
