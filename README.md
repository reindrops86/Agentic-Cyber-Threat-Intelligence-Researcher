# Agentic-Cyber-Threat-Intelligence-Researcher
A production-style starter for an AI-assisted CTI workflow.

"""Agentic Cyber Threat Intelligence Researcher.

A production-style starter for an AI-assisted CTI workflow.

Features:
- Extracts indicators from raw threat text
- Identifies likely MITRE ATT&CK techniques
- Scores risk by severity and confidence
- Produces a human-readable triage report
- Optionally calls Azure OpenAI when environment variables are configured

Usage:
    python CTIcode.py --text "Malicious domain ..."
    python CTIcode.py --file threat_report.txt
"""
