Live Demo Link: https://bizflowaierp.netlify.app/

Video Presentation: https://drive.google.com/file/d/1oM5utFkX_oHx7HfgsR6v_l9drqdiFYH2/view?usp=sharing


# BizFlow AI — Intelligent ERP for Pakistani SMBs

> AI-powered business automation platform integrating WooCommerce, Supabase, n8n, OpenAI, and Telegram for small and medium businesses.

---

## Overview

BizFlow AI is a multi-tenant ERP and business automation platform that helps Pakistani SMBs automate their sales tracking, inventory management, CRM lead scoring, and customer support — all through a real-time AI-powered dashboard and Telegram bot interface.

---

## System Architecture

```
Customer (Website Chatbot / Telegram)
        ↓
   n8n Workflows (Automation Layer)
        ↓
  OpenAI GPT-4o / Whisper (AI Layer)
        ↓
  Supabase PostgreSQL (Database Layer)
        ↓
  WooCommerce REST API (eCommerce Layer)
        ↓
  BizFlow Dashboard (Frontend — Netlify)
```

---

## Core Features

| Feature | Description |
|---|---|
| **AI Chatbot** | Product queries, prices, availability in Urdu/English via website widget |
| **Sales Analytics** | Revenue trends, top products, best days — query in natural language |
| **CRM Lead Scoring** | Auto-scores chatbot visitors as Hot/Warm/Cold leads |
| **Inventory Alerts** | Low stock detection with automated supplier email notifications |
| **Daily Reports** | Automated sales summaries via Telegram every morning |
| **Customer Intelligence** | Search pattern analysis, demand gaps, revenue opportunities |
| **Automation ROI** | Tracks AI tasks, hours saved, PKR value generated |

---

## n8n Workflows

### WF1 — Business Registration
Registers new businesses, syncs WooCommerce products/orders to Supabase.

**Trigger:** Webhook `POST /business-registration`

**Flow:** Validate → WooCommerce Auth → Sync Products → Sync Orders → Save Business Profile → Telegram Confirmation

---

### WF2 — Customer Chatbot (v6 MERGED)
Handles product queries from website chatbot widget with AI responses.

**Trigger:** Webhook `POST /chatbot-query`

**Flow:** Validate & Classify Intent → Build Supabase Query (AND + OR fallback) → Fetch Products → Format Context → OpenAI GPT-4o-mini → Score Lead → Log Search + Save CRM Lead → Return Answer

**Key Features:**
- Intent detection: `sale`, `price`, `stock`, `category`, `search`
- AND search with brand word filtering (Ashraf, Hamdard, Ajmal etc.)
- Automatic OR fallback if AND returns empty
- Lead scoring: price inquiry = Hot, stock check = Warm
- Bilingual: Urdu ↔ English ↔ Mix

---

### WF3 — Sales Analytics
Answers natural language sales queries for business owners.

**Trigger:** Webhook `POST /sales-analytics`

**Flow:** Classify Date Range → Build Supabase Query → Fetch Orders → Calculate Analytics → GPT-4o Insight → Log → Return Answer

**Supported Queries:**
- `today`, `yesterday`, `this week`, `last week`
- `this month`, `last month`, `this year`
- `last 30 days`, `last 90 days`, `3 months`
- Specific months: `February 2026`, `March ki sales`

---

### WF4 — Daily Sales Report
Automated morning sales report via Telegram.

**Trigger:** Schedule (daily 8:00 AM PKT)

**Flow:** Fetch Yesterday's Orders → Calculate Metrics → GPT-4o Summary → Telegram Message

---

### WF5 — CRM Lead Capture
Captures leads from dashboard form with AI scoring.

**Trigger:** Webhook `POST /lead-automation`

**Flow:** Validate Lead → GPT-4o-mini Score → Save to Supabase → Telegram Alert → Return to Dashboard

**Lead Priority Logic:**
- Score ≥ 70 → 🔥 Hot (Call within 2 hours)
- Score 40–69 → ⚡ Warm (Follow up today)
- Score < 40 → ❄️ Cold (Monitor)

---

### WF6 — Inventory Alert
Monitors stock levels and notifies suppliers.

**Trigger:** Schedule (every 6 hours)

**Flow:** Fetch Low Stock Products → GPT-4o Alert Message → Email Supplier → Telegram Notification

---

### WF7 — Customer Intelligence Analysis
Analyzes search patterns to identify demand gaps and opportunities.

**Trigger:** Schedule (every 6 hours) + Webhook `POST /analyze-customer-intelligence`

**Flow:** Fetch Search Logs → GPT-4o Trend Analysis → Save Insights → Return Report

**Output:**
- Top demanded products
- Demand gaps (searched but not found)
- Pricing alerts
- Revenue opportunity estimates

---

## Database Schema (Supabase)

```sql
-- Core Tables
businesses          -- Multi-tenant business profiles
woocommerce_products -- Synced product catalog
woocommerce_orders  -- Synced order history

-- AI & Analytics
crm_leads           -- Lead scoring and CRM pipeline
customer_search_logs -- Chatbot query history
ai_query_logs       -- Workflow execution logs
customer_insights   -- AI-generated trend analysis

-- Communication
telegram_sessions   -- Bot conversation state
```

### Row Level Security (RLS)
All tables enforce `business_id` isolation — businesses can only access their own data.

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Automation** | n8n (self-hosted) |
| **AI** | OpenAI GPT-4o, GPT-4o-mini, Whisper |
| **Database** | Supabase (PostgreSQL) |
| **eCommerce** | WooCommerce REST API |
| **Communication** | Telegram Bot API |
| **Frontend** | React + Recharts (Netlify) |
| **Chatbot Widget** | Vanilla JS (embedded on WooCommerce site) |

---

## Environment Variables

```env
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-anon-key
N8N_BASE_URL=https://your-n8n-instance.com
OPENAI_API_KEY=your-openai-key
TELEGRAM_BOT_TOKEN=your-bot-token
WOOCOMMERCE_URL=https://your-store.com
WOOCOMMERCE_CONSUMER_KEY=ck_xxxxx
WOOCOMMERCE_CONSUMER_SECRET=cs_xxxxx
```

---

## Dashboard

Live dashboard deployed on Netlify with:

- **Overview** — KPI cards (Revenue, Orders, Leads, AI ROI), trend charts
- **Sales** — Revenue vs Orders, status breakdown, monthly trends
- **Products** — Stock distribution, category revenue, price analysis
- **Customers** — Top customers, lifetime value, loyalty tiers
- **Inventory** — Low stock alerts, supplier notifications
- **Automation ROI** — AI tasks, hours saved, PKR value
- **AI Assistant** — Natural language sales queries

**Color Scheme:**
- Background: `#0D1117` Deep Midnight Navy
- Cards: `#1A2332` Slate Blue
- Accent: `#10B981` Emerald Green
- Revenue Chart: `#10B981 → transparent`
- Orders Chart: `#38BDF8` Sky Cyan
- Leads Chart: `#A78BFA` Purple
- Forecast Line: `#F59E0B` Amber dashed

---

## Chatbot Widget Integration

Add to any WooCommerce site:

```html
<script>
  window.BIZFLOW_CONFIG = {
    webhookUrl: 'https://your-n8n.com/webhook/chatbot-query',
    businessId: 'your-business-uuid',
    storeName: 'SK Natural Assistant',
    primaryColor: '#10B981'
  };
</script>
<script src="https://your-cdn.com/bizflow-widget.js"></script>
```

---

## Pricing Tiers

| Plan | Monthly | AI Queries | Workflows |
|---|---|---|---|
| **Starter** | PKR 5,000 | 1,000 | 3 |
| **Growth** | PKR 12,000 | 5,000 | 6 |
| **Enterprise** | PKR 25,000 | Unlimited | All |

---

## Quick Start

```bash
# 1. Clone repository
git clone https://github.com/your-org/bizflow-ai

# 2. Import n8n workflows
# Go to n8n → Workflows → Import from file
# Import all WF*.json files from /workflows directory

# 3. Set up Supabase
# Run schema.sql in Supabase SQL editor

# 4. Configure credentials in n8n
# - Supabase API
# - OpenAI API
# - Telegram Bot
# - WooCommerce API

# 5. Deploy dashboard
cd dashboard && npm install && npm run build
# Deploy /dist to Netlify
```

---

## Support

- **Telegram Bot:** @bizflow_support_bot
- **Email:** aiml.team31@gmail.com
- **Dashboard:** https://bizflowaierp.netlify.app/
---

*Built with ❤️ for Pakistani SMBs — BizFlow AI v2.0*
