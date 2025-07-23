# Advanced Blind SQL Injection Tool v2.0

A comprehensive Python-based blind SQL injection exploitation tool designed for authorized penetration testing and educational purposes. This tool supports multiple database engines, advanced WAF evasion techniques, concurrent processing, and intelligent session management.

## ⚠️ Legal Disclaimer

**This tool is intended for authorized security testing and educational purposes ONLY.** Unauthorized access to computer systems is illegal and unethical. Users are solely responsible for ensuring they have explicit permission to test target systems and must comply with all applicable laws and regulations.

## ✨ Features

- **Multi-Database Support**: PostgreSQL, MySQL, and Microsoft SQL Server
- **Advanced WAF Evasion**: Comment insertion, case randomization, and BETWEEN operator mode
- **Intelligent Threading**: Concurrent character extraction with configurable thread pools
- **Session Management**: Automatic progress saving and resumption capabilities
- **Enhanced Error Handling**: Automatic retry mechanisms and graceful failure recovery
- **Flexible Data Extraction**: Custom queries, table enumeration, and selective data dumping
- **Stealth Mode**: BETWEEN operator usage for enhanced evasion
- **Comprehensive Logging**: Detailed logging with statistics and progress tracking
- **Proxy Support**: HTTP/HTTPS proxy integration for testing through tools like Burp Suite

## 🛠️ Installation

### Prerequisites

- Python 3.7 or higher
- Required Python packages: `requests`

### Setup

1. **Clone the repository:**
```bash
git clone https://github.com/cybernock/Advanced-Blind-SQL-Injection.git
cd Advanced-Blind-SQL-Injection
```

2. **Install dependencies:**
```bash
pip install requests
```

3. **Make the script executable (optional):**
```bash
chmod +x sqli_exploiter.py
```

## 🚀 Usage

### Basic Usage Examples

**Dump database version:**
```bash
python sqli_exploiter.py --banner --url "https://example.com/api" --threads 10
```

**Enumerate all databases:**
```bash
python sqli_exploiter.py --dbs --url "https://example.com/api" --db-engine postgresql
```

**Extract table data with custom columns:**
```bash
python sqli_exploiter.py --fetch -D mydb -T users -C "username,email,password" --start 1 --stop 100
```

**Use stealth mode with proxy:**
```bash
python sqli_exploiter.py --banner --stealth --proxy "http://127.0.0.1:8080" --delay 1.0
```

### Advanced Usage Examples

**Custom SQL query execution:**
```bash
python sqli_exploiter.py --query "SELECT COUNT(*) FROM sensitive_table" -D production_db
```

**Complete database enumeration:**
```bash
python sqli_exploiter.py --dbs --tables -D target_db --columns -D target_db -T users
```

**Resume interrupted session:**
```bash
# The tool automatically detects and offers to resume previous sessions
python sqli_exploiter.py --fetch -D mydb -T large_table
```

## 📋 Command-Line Options

### Actions
| Option | Description |
|--------|-------------|
| `--banner` | Dump database version banner |
| `--user` | Dump current database user |
| `--current-db` | Dump current database name |
| `--dbs` | Enumerate all database names |
| `--schemas` | Enumerate schemas in database (requires `-D`) |
| `--tables` | Enumerate tables in database (requires `-D`) |
| `--columns` | Enumerate columns in table (requires `-D`, `-T`) |
| `--fetch` | Extract data from table (requires `-D`, `-T`) |
| `--query SQL` | Execute custom SQL query and dump result |
| `--flush-session` | Clear saved session and exit |

### Target Specification
| Option | Description |
|--------|-------------|
| `--url URL` | Base URL for injection (default: https://host/api) |
| `--suffix PATH` | URL suffix after injection point (default: /endpoint) |
| `--injection-point PARAM` | Injection point parameter name (default: value) |
| `--headers HEADERS` | Custom headers (format: 'Header1:Value1,Header2:Value2') |
| `--cookie COOKIE` | Cookie header value |
| `--proxy PROXY` | HTTP proxy (e.g., http://127.0.0.1:8080) |

### Database Options
| Option | Description |
|--------|-------------|
| `-D, --database DB` | Target database name |
| `-T, --table TABLE` | Target table name |
| `--schema SCHEMA` | Target schema name (optional) |
| `-C, --column COLS` | Comma-separated column names for --fetch |
| `--db-engine ENGINE` | Target database engine (postgresql/mysql/mssql) |

### Data Extraction
| Option | Description |
|--------|-------------|
| `--start N` | Start row for --fetch (1-based, default: 1) |
| `--stop N` | Stop row for --fetch (inclusive) |

### Request Configuration
| Option | Description |
|--------|-------------|
| `--threads N` | Concurrent threads (default: 15) |
| `--delay SECONDS` | Delay between requests in seconds (default: 0.0) |
| `--true-code CODE` | HTTP status code for TRUE conditions |
| `--false-code CODE` | HTTP status code for FALSE conditions |
| `--auto-detect` | Auto-detect TRUE/FALSE status codes |

### Evasion Options
| Option | Description |
|--------|-------------|
| `--stealth` | Use BETWEEN operator for WAF evasion (slower) |

### Output Options
| Option | Description |
|--------|-------------|
| `--verbose` | Enable verbose output |
| `--output FILE` | Save results to file |
| `--continue-on-error` | Continue execution even if an action fails |

## 📊 Sample Output

```
================================================================================
[*] Action: Dumping Database Banner
--------------------------------------------------------------------------------
[*] Target SQL: version()
[*] Database Engine: POSTGRESQL
[*] Target URL: https://example.com/api[PAYLOAD]/endpoint
[*] Injection Point: value
[*] Threads: 15
[*] Mode: Fast (> operator)
[*] Response Codes: True=200, False=500
[*] Request Delay: 0.0s
================================================================================

[12:34:56] [INFO] Discovering Length of Database Banner...
[12:34:57] [SUCCESS] Discovered Length of Database Banner: 87
[12:34:57] [INFO] Extracting Database Banner (87 characters)...
[+] Progress: PostgreSQL 13.7 on x86_64-pc-linux-gnu, compiled by gcc 9.4.0 (100.0%)

Database Banner:
==================================================
PostgreSQL 13.7 on x86_64-pc-linux-gnu, compiled by gcc 9.4.0
==================================================

============================================================
SESSION STATISTICS
============================================================
Total Requests Sent: 156
Failed Requests: 0
Success Rate: 100.0%
Characters Extracted: 87
Strings Extracted: 1
Total Time: 12.3 seconds
Average Request Time: 0.08 seconds
============================================================
```

## 📁 Session Management

The tool automatically saves progress to `sqli_session.json` and offers to resume interrupted sessions. Session files include:

- Progress tracking for each action
- Partial character extraction data
- Request statistics
- Command-line arguments validation

To clear sessions:
```bash
python sqli_exploiter.py --flush-session
```

## 🔧 Configuration

Default configuration can be modified in the script:

```python
TARGET_URL_BASE = "https://host/api"
URL_SUFFIX = "/endpoint"
TRUE_STATUS_CODE = 200
FALSE_STATUS_CODE = 500
MAX_STRING_LENGTH = 200
DEFAULT_THREADS = 15
```

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/enhancement`)
3. **Commit your changes** (`git commit -am 'Add new feature'`)
4. **Push to the branch** (`git push origin feature/enhancement`)
5. **Create a Pull Request**

### Development Guidelines

- Follow PEP 8 coding standards
- Add comprehensive docstrings
- Include error handling for new features
- Test with multiple database engines
- Update documentation for new options

## 📝 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**cybernock**
- GitHub: [@cybernock](https://github.com/cybernock)
- Repository: [Advanced-Blind-SQL-Injection](https://github.com/cybernock/Advanced-Blind-SQL-Injection)

## ⚖️ Ethical Use Statement

This tool was developed to assist security professionals in identifying and addressing SQL injection vulnerabilities in web applications. It should only be used on systems where you have explicit written authorization to perform security testing.

**Prohibited Uses:**
- Testing systems without proper authorization
- Accessing data without permission
- Any malicious or illegal activities

**Recommended Uses:**
- Authorized penetration testing
- Security research and education
- Vulnerability assessment with proper consent
- Bug bounty programs where applicable

By using this tool, you acknowledge that you understand these restrictions and agree to use it responsibly and ethically.

*For questions, issues, or feature requests, please open an issue on the [GitHub repository](https://github.com/cybernock/Advanced-Blind-SQL-Injection/issues).*

[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/15888274/2670b18c-4236-4d0a-a909-506f2c36cd50/urls.txt
