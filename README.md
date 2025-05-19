
# Web Application Vulnerability Assessment Lab

This repository contains a comprehensive **hands-on lab** environment designed to teach and demonstrate **web application vulnerability assessments** using **Kali Linux** and industry-standard tools. It is tailored for cybersecurity students, ethical hackers, red teamers, and blue team defenders seeking real-world training on **XSS**, **CSRF**, **SQLi**, **CORS misconfigurations**, **XXE**, **SSTI**, **SSRF**, and more.



![Ethical cybersecurity hacker wearing black hoody](/blue_murrader.png)

---

## Objectives

- Build a professional-grade web app testing environment using **Kali Linux** and Dockerized targets.
- Learn how to discover, exploit, and defend against major web vulnerabilities.
- Use tools like **Burp Suite**, **XSStrike**, **sqlmap**, **ffuf**, and custom Python scripts.
- Understand how to implement and test **Content Security Policy (CSP)** and other modern defenses.
- Integrate blue team insights for logging, mitigation, and response.

---

## 🧱 Experiment Structure

### 📁 Module 0: Environment Setup
- Deploy Kali Linux with testing tools pre-installed
- Setup vulnerable apps: DVWA, OWASP Juice Shop, bWAPP
- Configure Burp Suite, Python server, browser proxying

---

### 🧪 Module 1: Cross-Site Scripting (XSS)
- 🔍 Reflected XSS Discovery with **XSStrike** and **Burp Suite**
- 💣 DOM-based XSS with **OWASP Juice Shop**
- ⚠️ Data exfiltration using browser scripting and Python HTTP server
- 🛡️ Defense validation with **CSP headers**

---

### 🔐 Additional Modules (Coming Soon)
- **Module 2**: Cross-Site Request Forgery (CSRF)
- **Module 3**: CORS Misconfigurations & Exploits
- **Module 4**: SQL Injection & Database Enumeration
- **Module 5**: Directory Traversal & File Disclosure
- **Module 6**:Server-Side Template Injection (SSTI) & SSRF Chains
- **Module 7**: Advinced Sequence: XXE + SSRF + DoS Chains

Each module will include:
- Definitions and theory
- Manual and automated exploitation
- Evasion and obfuscation techniques
- Blue team detection and mitigation walkthrough
- Case study and real-world context

---

## 🛠 Tools Used

- Kali Linux (latest)
- Burp Suite
- XSStrike
- sqlmap
- ffuf / gobuster
- Python 3.x (`http.server`)
- Docker (for target environments)
- Browser DevTools

---

##  Who This Is For

This lab is built for:
- SOC Analysts and Incident Responders
- Penetration Testers
- Blue Team Defenders
- Cybersecurity Students
- Offensive Security & CTF Competitors

---

## 📜 License

This project is licensed under the **Apache License 2.0** — see the [LICENSE](LICENSE) file for details.

---

## 📚 References

- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [Burp Suite Docs](https://portswigger.net/burp/documentation)
- [XSStrike GitHub](https://github.com/s0md3v/XSStrike)
- [Juice Shop](https://owasp.org/www-project-juice-shop/)

---

> Use these experiments ethically, legally, and within authorized environments. This is an educational tool for students, defenders, and researchers.
