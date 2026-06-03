# Phishing Email Analyzer

A Kiro skill for analyzing and identifying phishing emails, designed for sales teams in international trade companies.

## Overview

This skill acts as a red team anti-fraud expert, helping sales colleagues identify and respond to phishing email threats. It provides business-first security analysis — protecting against attacks without killing potential deals.

## Key Features

- **Phishing Detection**: Identifies credential harvesting, BEC attacks, malicious attachments, and social engineering tactics
- **Three-Level Alert System**: Clear risk classification (🟢 Safe / 🟡 Suspicious / 🔴 Critical) with actionable next steps
- **Business-First Approach**: Balances security with business needs — never kills a potential deal without offering a safe verification path
- **Source Code Analysis**: Analyzes HTML/JavaScript source code of suspicious attachments to detect hidden phishing logic
- **URL Reputation Check**: Queries domain reputation and registration info for suspicious links

## Threat Coverage

- Fake login pages (Google, Microsoft 365, SSO)
- BEC / CEO fraud attacks
- Malicious attachments (.html, .pdf, .zip with embedded scripts)
- Payment redirection scams
- OAuth authorization hijacking
- Spear phishing targeting specific individuals

## Installation

1. Download or clone this repository
2. Place the `phishing-email-analyzer` folder into your Kiro skills directory
3. The skill will be automatically activated when users mention phishing-related topics

## Usage

Simply describe the suspicious email or paste its content in your Kiro chat. The skill triggers when you mention:

- "帮我看看这封邮件"
- "这个链接安全吗"
- "收到奇怪的邮件"
- "客户发来的邮件不太对"
- "收款账号变更"
- Any phishing/suspicious email related topics

## File Structure

```
phishing-email-analyzer/
├── README.md
├── LICENSE
├── SKILL.md                              # Main skill definition
└── references/
    ├── common-phishing-patterns.md       # Common phishing patterns & real case templates
    └── emergency-response.md             # Emergency response procedures
```

## Output Format

The skill outputs a structured security audit report including:

- Risk verdict and score (0-100)
- Threat classification tags
- List of suspicious indicators
- Plain-language risk explanation
- Link/attachment analysis results
- Actionable next steps
- Tips for future self-identification

## Language

This skill outputs analysis in **Chinese (中文)**, as it's designed for Chinese-speaking sales teams.

## License

[MIT](LICENSE)

## Author

Aliex Zeng
