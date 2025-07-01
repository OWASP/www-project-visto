---
title: Deployment
layout:  null
tab: true
order: 1
tags: deployment-tag
---

## **Getting Started**

<ins>Prerequisites</ins>
- *Kali Linux* (preferred and tested during development testing)
- Python 3.8+
- pip (Python package installer)
- nmap
- A local LLM server (by default: Ollama running phi3) [`Phi-3 is a family of open AI models developed by Microsoft.`]

<ins>Deployment</ins>

1. Install Ollama on Kali Linux
```
curl -fsSL https://ollama.com/install.sh | sh
```
2. After installation, confirm it's working
```
ollama --version
```
3. Pull the Phi-3 Model (You can use your preferred LLM, but please align with your hardware configuration)
```
ollama pull phi3:mini
```
4. Run Phi-3 Locally
```
ollama run phi3:mini
```
5. Clone the VISTO repository
```
git clone https://github.com/redblueteam/VISTO.git
cd VISTO
```
6. Create a virtual environment (recommended)
```
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```
7. Install dependencies
```
pip install -r requirements.txt
```
8. Set up config.py
```
    # Application-wide configuration settings.
    FLASK_SECRET_KEY = os.environ.get('FLASK_SECRET_KEY', 'your_super_secret_key_here_change_this_in_production_!')
    DATABASE_PATH = 'data/VISTO.db'
    LOG_DIR = 'data/logs'
    DATA_DIR = 'data'
    FLASK_PORT = 5000
    DEBUG_MODE = True
    NMAP_PATH = '/usr/bin/nmap'

    # LLM Configuration
    LLM_API_URL = os.environ.get('LLM_API_URL', 'http://localhost:11434/v1/chat/completions')
    LLM_MODEL_NAME = os.environ.get('LLM_MODEL_NAME', 'phi3')
    LLM_API_KEY = os.environ.get('LLM_API_KEY', 'your_llm_api_key_here_change_this_in_production_!')
    SHODAN_API_KEY = os.environ.get('SHODAN_API_KEY', 'your_shodan_api_key')

    # Scanning Control
    ALLOW_EXTERNAL_SCANNING = True
    INTERNAL_IP_RANGES = [
        "127.0.0.0/8",      # Loopback
        "10.0.0.0/8",       # Private A
        "172.16.0.0/12",    # Private B
        "192.168.0.0/16"    # Private C
        # Add any other internal IP ranges specific to your environment
    ]

```
9. Running the Application (Use sudo to ensure Nmap can perform a full scan, as non-privileged users may have limited scanning capabilities.)
```
sudo python3 app.py
```
10. Register a new user (For first-time use) via the WEB GUI
```
http://127.0.0.1:5000
```
11. Accessing the Dashboard (Authenticate with a valid user)
```
http://127.0.0.1:5000
```
12. Enable 2FA (Optional)
```
http://127.0.0.1:5000
```

## **Command Examples**

i. Network Discovery

`e.g., Scans a network range 192.168.1.0/24 for active hosts`
```
network_discovery 192.168.1.0/24
```
ii. IP address scanning

`e.g., Scans multiple IP addresses 192.168.1.1,192.168.1.2 for open ports/network services`
```
ip_scan 192.168.1.1,192.168.1.2
```
iii. OSINT

`e.g., Retrieves Shodan Information of an IP addresses (Shodan API Key is required to be configured in config.py)`
```
osint ip {PUBLIC_IP_ADDR} shodan_check
```
`e.g., Attempts to find subdomains for a given domain`
```
osint domain {domain_name} subdomain_enum
```
`e.g., Performs a WHOIS lookup for domain registration details`
```
osint domain {domain_name} whois_check
```
`e.g., Performs a TLS information check for a domain`
```
osint fqdn www.owasp.org tls_check
```
`e.g., Ask Local LLM for other questions`
```
ask_ai What is XSS? How to remediate?
```

## **Screenshots**

**`SC01. Screenshot of VISTO login page`**
![Screenshot of VISTO login page](https://github.com/OWASP/www-project-visto/blob/main/assets/images/Login_sample.png?raw=true)

**`SC02. Screenshot of VISTO Dashboard`**
![Screenshot of VISTO Dashboard](https://github.com/OWASP/www-project-visto/blob/main/assets/images/Dashboard_sample.png?raw=true)

**`SC03. Screenshot of VISTO project history (audit trail)`**
![Screenshot of project history](https://github.com/OWASP/www-project-visto/blob/main/assets/images/Project_History_sample_view.png?raw=true)

**`SC04. Screenshot of VISTO LLM generated report`**
![Screenshot of a sample LLM generated report](https://github.com/OWASP/www-project-visto/blob/main/assets/images/LLM_generated_sample_report.png?raw=true)
