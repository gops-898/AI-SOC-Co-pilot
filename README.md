# 🛡️ AI SOC Copilot

An AI-powered Security Operations Center assistant that analyzes security log files, extracts indicators of compromise, detects threats using rule-based detection, maps findings to MITRE ATT&CK, and provides an intelligent chat interface powered by Mistral AI.

---

## 📌 Features

- **File Upload** — supports CSV and Excel security logs
- **IOC Extraction** — automatically finds IP addresses, domains, URLs, file hashes, and email addresses
- **Threat Detection** — rule-based engine detects encoded PowerShell, Mimikatz, ransomware indicators, brute force patterns, credential dumping, and more
- **Risk Scoring** — calculates a 0–100 risk score with severity level (LOW / MEDIUM / HIGH / CRITICAL)
- **MITRE ATT&CK Mapping** — maps every detection to its ATT&CK tactic and technique
- **AI Investigation Report** — Mistral AI explains findings in plain English, strictly based on detected evidence
- **SOC Copilot Chat** — ask any security question about the analyzed file and get a detailed, context-aware response

---

## 🏗️ How It Works

```
Upload File → Parse → Extract IOCs → Detect Threats → Score Risk → AI Report → Chat
```

The system uses a hybrid approach: rule-based detection finds the evidence (deterministic, auditable), and the LLM only explains that evidence — it never invents threats.

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| UI | Streamlit |
| LLM | Mistral AI (ministral-8b-latest) |
| LLM Framework | LangChain, langchain-mistralai |
| Agent Workflow | LangGraph |
| RAG | LangChain + ChromaDB |
| Data Processing | Pandas |
| IOC Extraction | Regex-based custom extractor |
| Knowledge Base | MITRE ATT&CK, IR Playbooks, Threat Reports |

---

## 📁 Project Structure

```
AI SOC Copilot/
├── app.py                        # Streamlit UI
├── report_generator.py
├── workflow_langgraph.py
├── requirements.txt
│
├── agents/
│   ├── investigation_agent.py    # Mistral chat + report generation
│   ├── investigation_llm.py
│   ├── mitre_agent.py
│   ├── severity_agent.py
│   ├── threat_intel_agent.py
│   └── recommendation_agent.py
│
├── workflow/
│   └── soc_workflow.py           # Core orchestration
│
├── parsers/
│   ├── parser_router.py
│   ├── csv_parser.py
│   └── excel_parser.py
│
├── ioc/
│   └── extractor.py              # IP, domain, URL, hash, email extraction
│
├── detections/
│   └── detection_engine.py       # Rule-based threat signatures
│
├── risk/
│   └── scorer.py
│
├── rag/
│   ├── ingest.py                 # Ingest knowledge base into ChromaDB
│   ├── retriever.py
│   └── vectorstore.py
│
└── knowledge_base/
    ├── mitre_attack.md
    ├── incident_response.md
    └── threat_reports.md
```

---

## 🚀 Setup

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/ai-soc-copilot.git
cd ai-soc-copilot
```

### 2. Create a virtual environment
```bash
python -m venv venv
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Add your API key
Create a `.env` file in the root folder:
```
MISTRAL_API_KEY=your_mistral_api_key_here
```
Get a free API key at [console.mistral.ai](https://console.mistral.ai)

### 5. Build the knowledge base
```bash
python rag/ingest.py
```
This creates the `vector_db/` ChromaDB files locally (not stored in GitHub).

### 6. Run the app
```bash
streamlit run app.py
```

---

## ⚠️ Notes

- `vector_db/` is excluded from this repo — regenerate it locally by running `python rag/ingest.py`
- Never commit your `.env` file — your API key lives only on your machine
- Test log files (`.csv`, `.xlsx`) are also excluded — see the sample files section below for testing

---

## 🧪 Testing

Upload any of these file types to test the analyzer:

| Scenario | Expected Result |
|---|---|
| CSV with PowerShell commands | HIGH/CRITICAL risk, Execution technique detected |
| CSV with repeated failed logins from one IP | MEDIUM/HIGH risk, Brute Force detected |
| Excel with mimikatz in command lines | CRITICAL risk, Credential Access detected |
| Normal activity log (no threats) | LOW risk, no findings |

---

## 📄 License

© 2026 [Gopal Reddy Bujala]. All rights reserved.

---

## 👤 Gopal Reddy Bujala

**[Your Name]**  
[LinkedIn](https://linkedin.com/in/yourprofile) | [GitHub](https://github.com/yourusername)
