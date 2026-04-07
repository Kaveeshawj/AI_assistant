# 🏦 FIN.TRACE — Payment Intelligence Platform

> **AI-powered code analyzer and fintech intelligence suite for payment switch engineers.**  
> Built for ISO 8583 · ISO 20022 · SWIFT · PCI-DSS v4 · Java / Spring ecosystems.

[![Live Demo](https://img.shields.io/badge/Live-Demo-teal?style=flat-square)](https://kaveeshawj.github.io/AI_assistant/index.html)
[![Stack](https://img.shields.io/badge/Stack-HTML%20%2F%20JS%20%2F%20OpenRouter-navy?style=flat-square)]()
[![Domain](https://img.shields.io/badge/Domain-Fintech%20%2F%20Payments-gold?style=flat-square)]()

---

## 📌 Overview

**FIN.TRACE** is a browser-based AI platform purpose-built for backend payment switch engineers. It combines a **static code analyzer** with a suite of **RAG-inspired AI intelligence tools** — all requiring zero backend infrastructure. Just open the HTML file, plug in an OpenRouter API key, and get expert-level insights on your payment code, transactions, logs, and protocol messages.

Built during an internship at **Epic Lanka (Pvt) Ltd** — Sri Lanka's leading payment technology company — this tool directly addresses the day-to-day debugging and compliance challenges in a real-world card switch environment.

---

## ✨ Features

### ⚡ Tab 1 — Switch Code Analyzer

Paste Java/Spring payment switch code and get a structured audit report in seconds.

| Mode | What It Checks |
|---|---|
| **Full Switch Audit** | All categories combined |
| **ISO 8583** | MTI validity, mandatory fields per message type (0100/0110/0200/0400), bitmap, STAN/RRN, MAC (F64/F128), response codes (F39) |
| **ISO 20022** | pacs.008/009/002, pain.001, camt.053, BIC/IBAN format, XXE injection, BigDecimal usage |
| **SWIFT** | MT103/MT202/MT940 mandatory fields, BIC country code validation, UETR/gpi, AML hooks |
| **PCI-DSS v4** | Req 3.3.1 (CVV storage), 3.4.1 (PAN masking), 4.2.1 (cleartext HTTP), 6.3.1 (SQL injection), 6.3.3 (hardcoded keys), 8.3.6 (MD5/SHA1/DES banned), PIN block ISO 9564 |
| **Txn Flow** | Reversal on timeout, idempotency, duplicate detection, response code propagation |
| **TPS / Perf** | `synchronized` hot-path bottlenecks, N+1 DB queries, `DriverManager` vs HikariCP, Caffeine cache, `RestTemplate` timeouts, Resilience4j circuit breakers |

**Output includes:**
- Compliance score (0–100) with per-standard breakdown (PCI-DSS, ISO 8583, ISO 20022, SWIFT, TPS-Ready)
- Categorized issues: Critical / Bug / Warning / Info with line numbers
- Spec references (e.g., `PCI-DSS Req 3.3.1`, `ISO 8583 F37`)
- One-click **Apply Fix** — corrected code auto-applied to the editor
- **Export to JSON** or **Copy plain-text report**

---

### 🧠 Tab 2 — FinTrace AI (6 Intelligence Tools)

#### 🧾 Transaction Explainer
Enter raw transaction fields (TXN ID, Amount, Type, ISO 8583 Response Code F39, Channel, Merchant) and get a plain-English explanation tailored to:
- **Developer** — technical ISO 8583 context
- **Customer Support** — jargon-free, actionable
- **End Customer** — empathetic, simple

Supports quick-fill presets: Insufficient Balance, Issuer Timeout, Expired Card, Suspected Fraud.

#### 🚨 Fraud / Risk Analyzer
Paste transaction context JSON and get a structured risk report:
- Risk Level: Critical / High / Medium / Low
- Named fraud typologies (velocity spike, geographic anomaly, new beneficiary attack)
- Concrete rule suggestion for the switch
- Frameworks: ISO 8583 / PCI-DSS indicators / General fintech

#### 🔌 API Error Debugger
Paste Spring Boot exceptions or stack traces:
- Root cause identification
- Payment impact assessment (was a reversal needed?)
- Java/Spring fix with code example
- Prevention strategy

Presets: NullPointerException, DB Connection Error, Gateway Timeout, ISO Parse Error.

#### 📊 Log Analyzer
Feed raw Spring Boot, jPOS, HikariCP, or GC logs and get:
- CRITICAL EVENTS list with timestamps
- Systemic patterns
- Affected transaction list
- Root cause hypothesis
- Immediate on-call action + monitoring recommendations

#### 📋 ISO 8583 Reference
Natural language Q&A over the ISO 8583:2003 standard + EMV 4.3:
- Field definitions (format, length, LLVAR/LLLVAR, BCD/ASCII/Binary)
- Response code tables (F39)
- MTI mandatory field lists
- jPOS Java examples

#### 🌐 SWIFT Decoder
Paste MT103 / MT202 / MT940 messages and get:
- Header block analysis ({1}, {2}, {3})
- Field-by-field decoding with SWIFT Standards 2024
- Transaction plain-English summary
- Compliance notes: missing mandatory fields, gpi UETR, AML indicators

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Vanilla HTML5, CSS3, JavaScript (ES2020+) |
| **Styling** | CSS Custom Properties (design tokens), Tailwind CSS (CDN utility classes) |
| **Fonts** | IBM Plex Sans + IBM Plex Mono (Google Fonts) |
| **AI Runtime** | [OpenRouter API](https://openrouter.ai) — unified gateway to multiple LLMs |
| **Architecture** | Single-file SPA, zero build step, zero backend |

### Supported Models

| Tier | Models |
|---|---|
| **Free** | `step-3.5-flash`, `nemotron-3-120b`, `gemma-3-27b`, `llama-4-scout`, `deepseek-r1-zero`, `qwen3-30b` |
| **Premium** | `gpt-4o`, `claude-3.5-sonnet`, `gemini-2.5-pro`, `deepseek-r1` |

---

## 🚀 Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/Kaveeshawj/AI_assistant.git
```

### 2. Open in browser

```bash
# No build required — just open the file
open index.html
# or serve with any static server:
npx serve .
```

### 3. Add your API key

Get a free key at [openrouter.ai](https://openrouter.ai) → paste it into the 🔑 field in the toolbar.

### 4. Select a model

Pick any free model from the dropdown (e.g., `step-3.5-flash · free`) and start analyzing.

---

The entire platform — HTML, CSS (1,800+ lines of design system), JavaScript (700+ lines of logic), and 6 AI tool prompt templates — lives in a single, self-contained `index.html`.

---

## 🎯 Sample Scenarios

### Scenario 1 — PCI-DSS Audit
Paste a `CardService.java` that stores CVV and logs PANs → get Critical violations flagged with exact requirement references (Req 3.3.1, 3.4.1, 8.3.6) and a corrected code snippet.

### Scenario 2 — Failed Transaction
Fill in: Type=TRANSFER, Status=FAILED, RC=51, Amount=LKR 25,000 → get a developer explanation referencing ISO 8583 F39=51 (Insufficient Funds) and a customer-friendly version in the same click.

### Scenario 3 — SWIFT Decode
Paste an MT103 message → get every field explained: `:20:` (Transaction Reference), `:32A:` (Value Date + Currency + Amount), `:50A:` (Ordering Institution BIC), `:71A:` (Charges — SHA/OUR/BEN).

### Scenario 4 — Log Triage
Paste a Spring Boot log with `HikariPool-1 - Connection is not available` → get root cause (pool exhaustion), affected STANs, and recommended `hikari.maximum-pool-size` fix.

---

## 🏗️ Architecture

```
User Input
    │
    ├── Code Analyzer → builds expert Java/fintech prompt → OpenRouter API
    │                                                            │
    └── FinTrace Tools → RAG-style domain context injection ────┘
                                                                │
                                              Structured JSON / Free-text
                                                                │
                                               Rendered UI (score ring,
                                               compliance bars, issue cards,
                                               AI response cards)
```

The "RAG" in this project is **prompt-level retrieval** — each tool injects a curated domain knowledge context (ISO 8583 field tables, PCI-DSS requirement numbers, SWIFT field definitions) into the prompt before sending to the LLM, simulating retrieval-augmented generation without a vector database.

---

## 🌐 Domain Knowledge Embedded

- **ISO 8583:2003** — MTI definitions, all mandatory fields per message type, bitmap mechanics, F39 response code table, F52 (PIN), F55 (EMV), F64/F128 (MAC)
- **ISO 20022** — pacs.008/009/002, pain.001, camt.053 schema rules, IBAN MOD97, BIC format
- **SWIFT** — MT103/MT202/MT940 field sets, gpi/UETR, AML indicators, SWIFT Standards 2024
- **PCI-DSS v4.0** — Requirements 3.3.1, 3.4.1, 4.2.1, 6.3.1, 6.3.3, 8.3.6
- **EMV 4.3** — Tag definitions for Field 55
- **jPOS** — `ISOMsg`, `ISOBasePackager`, `ISOException` patterns
- **HikariCP** — Pool configuration best practices
- **Resilience4j** — Circuit breaker patterns for issuer timeout scenarios

---

## 🔒 Privacy & Security

- **No data leaves your browser** except to the OpenRouter API endpoint you configure.
- **No backend, no database, no analytics.**
- API key is stored only in the browser session (input field) — never persisted.
- The tool is designed for **non-production / development code review** — do not paste live PAN data.

---

## 🤝 Contributing

Pull requests welcome. Areas for contribution:

- Additional ISO 8583 sample snippets
- ISO 20022 pacs.009 (FI-to-FI credit transfer) support
- Dark mode toggle
- Offline model support (Ollama integration)
- Export to PDF report

---

## 👨‍💻 Author

**Kaveesha Wijeweera**  
[LinkedIn](https://www.linkedin.com/in/kaveewijeweera/) · [GitHub](https://github.com/Kaveeshawj)

---

*Built with deep respect for the engineers who keep payment systems running 24/7. 🙏*
