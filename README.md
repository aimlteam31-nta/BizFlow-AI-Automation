Live Demo Link: https://aiml-erpai-systems.netlify.app/

Video Presentation: https://drive.google.com/drive/folders/16dxuf0ez4-25lp2r8jPVNEhjsWBkzts0?usp=sharing


This demo script is structured to show the technical depth and business impact of **BizFlow AI**, specifically focusing on the live implementation for "SK Natural." It follows a logical flow from onboarding to autonomous operations.

---

# Project Demo: BizFlow AI — The Agentic ERP
Presenter: AIML Team 31  
Case Study: SK Natural (E-commerce Herbal Store)

---

## 1. Executive Summary
BizFlow AI is an **Agentic ERP system** designed to act as a 24/7 Digital Employee. Unlike traditional ERPs that are passive databases, BizFlow is **proactive**. It doesn't just store data; it analyzes intent, predicts stock shortages, and communicates directly with the owner and suppliers via AI-driven channels.

---

## 2. Phase 1: Seamless Onboarding & Synchronization
The journey starts with the **Business Registration Workflow**.
* **The Process:** By simply providing the WooCommerce API keys and business details (Store Name, Website, Telegram ID), the system triggers an n8n orchestration.
* **Initial Sync:** For SK Natural, the system instantly fetched **1,400+ historical orders and products**, creating a centralized database in **Supabase**.
* **Instant Confirmation:** The owner receives an automated onboarding email and a Telegram welcome message, confirming the "Digital Twin" of their business is live.

---

## 3. Phase 2: Lead Conversion & Intent Intelligence
BizFlow transforms a standard website into a smart sales engine.
* **The Website Chatbot:** Integrated with **RAG (Retrieval-Augmented Generation)**, the bot answers product queries using live database data.
* **Intent Scoring:** Every interaction is analyzed. n8n scores leads as **Hot, Warm, or Cold**. 
* **The Sales "Hook":** When a user asks about pricing, the bot intelligently offers a bulk discount and requests a WhatsApp number, instantly redirecting the lead to the owner's WhatsApp to close the deal.
* **Real-time Awareness:** Every search query and high-intent lead triggers a **Telegram Alert**, ensuring the owner knows exactly what customers are looking for at any given second.

---

## 4. Phase 3: Autonomous Operations (The Telegram Bot)
The Telegram bot serves as the **"Business in Your Pocket."**
* **Proactive Reporting:** Every morning at **9:00 AM**, the system sends a **Scheduled Daily Sales Report**, summarizing revenue and performance to help the owner plan their day.
* **Hourly Inventory Vigilance:** The system checks stock levels every hour. 
* **Autonomous Action:** If a product is low, the bot doesn't just alert the owner; it asks for permission to **automatically email the supplier** for a restock, closing the loop of the supply chain without human data entry.
* **Natural Language Interaction:** The owner can query the system via **Text or Voice** (e.g., "What were yesterday's sales?") to get instant AI-generated summaries.

---

## 5. Phase 4: Data Visualization & Forecasting (The Dashboard)
For high-level strategy, BizFlow provides a sophisticated **React-based Dashboard**.
* **Simplified Login:** Access is granted via a unique **Business ID**.
* **Intelligent Metrics:** It displays KPI cards and interactive graphs for **Sales, Orders, and Leads**.
* **Trend Selection:** Data can be filtered by **7, 30, and 90-day ranges** to identify seasonal patterns.
* **AI Forecasting:** The dashboard doesn't just show what happened; it uses historical trends to **forecast future performance**, allowing for data-driven inventory and marketing decisions.

---

## 6. Technical Architecture & Impact
* **Stack:** n8n (Orchestration), Supabase (Vector & Relational DB), OpenAI/Claude (Intelligence), Telegram API (Interface), React (Frontend).
* **The Benefit:**
    1.  **Reduces Overhead:** Replaces the need for manual data entry and basic customer support.
    2.  **Eliminates Stock-outs:** Proactive supplier alerts ensure no sales are lost.
    3.  **High Conversion:** Intent scoring ensures the owner spends time only on "Hot" leads.

---

**Conclusion:** BizFlow AI is not just a tool; it is an evolving **Agentic System** that grows with the business, shifting the owner’s role from "Data Operator" to "Strategic Visionary."
