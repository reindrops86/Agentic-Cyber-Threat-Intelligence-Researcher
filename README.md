# Agentic-Cyber-Threat-Intelligence-Researcher
A production-style starter for an AI-assisted CTI workflow.

# Agentic CTI Researcher

A lightweight cyber threat intelligence (CTI) triage workflow that extracts indicators from raw threat text, enriches them with local intel, scores risk, raises alerts, and stores case records for analyst follow-up.

## Overview

This project is a production-style starter for an AI-assisted CTI workflow. It can:

- Extract indicators from raw threat text
- Identify likely MITRE ATT&CK techniques
- Score risk by confidence and malicious signal strength
- Generate analyst-facing summaries and alerts
- Maintain a local case queue with related-case matching
- Optionally call Azure OpenAI for a richer threat brief when configured

## Files

- [CTIcode.py](CTIcode.py) — main CTI workflow and CLI entrypoint
- [README.md](README.md) — project documentation
- `cti_memory.json` — created automatically when cases are analyzed

## Requirements

- Python 3.10+
- Standard library only

## Usage

Run against a text string:

```bash
python CTIcode.py --text "Payroll login secure domain payroll-login-secure.co and IP 185.220.101.42"
```

Run against a file:

```bash
python CTIcode.py --file threat_report.txt
```

Assign an analyst and add a note:

```bash
python CTIcode.py --text "Malicious domain observed." --assignee "Analyst A" --note "Initial triage review."
```

Update the case status:

```bash
python CTIcode.py --text "Malicious domain observed." --assignee "Analyst A" --status in_progress --status-note "Investigating phishing lure and C2 IP."
```

Write results to a JSON file:

```bash
python CTIcode.py --file threat_report.txt --output result.json
```

## Optional environment variables

These are optional and only needed for external enrichment or LLM summarization.

```bash
export AZURE_OPENAI_API_KEY="..."
export AZURE_OPENAI_ENDPOINT="https://<resource>.openai.azure.com"
export AZURE_OPENAI_DEPLOYMENT="gpt-4o-mini"
export AZURE_OPENAI_API_VERSION="2024-02-01"

export ABUSEIPDB_API_KEY="..."
export VIRUSTOTAL_API_KEY="..."
```

If these values are not set, the script falls back to local intelligence data and a built-in summary.

## Output

The script prints a JSON object to stdout with values such as:

- `case_id`
- `status`
- `priority`
- `severity`
- `risk_score`
- `summary`
- `indicators`
- `alerts`
- `related_cases`
- `case_queue`

## Notes

- The local threat feed is intentionally lightweight and suitable for demos or lab environments.
- Case history is persisted to `cti_memory.json` so related cases can be matched across runs.
- For production deployments, replace the simulated enrichment logic with real threat intel integrations and a persistent case-management system.

## Example

The script includes a default sample threat report with a phishing lure, fake payroll domain, C2 IP, suspicious hash, and ransomware-linked infrastructure. Running without arguments uses that content and produces a CTI assessment automatically.
