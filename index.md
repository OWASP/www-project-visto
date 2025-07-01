---

layout: col-sidebar
title: OWASP VISTO (Vulnerability Intelligence & Security Testing Orchestrator)
tags: deployment-tag
level: 2
type: code
pitch: A very brief, one-line description of your project

---

VISTO is a prototype AI-powered agent designed to empower penetration testing teams by streamlining initial reconnaissance, automating data collection, and providing insightful, actionable analysis. The core objective is to help pentest teams:

* Systematically Conduct Pentests: Ensure a consistent and auditable approach to early-stage assessments.
* Maintain Comprehensive Audit Trails: Automatically record every command executed and its output, providing a clear history of testing activities for compliance and review.
* Maximize Pentester Efficiency: By automating basic checks and managing pentest data, VISTO aims to free up valuable time for human pentesters, allowing them to focus on more complex manual advanced testing, exploit development, and deeper vulnerability research.
* Ensure Data Privacy and Portability: Leveraging local Large Language Models (LLMs) for analysis, and sensitive testing data never leaves your controlled environment, preventing potential data leaks to public LLM services. This also makes the tool highly portable for use in various isolated testing environments.
* Generate Actionable Reports: The tool can generate a concise, executive-level security report, transforming raw findings and LLM analyses into structured, prioritized recommendations.

### Road Map
The initial workable version has been completed.

Platform Features

* Project Management: Organize your penetration tests into distinct projects with dedicated sessions.
* Audit Trails: All command executions, outputs, and LLM analyses are logged and stored, forming an invaluable audit trail accessible per project.
* 2-Factor Authentication (2FA): (Optional) Enhanced login security for the web interface.
* AI Assistant (ask_ai): Engage with a local LLM for general cybersecurity questions and advice.
* LLM-Powered Analysis: Receive immediate, technical insights and concise remediation suggestions for each command's output.
* Automated Executive Reporting: Generate a comprehensive security report summarizing all findings, categorizing vulnerabilities, and providing prioritized remediation steps.

Modular Functionality Overview ( 👷 Keep updating )

* OSINT (Open Source Intelligence): Gather public information on IPs, domains, and FQDNs (e.g., WHOIS, geolocation, subdomain enumeration, Shodan checks, TLS information).
* Network Discovery: Scan specified IP ranges or subnets to identify active hosts.
* IP Scanning: Perform port scanning on single or multiple IP addresses/FQDNs, with support for various Nmap flags and default top 500 port scanning.
