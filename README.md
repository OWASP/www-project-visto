# VISTO (Vulnerability Intelligence & Security Testing Orchestrator) 
<sup>AI-Powered Penetration Testing Agent</sup>

**Objective and Vision**

`VISTO` is a prototype AI-powered agent designed to empower penetration testing teams by streamlining initial reconnaissance, automating data collection, and providing insightful, actionable analysis. The core objective is to help pentest teams:
- **`Systematically Conduct Pentests`**: Ensure a consistent and auditable approach to early-stage assessments.
- **`Maintain Comprehensive Audit Trails`**: Automatically record every command executed and its output, providing a clear history of testing activities for compliance and review.
- **`Maximize Pentester Efficiency`**: By automating basic checks and managing pentest data, VISTO aims to free up valuable time for human pentesters, allowing them to focus on more complex manual advanced testing, exploit development, and deeper vulnerability research.
- **`Ensure Data Privacy and Portability`**: Leveraging local Large Language Models (LLMs) for analysis, and sensitive testing data never leaves your controlled environment, preventing potential data leaks to public LLM services. This also makes the tool highly portable for use in various isolated testing environments.
- **`Generate Actionable Reports`**: The tool can generate a concise, executive-level security report, transforming raw findings and LLM analyses into structured, prioritized recommendations.

:star2: **Features**

VISTO is designed with modular functionality in mind, allowing for easy expansion. Contributions to module development are highly encouraged. Its current capabilities include:

<ins>Platform Features</ins>

- **`Project Management`**: Organize your penetration tests into distinct projects with dedicated sessions.
- **`Audit Trails`**: All command executions, outputs, and LLM analyses are logged and stored, forming an invaluable audit trail accessible per project.
- **`2-Factor Authentication (2FA)`**: (Optional) Enhanced login security for the web interface.
- **`AI Assistant (ask_ai)`**: Engage with a local LLM for general cybersecurity questions and advice.
- **`LLM-Powered Analysis`**: Receive immediate, technical insights and concise remediation suggestions for each command's output.
- **`Automated Executive Reporting`**: Generate a comprehensive security report summarizing all findings, categorizing vulnerabilities, and providing prioritized remediation steps.

<ins>Modular Functionality Overview</ins>  ( :construction_worker: Keep updating )

- **`OSINT (Open Source Intelligence)`**: Gather public information on IPs, domains, and FQDNs (e.g., WHOIS, geolocation, subdomain enumeration, Shodan checks, TLS information).
- **`Network Discovery`**: Scan specified IP ranges or subnets to identify active hosts.
- **`IP Scanning`**: Perform port scanning on single or multiple IP addresses/FQDNs, with support for various Nmap flags and default top 500 port scanning.

:question: **Why VISTO?**

- **`Boost Productivity`**: Spend less time on repetitive scanning and data aggregation, more time on critical thinking and complex exploitation.
- **`Consistent Methodology`**: Ensure all team members follow a standardized initial reconnaissance process, generating uniform audit data.
- **`Initial Reporting`**: Automatically produce reports that consolidate technical findings into actionable business insights.
- **`Data Sovereignty`**: Leverage the Local LLMs without compromising data sovereignty. Your data stays local, always.
- **`Accelerated Learning & Onboarding`**: New team members can quickly get up to speed by observing command executions and instant LLM analyses.
- **`Air-gap Capability`**: Since it uses Local LLMs, VISTO is ideal for isolated network environments where internet access is restricted.

## :electric_plug: **Getting Started**

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
import os

class Config:
    """Application-wide configuration settings."""
    FLASK_SECRET_KEY = os.environ.get('FLASK_SECRET_KEY', 'your_super_secret_key_here_change_this_in_production_!!!')
    DATABASE_PATH = 'data/VISTO.db'
    LOG_DIR = 'data/logs'
    DATA_DIR = 'data'
    FLASK_PORT = 5000
    DEBUG_MODE = True
    NMAP_PATH = '/usr/bin/nmap'

    # LLM Configuration
    LLM_API_URL = os.environ.get('LLM_API_URL', 'http://localhost:11434/v1/chat/completions')
    LLM_MODEL_NAME = os.environ.get('LLM_MODEL_NAME', 'phi3')
    LLM_API_KEY = os.environ.get('LLM_API_KEY', 'your_llm_api_key_here_change_this_in_production_!!!')
    SHODAN_API_KEY = os.environ.get('SHODAN_API_KEY', 'your_shodan_api_key')

    # --- Scanning Control ---
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

## :computer: **Command Examples**

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

## :warning: **Important Considerations & Disclaimers**

- **`Authorised Testing Only`**: This tool may trigger various security testing utilities that interact with networks, systems, or applications in ways that could be considered intrusive or malicious. Ensure you have explicit authorisation and appropriate permissions before conducting any security testing. 
Unauthorised use of this tool may breach laws or regulations, and could result in disciplinary action, legal consequences, or criminal prosecution. 
Always test responsibly.
- **`Local Network Deployment Only`**: At its current stage, the authentication and security mechanisms of VISTO are designed for project segregation, not robust internet-facing security. DO NOT expose the web interface to the public internet. Deploy and use this tool only within trusted, isolated network environments (e.g., your internal pentest lab, a Kali VM with host-only networking).
- **`LLM Analysis Verification`**: The analyses and recommendations generated by the LLM are based on patterns learned from data. While powerful, they are not infallible. Always double-verify all LLM-generated analysis, findings, and remediation suggestions with your own expert judgment and manual testing. It is possible that the data presented could be incorrect, incomplete, or lead to false positives/negatives.
- **`Performance Notes`**: The code has been tested on a Kali Linux virtual machine with 8GB RAM and 4 vCPUs, using the phi3 LLM model. Under these specifications, the execution speed for individual commands is generally acceptable. However, LLM analysis, especially for comprehensive report generation, may still take several minutes depending on the complexity of the command output and the number of commands in the project.

## :octocat: **Contributions**

Contributions are welcome! If you have suggestions for improvements, bug reports, or want to contribute code, please open an issue or submit a pull request on the GitHub repository.

## :blue_book: **License**

VISTO is distributed under the Apache License 2.0.

## :computer: **Screenshots**

**`SC01. Screenshot of VISTO login page`**
![Screenshot of VISTO login page](/assets/images/Login_sample.png)

**`SC02. Screenshot of VISTO Dashboard`**
![Screenshot of VISTO Dashboard](/assets/images/Dashboard_sample.png)

**`SC03. Screenshot of VISTO project history (audit trail)`**
![Screenshot of project history (audit trail)](/assets/images/Project_History_sample_view.png)

**`SC04. Screenshot of VISTO LLM generated report`**
![Screenshot of a sample LLM generated report](/assets/images/LLM_generated_sample_report.png)
