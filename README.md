# 🤖 SCM Assistant Bot

A RAG-based Supply Chain Management chatbot built using Flowise AI. It answers supplier and policy questions using retrieval-augmented generation over a supplier performance dataset and a governance policy document.

---

## 🔗 Public Chatbot URL

👉 [https://cloud.flowiseai.com/chatbot/78a9e2ae-309e-4c9a-868f-08bf9a28f164](https://cloud.flowiseai.com/chatbot/78a9e2ae-309e-4c9a-868f-08bf9a28f164)

---

## 🧠 LLM and Embeddings Used

| Component | Provider | Model |
|---|---|---|
| Chat Model | Cohere | `command-a-03-2025` |
| Embeddings | Cohere | `embed-english-v3.0` |
| Vector Store | Pinecone | Free Tier (Dense, 1024 dimensions) |
| Framework | Flowise AI | Cloud |

---


## ⚙️ Chunk Configurations Tested

| Configuration | Chunk Size | Overlap | Result |
|---|---|---|---|
| Config 1 | 500 | 50 | More chunks, precise but loses cross-row context |
| Config 2 | 1500 | 200 | Fewer chunks, better context retention for policy sections |

**Selected Configuration:** Config 2 (Chunk Size: 1500, Overlap: 200)

**Reason:** Larger chunks kept policy sections like §3.2, §4.2, and §9 intact and preserved supplier data context across rows, resulting in more complete answers.

---

## ❓ Sample Q&A (Verbatim Chatbot Answers)

### Q1: Which Tier-3 suppliers have an active disruption flag, and what response level applies per policy?

> Based on the provided context, there is no specific information about which Tier-3 suppliers have an active disruption flag. However, the policy outlines that if a Tier-3 supplier has an active disruption flag, the response level depends on the risk level and the nature of the disruption.
>
> For Tier-3 suppliers (High Risk), any disruption flag would typically trigger a **Level 3 — Activate** response. Additionally, certain disruption categories (export control restrictions, active labour strikes, regulatory enforcement actions, and port closure events exceeding 72 hours) mandate a Level 3 response regardless of the supplier's risk level.

---

### Q2: Which suppliers qualify for the annual Volume Rebate Program and how many are there?

> According to the provided context, Tier-1 suppliers qualify for the annual Volume Rebate Program if they meet the following criteria for a full calendar year:
> - OTD (On-Time Delivery) at or above 93.0%
> - Defect Rate below 0.5%
> - Sustainability Score at or above 85
>
> Qualifying suppliers receive an annual volume rebate of 2.5% of their total annual invoice value.
>
> However, the context does not specify the exact number of Tier-1 suppliers that meet these criteria. Therefore, I cannot provide a count of how many suppliers qualify.

---

### Q3: Which region has the highest total PO value, and does it breach the concentration limit?

> The context does not provide specific data on the total PO (Purchase Order) value by region. However, it does outline the Concentration Risk Rule:
> - No single region (APAC, EMEA, LATAM, NA) may account for more than **45%** of total annual procurement spend.
> - No single country may represent more than **25%** of spend.
>
> Without the actual PO value data, I cannot determine which region has the highest total PO value or if it breaches the concentration limit.

---

### Q4: Which suppliers are on Supplier Watch List (SWL) status and what does it restrict?

> Suppliers are placed on Supplier Watch List (SWL) status if they meet any of the following criteria:
> - Compliance Score below 60 at any audit, regardless of tier designation.
> - Audit Overdue status:
>   - Tier-1: Last Audit Date > 14 months ago
>   - Tier-2: Last Audit Date > 7 months ago
>   - Tier-3: Last Audit Date > 4 months ago
>
> **Restrictions for SWL status:** New PO issuance is limited to 20% of prior quarter volume.
>
> The context does not provide a list of specific suppliers currently on SWL status.

---

### Q5: Which product category has the highest average defect rate and does it exceed the Tier-2 limit?

> The context does not provide information on defect rates by product category. It only specifies the maximum permissible defect rates by tier:
> - Tier-1: 0.99%
> - Tier-2: 2.50%
> - Tier-3: 4.00%
>
> Without data on average defect rates by product category, I cannot determine which category has the highest rate or if it exceeds the Tier-2 limit.

---

## 📸 Screenshots

All setup screenshots are available in the [`/screenshots`](./screenshots) folder, including:
- Document Store configuration
- Chunk config 1 (500/50) upsert result
- Chunk config 2 (1500/200) upsert result
- Chatflow canvas
- Public chatbot share settings
- Sample Q&A results

---

## 🔧 What I Would Improve

- **Better CSV handling** — Model is not able to retrive data from csv. Convert raw CSV to structured text format per supplier for improved RAG retrieval accuracy
- **Paid embedding model** — Use OpenAI `text-embedding-3-large` for higher dimensional embeddings and better semantic search
- **Add conversation memory** — Enable Buffer Memory node so the chatbot retains conversation history across turns
- **Hybrid search** — Combine dense + sparse vector search for better retrieval of both numeric and textual supplier data
- **Custom system prompt** — Add a prompt template to guide the model to always reference both the CSV data and policy document together

---

