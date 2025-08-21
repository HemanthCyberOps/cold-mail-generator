# 📧 Cold Mail Generator

Generate tailored cold emails for services companies using **Groq**, **LangChain**, and **Streamlit**. Input a company careers page URL → extract job listings → craft concise, value-first outreach emails enriched with **relevant portfolio links** retrieved from a **vector database**.

---

## 🌍 Real‑World Example
1) Scenario (README copy)

Nike (global sportswear brand) is hiring a Senior Backend Engineer to accelerate a critical checkout migration and reduce cart abandonment. TCS, a service-based software engineering firm, has engineers experienced in payments and checkout reliability. The SDR at TCS pastes Nike’s careers URL into the app, selects the Senior Backend role, and generates a personalized outreach email that:

Mirrors Nike’s job language and priorities,

Highlights two relevant case studies (e.g., “reduced checkout latency by 35%”),

Proposes a concise 20-minute discovery call this week.

2) Sample cold email (copy-paste ready)

Subject: Helping Nike speed up checkout — 20-minute call?

Hi [Hiring Manager / Talent Team],

I’m reaching out from TCS — we help large retailers accelerate checkout migrations while improving reliability and conversion. I saw the Senior Backend Engineer (Payments) role on Nike’s careers page and noticed the focus on payment throughput and latency reduction.

Recently, our team delivered a checkout migration for a major retailer where we:

Reduced checkout latency by 35%, improving conversion during peak traffic, and

Implemented a fault-tolerant payments service that handled 3× expected peak load without downtime.

If helpful, I can share two short case studies showing the architecture and measurable outcomes. Would you be open to a 20-minute discovery call this week to see whether we can provide an engineer who’s already done this work?

Best regards,MohanBusiness Development, TCS[manager@tcs.com] | +91-XXXXXXXXXX



---

## 🏗️ Architecture

![Architecture](imgs/architecture.png)

---

## ⚙️ Setup

1. Create a Groq API key: [https://console.groq.com/keys](https://console.groq.com/keys)
2. Create `app/.env`:

```env
GROQ_API_KEY=your_key_here
# Optional
VECTOR_DB_PATH=./data/index
PORTFOLIO_JSON=./data/portfolio.json
MODEL_NAME=llama3-groq-70b-8192
TOP_K=4
TEMPERATURE=0.4
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Run the app:

```bash
streamlit run app/main.py
```

---

## 🚀 How It Works

1. **Scrape** the careers URL and parse job postings (title, location, description).
2. **Embed & Retrieve**: create embeddings for the JD and fetch top‑K matching portfolio items from the vector store.
3. **Generate**: assemble a short, value‑driven email via Groq + prompt template.
4. **Review & Copy**: preview the email, tweak if needed, and copy/send.

---

## ✨ Features

* One‑click JD extraction from careers pages
* Context‑aware email generation (Groq + LangChain)
* Vector search over your portfolio/case studies
* Streamlit UI with copy‑to‑clipboard
* Simple env‑based configuration

---

## 🧰 Tech Stack

* **UI**: Streamlit
* **LLM**: Groq
* **Orchestration**: LangChain
* **Vector DB**: FAISS or Chroma
* **Scraping**: requests + BeautifulSoup (or Playwright for dynamic sites)

---

---

## 📨 Prompt Template (example)

```
You are an expert BD email writer. Draft a concise, value-first cold email to <company> about <job_title>.
Tone: professional, friendly, 120–160 words. Include 2–3 relevant portfolio links:
{{ portfolio_items }}
Job description summary:
{{ jd_summary }}
End with a clear CTA for a 20‑minute discovery call this week.
```

---

## 🛠️ Troubleshooting

* **No jobs found** → Page is dynamic: use Playwright for rendering.
* **Empty retrieval** → Build embeddings; check `VECTOR_DB_PATH` and `PORTFOLIO_JSON`.
* **Low email quality** → Tune `TEMPERATURE`, refine prompt, add better tags to portfolio.

---

## 🗺️ Roadmap

* Batch mode for multiple companies
* Gmail/Outlook send integration
* Open/click tracking dashboard
* JD deduplication & seniority tagging

---
