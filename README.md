# Advanced Blind SQL Injection Exploiter

![GitHub stars](https://img.shields.io/github/stars/cybernock/Advanced-Blind-SQL-Injection?style=social)
![GitHub forks](https://img.shields.io/github/forks/cybernock/Advanced-Blind-SQL-Injection?style=social)

An advanced, multi-threaded blind SQL injection exploitation tool with support for **PostgreSQL**, **MySQL**, and **MSSQL**. It includes features like **WAF evasion**, **stealth mode**, **session resumption**, **custom headers**, and **detailed output logging**.

> **FOR EDUCATIONAL AND AUTHORIZED TESTING PURPOSES ONLY**

## 🚀 Features

- ✅ Boolean-based blind SQLi exploitation
- ✅ Supports PostgreSQL, MySQL, and MSSQL
- ✅ Threading support with progress tracking
- ✅ WAF evasion using stealth `BETWEEN` payloads and case obfuscation
- ✅ Session save/resume with JSON state file
- ✅ Custom headers, cookies, proxy support
- ✅ Auto-detection of true/false HTTP response codes
- ✅ Dumps database banner, user, schema, tables, columns, and data

---

## 📦 Installation

```bash
git clone https://github.com/cybernock/Advanced-Blind-SQL-Injection.git
cd Advanced-Blind-SQL-Injection
pip install -r requirements.txt
