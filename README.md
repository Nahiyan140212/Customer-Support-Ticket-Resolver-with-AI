# Streamlit Customer Support Ticket System

A lightweight, end‑to‑end customer‑support platform built with **Streamlit** and powered by **LLM‑based replies**.  Two micro‑frontends work together:

* **`register_ticket.py`** – public‑facing form where customers open a new ticket.
* **`main.py`** – internal dashboard for support agents to **look up**, **analyse**, and **reply**.  Replies are drafted by an AI model and can be edited before sending.

All tickets, agent notes, and final replies are automatically persisted to **Google Sheets** for a single source of truth.

---

## Key Features

| Capability | Description |
|------------|-------------|
| Ticket Registration | Simple Streamlit form collects name, email, category, priority & message. |
| Agent Dashboard | Search / filter tickets, view full history, and trigger AI analysis. |
| AI‑Assisted Replies | Calls OpenAI (or your chosen LLM) to draft contextual responses. |
| Google Sheets Log | Each interaction is appended to a sheet, enabling analytics & auditing. |
| Stateless Deployment | No dedicated DB needed—ideal for quick proofs‑of‑concept. |

---

> **Already wrote a detailed walkthrough?** Drop it into `docs/STEP_BY_STEP_GUIDE.md` and reference it from the sections below.

---

## Quick Start

1. **Clone & install**
   ```bash
   git clone  https://github.com/Nahiyan140212/Customer-Support-Ticket-Resolver-with-AI.git
   cd Customer-Support-Ticket-Resolver-with-AI
   pip install -r requirements.txt
   ```
2. **Configure secrets** – create `.streamlit/secrets.toml`:
   ```toml
   [google]
   service_account = "{"type":"service_account",...}"

   [openai]
   api_key = "sk‑..."
   ```
3. **Launch endpoints** (in separate terminals):
   ```bash
   streamlit run register_ticket.py  # Customer form – port 8501
   streamlit run main.py             # Agent dashboard – port 8502
   ```
4. **Open browser**
   * `http://localhost:8501` – create a ticket
   * `http://localhost:8502` – manage & reply

Full environment setup is covered in **docs/STEP_BY_STEP_GUIDE.md**.

---

## Google Sheets Integration

The helper `sheets_connecter.py` (imported by both endpoints) uses *gspread* to:

* `append_ticket()` – write new submissions.
* `append_reply()` – log AI draft & final response.
* `list_tickets()` – fetch all rows for dashboard display.

> **Tip:** Share the sheet with your service‑account email and turn on *Anyone with the link → Viewer* if you need anonymous read‑only embeds.

---

## AI Reply Flow

```mermaid
graph TD
    A[Agent clicks "Analyze & Reply"] -->|sends prompt| B(OpenAI API)
    B --> C{Draft reply}
    C -->|approve / edit| D[Send email]
    D --> E[Log reply to Google Sheets]
```

## Deployment

| Target | Notes |
|--------|-------|
| **Streamlit Community Cloud** | Easiest—push to a public repo and set Secrets tab. |
| **AWS EC2 / Lightsail** | `tmux` two Streamlit processes or use Nginx with subpaths. |
| **Docker** | See `docker-compose.yml` (experimental). |

---

## Roadmap

- ☐ OAuth login for agents
- ☐ File‑attachment support
- ☐ SLA metrics & dashboards in Looker Studio
- ☐ Slash‑command integration for Slack

---

## Contributing

1. Fork the repo & create a branch.
2. Commit descriptive messages.
3. Open a Pull Request—one of the maintainers will review.

---

## License

Distributed under the MIT License. See `LICENSE` for details.

