# CMPE 297 – ADK Multimodal Agents (Gemini + Google ADK)

This repo contains five end-to-end agents built with **Google ADK** and **Gemini**, each implemented as a Google Colab notebook:

1. Deep research lead generation agent
2. Advanced tool agent using a Gemini CLI-style tool
3. Bug assistance agent
4. Code review assistant
5. E-commerce shopping agent

All agents run entirely in **Google Colab** and use Gemini via `google-genai` and ADK via `google-adk`.

> 📺 **Demo video (all agents)**: [LINK]()

---

## How to Run Any Notebook

1. Open the Colab link for the agent you want (below).
2. Set your `GEMINI_API_KEY` at the top of the notebook (replace the placeholder string).
3. Run all cells in order.
4. Use the final “helper” cell(s) to interact with the agent (e.g., ask for leads, run code reviews, ask e-commerce questions).

---

## 1. Deep Research Lead Generation Agent

**Goal:**
Build a deep research agent that:

* Uses a web search tool to find B2B SaaS leads.
* Synthesizes structured lead objects (company, website, segment, why_good_lead).
* Saves leads into `leads.csv` for later analysis.

**Key pieces:**

* `web_search` tool using DuckDuckGo (`ddgs`).
* `save_leads` tool that appends leads to `leads.csv`.
* `deep_research_agent` (LlmAgent) orchestrating the tools via ADK.
* `run_lead_query(...)` helper to trigger end-to-end lead generation.

**Colab notebook:**

* Notebook path: `deep-research-leads/notebook.ipynb`
* Open in Colab: [Deep Research Lead Generation Agent](https://colab.research.google.com/drive/1EJJ3Qp1RV1rxid6QMvcVWg1P0tUuzgpF?usp=sharing)

---

## 2. Gemini CLI Tool Agent

**Goal:**
Show an **advanced tool agent** that calls a separate Gemini CLI-style script inside an ADK pipeline.

**Key pieces:**

* `gemini_cli_tool.py`: small script that reads text, calls Gemini, prints output.
* `run_gemini_cli(...)` tool: wraps the script using `subprocess`.
* `cli_agent` (LlmAgent): decides when to call the CLI tool and summarizes its output.
* `run_cli_agent(...)` helper: send prompts through the agent.

**Colab notebook:**

* Notebook path: `gemini-cli-tool-agent/notebook.ipynb`
* Open in Colab: [Gemini CLI Tool Agent](https://colab.research.google.com/drive/1aMqQyJaJ5vCEIzG07VKeImQFLYtK-ZBx?usp=sharing)

---

## 3. Bug Assistant Agent

**Goal:**
Build a bug-assistance agent that helps diagnose and fix code issues.

**Key pieces:**

* `analyze_bug(code, error_message)` tool:

  * Sends code + error to Gemini.
  * Returns root cause + suggested fix.
* `bug_agent` (LlmAgent): calls `analyze_bug` as needed to answer user bug reports.
* `ask_bug_agent(...)` helper: takes code + error and prints the agent’s explanation.

**Colab notebook:**

* Notebook path: `mcp-bug-assistant/notebook.ipynb`
* Open in Colab: [Bug Assistant Agent](https://colab.research.google.com/drive/194Yvj85hD4659Fg1pb4uQxnvkTTbZZpJ?usp=sharing)

---

## 4. Code Review Assistant

**Goal:**
Implement a production-style **code review assistant** that provides structured feedback and improved snippets.

**Key pieces:**

* `review_code(code, language, focus)` tool:

  * Asks Gemini for a review focused on readability, bugs, security, etc.
  * Returns summary, issues, and suggestions with example patches.
* `code_review_agent` (LlmAgent): orchestrates calls to `review_code`.
* `ask_code_reviewer(...)` helper: sends code plus focus area and prints review.

**Colab notebook:**

* Notebook path: `code-review-assistant/notebook.ipynb`
* Open in Colab: [Code Review Assistant](https://colab.research.google.com/drive/1wjdcOjm5pqflCzviYdc_Scktjt5x0Rur?usp=sharing)

---

## 5. E-Commerce Shopping Agent

**Goal:**
Build a small “production-style” e-commerce agent grounded in a real product catalog.

**Key pieces:**

* SQLite DB `ecommerce.db` with a `products` table (SKU, name, category, price, currency, description).
* `search_products(query)` tool: SQL `LIKE` search over the product catalog.
* `ecom_agent` (LlmAgent):

  * Uses `search_products` to find matching products.
  * Recommends 1–3 items with SKU, price, and explanation.
* `ask_ecom_agent(...)` helper: natural language shopping queries (e.g., “running shoes under $120”).

**Colab notebook:**

* Notebook path: `ecommerce-agent/notebook.ipynb`
* Open in Colab: [E-Commerce Shopping Agent](https://colab.research.google.com/drive/1YC4fm1T9JIQu5bpBY2V-T-trZXKgvN3-?usp=sharing)

---

## Repository Structure (Suggested)

```text
.
├── README.md
├── deep-research-leads/
│   └── notebook.ipynb
├── gemini-cli-tool-agent/
│   └── notebook.ipynb
├── mcp-bug-assistant/
│   └── notebook.ipynb
├── code-review-assistant/
│   └── notebook.ipynb
└── ecommerce-agent/
    └── notebook.ipynb
```
